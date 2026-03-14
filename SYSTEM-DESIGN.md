# SYSTEM-DESIGN.md — AI Recruitment Platform

System design best practices applied to this platform, based on:
- **Clean Architecture** (Uncle Bob)
- **Hexagonal Architecture** (Ports & Adapters)
- **Domain-Driven Design** (DDD)
- **Scalability & Resilience patterns** for 100k+ scale

> All agents and developers must read this file alongside `AGENTS.md`.

---

## 1. Architecture Style: Hexagonal + Clean Architecture

The backend uses **Hexagonal Architecture** (Ports & Adapters) so every external dependency — OpenAI, Proxycurl, PostgreSQL, S3 — can be swapped without touching business logic.

```
  ┌──────────────────────────────────────────────────────────┐
  │                     Domain Core                          │
  │  Entities · Value Objects · Aggregates · Domain Events   │
  │                                                          │
  │  ┌────────────────────────────────────────────────────┐  │
  │  │                   Use Cases                        │  │
  │  │  ScoreCandidate · ParseResume · GenerateJobAd      │  │
  │  │  EnrichCandidate · ShortlistCandidates             │  │
  │  └────────────────────────────────────────────────────┘  │
  └──────────────────────┬───────────────────────────────────┘
                         │  Ports (interfaces)
             ┌───────────┴────────────┐
             │                        │
  ┌──────────▼──────┐      ┌──────────▼──────────────────────┐
  │  Primary Ports  │      │       Secondary Ports            │
  │  (Driving)      │      │       (Driven)                   │
  │                 │      │                                  │
  │  REST API       │      │  IResumeParser                   │
  │  n8n Webhooks   │      │  IScoringEngine                  │
  │  Cron triggers  │      │  IJobAdGenerator                 │
  │                 │      │  IEnrichmentProvider             │
  └──────────┬──────┘      │  ICandidateRepository            │
             │              │  IJobRepository                  │
  ┌──────────▼──────────────▼────────────────────────────────┐
  │                      Adapters                            │
  │                                                          │
  │  OpenAIResumeParser   │  ProxycurlEnrichmentAdapter      │
  │  OpenAIScoringAdapter │  PostgresCandidateRepository     │
  │  OpenAIAdGenAdapter   │  S3FileStorageAdapter            │
  └──────────────────────────────────────────────────────────┘
```

**Dependency rule:** Domain core has zero knowledge of adapters. All arrows point inward.

---

## 2. Bounded Contexts (DDD Strategic Design)

The platform is split into **4 bounded contexts**. Each context owns its data and communicates via domain events.

```
  ┌──────────────────┐     ┌──────────────────┐
  │  Recruitment     │     │  Candidate       │
  │  Context         │     │  Intelligence    │
  │                  │     │  Context         │
  │  Job · Pipeline  │────►│  Profile · Score │
  │  Application     │     │  Resume · Skills │
  └──────────────────┘     └────────┬─────────┘
                                    │
  ┌──────────────────┐     ┌────────▼─────────┐
  │  Enrichment      │     │  Tenant &        │
  │  Context         │     │  Auth Context    │
  │                  │     │                  │
  │  LinkedIn URL    │     │  Tenant · User   │
  │  Career Updates  │     │  RBAC · Billing  │
  └──────────────────┘     └──────────────────┘
```

| Context | Owns | Communicates via |
|---|---|---|
| **Recruitment** | Jobs, Applications, Pipeline stages | `ApplicationSubmittedEvent` |
| **Candidate Intelligence** | Candidate profiles, scores, skills | `CandidateScoredEvent`, `ResumeParseCompletedEvent` |
| **Enrichment** | LinkedIn URLs, career updates | `CandidateEnrichedEvent` |
| **Tenant & Auth** | Tenants, users, RBAC | Synchronous (auth middleware) |

---

## 3. Project Directory Structure

```
app/
├── domain/                      ← Core business rules (no framework deps)
│   ├── entities/
│   │   ├── candidate.py         ← Candidate aggregate root
│   │   ├── job.py               ← Job entity
│   │   ├── application.py       ← Application entity
│   │   └── tenant.py            ← Tenant entity
│   ├── value_objects/
│   │   ├── email.py             ← Validated email VO
│   │   ├── suitability_score.py ← Score(0-100) VO with validation
│   │   ├── employment_record.py ← Immutable employment history entry
│   │   └── skill_set.py         ← Normalised skill set VO
│   ├── events/
│   │   ├── application_submitted.py
│   │   ├── candidate_scored.py
│   │   ├── resume_parsed.py
│   │   └── candidate_enriched.py
│   └── interfaces/              ← Ports (abstract contracts)
│       ├── i_resume_parser.py
│       ├── i_scoring_engine.py
│       ├── i_job_ad_generator.py
│       ├── i_enrichment_provider.py
│       ├── i_candidate_repository.py
│       └── i_job_repository.py
│
├── use_cases/                   ← Application business rules
│   ├── parse_resume.py
│   ├── score_candidate.py
│   ├── shortlist_candidates.py
│   ├── generate_job_ad.py
│   └── enrich_candidate.py
│
├── adapters/                    ← Implementations of ports
│   ├── parsers/
│   │   └── openai_resume_parser.py
│   ├── scoring/
│   │   └── openai_scoring_engine.py
│   ├── ad_generation/
│   │   └── openai_ad_generator.py
│   ├── enrichment/
│   │   ├── proxycurl_adapter.py
│   │   └── pdl_adapter.py
│   ├── repositories/
│   │   ├── postgres_candidate_repository.py
│   │   └── postgres_job_repository.py
│   ├── storage/
│   │   └── s3_file_storage.py
│   └── controllers/             ← HTTP layer (FastAPI routers)
│       ├── application_controller.py
│       ├── job_controller.py
│       ├── scoring_controller.py
│       └── enrichment_controller.py
│
└── infrastructure/              ← Framework config, DI container
    ├── database.py
    ├── config.py
    ├── logging.py
    └── container.py             ← Dependency injection wiring
```

---

## 4. Domain Entities & Value Objects

### Key Value Objects

```python
# domain/value_objects/suitability_score.py
@dataclass(frozen=True)
class SuitabilityScore:
    value: int  # 0-100

    def __post_init__(self):
        if not 0 <= self.value <= 100:
            raise ValueError(f"Score must be 0-100, got {self.value}")

    def is_shortlistable(self, threshold: int = 70) -> bool:
        return self.value >= threshold

# domain/value_objects/employment_record.py
@dataclass(frozen=True)
class EmploymentRecord:
    employer: str
    employer_tier: int          # 1-5 from tier DB
    job_title: str
    start_date: date
    end_date: Optional[date]    # None = current role

    @property
    def tenure_months(self) -> int:
        end = self.end_date or date.today()
        return (end.year - self.start_date.year) * 12 + \
               (end.month - self.start_date.month)

    @property
    def is_stable(self) -> bool:
        return self.tenure_months >= 12
```

### Candidate Aggregate Root

```python
# domain/entities/candidate.py
class Candidate:
    """Aggregate root — controls all mutations to candidate data."""

    def __init__(self, id: str, tenant_id: str, email: Email, name: str):
        self.id = id
        self.tenant_id = tenant_id                # multi-tenant isolation
        self.email = email
        self.name = name
        self.skills: SkillSet = SkillSet.empty()
        self.employment_history: list[EmploymentRecord] = []
        self.linkedin_url: Optional[str] = None
        self._events: list[DomainEvent] = []

    def apply_parsed_resume(self, parsed: ParsedResume) -> None:
        """Update candidate from parsed resume data."""
        self.skills = parsed.skills
        self.employment_history = parsed.employment_history
        self._events.append(ResumeParseCompletedEvent(self.id))

    def update_career(self, updated: EmploymentRecord) -> None:
        """Apply career update — detected by enrichment monitor."""
        # replace matching record or append new
        self._update_history(updated)
        self._events.append(CandidateCareerUpdatedEvent(self.id))

    def enrich_linkedin(self, url: str) -> None:
        if self.linkedin_url:
            return  # never overwrite existing URL
        self.linkedin_url = url
        self._events.append(CandidateEnrichedEvent(self.id))

    @property
    def avg_tenure_months(self) -> float:
        if not self.employment_history:
            return 0
        return sum(r.tenure_months for r in self.employment_history) \
               / len(self.employment_history)
```

---

## 5. Port Interfaces (Contracts)

```python
# domain/interfaces/i_resume_parser.py
class IResumeParser(ABC):
    @abstractmethod
    async def parse(self, file_bytes: bytes, mime_type: str) -> ParsedResume:
        """Extract structured data from PDF or DOCX bytes."""
        ...

# domain/interfaces/i_scoring_engine.py
class IScoringEngine(ABC):
    @abstractmethod
    async def score(
        self,
        candidate: Candidate,
        job: Job,
        weights: ScoringWeights,
        employer_tiers: dict[str, int]
    ) -> ScoringResult:
        """Return score 0-100 + per-signal breakdown."""
        ...

# domain/interfaces/i_enrichment_provider.py
class IEnrichmentProvider(ABC):
    @abstractmethod
    async def find_linkedin(self, name: str, email: str) -> Optional[str]:
        """Return LinkedIn URL or None if not found."""
        ...

    @abstractmethod
    async def get_current_role(self, linkedin_url: str) -> Optional[EmploymentRecord]:
        """Return latest employment record or None."""
        ...
```

---

## 6. Use Case Layer

```python
# use_cases/score_candidate.py
class ScoreCandidateUseCase:
    def __init__(
        self,
        scoring_engine: IScoringEngine,           # injected port
        candidate_repo: ICandidateRepository,
        job_repo: IJobRepository,
        employer_tier_repo: IEmployerTierRepository
    ):
        self._engine = scoring_engine
        self._candidates = candidate_repo
        self._jobs = job_repo
        self._tiers = employer_tier_repo

    async def execute(self, cmd: ScoreCandidateCommand) -> ScoringResult:
        candidate = await self._candidates.find_by_id(
            cmd.candidate_id, cmd.tenant_id
        )
        job = await self._jobs.find_by_id(cmd.job_id, cmd.tenant_id)
        weights = job.scoring_weights or ScoringWeights.defaults()
        tiers = await self._tiers.get_all(cmd.tenant_id)

        result = await self._engine.score(candidate, job, weights, tiers)

        # Update application record via domain event
        candidate.record_score(cmd.job_id, result.score)
        await self._candidates.save(candidate)

        return result
```

**Rule:** Use cases contain **all business logic**. Controllers only call use cases. Adapters only implement ports.

---

## 7. Scalability Design (100k+ Scale)

### 7.1 Database

| Pattern | Implementation | Why |
|---|---|---|
| **Read replicas** | PostgreSQL streaming replica | Offload score queries and search |
| **Connection pooling** | PgBouncer | Handle 100k+ concurrent connections |
| **Partitioning** | `applications` table partitioned by `tenant_id` | Isolate tenant query load |
| **Vector index** | `pgvector` HNSW index on candidate embeddings | Sub-10ms semantic search at scale |
| **Async writes** | Score results queued, written async | Don't block API response on DB write |

### 7.2 API

| Pattern | Implementation | Why |
|---|---|---|
| **Async endpoints** | FastAPI `async def` throughout | Non-blocking I/O for LLM calls |
| **Rate limiting** | Per-tenant token bucket | Prevent one tenant starving others |
| **Pagination** | Cursor-based (not offset) | Stable pagination at 100k rows |
| **Response caching** | Redis cache on employer tier lookups | Avoid DB hit per scoring call |

### 7.3 Async Processing

All LLM calls (parse, score, generate ad) are **async via n8n** — never synchronous in the HTTP request:

```
HTTP Request ──► API saves record ──► Publishes webhook event ──► n8n picks up
                                                                        │
                                                            ┌───────────▼───────┐
                                                            │  LLM processing   │
                                                            │  (async, retried) │
                                                            └───────────────────┘
```

### 7.4 Resilience Patterns

| Pattern | Where applied |
|---|---|
| **Retry with backoff** | All LLM API calls (OpenAI, Proxycurl) |
| **Circuit breaker** | Per external provider — fail fast when a provider is down |
| **Idempotent webhooks** | n8n webhook handlers check for duplicate `event_id` before processing |
| **Dead letter queue** | Failed n8n executions → DLQ → manual review |
| **Graceful degradation** | If enrichment provider fails → skip enrichment, don't fail application submission |

---

## 8. Multi-Tenancy Patterns

Every repository method **always filters by `tenant_id`**. This is enforced at the repository layer, not the controller.

```python
# adapters/repositories/postgres_candidate_repository.py
class PostgresCandidateRepository(ICandidateRepository):

    async def find_by_id(self, candidate_id: str, tenant_id: str) -> Candidate:
        """tenant_id is REQUIRED — never omit."""
        row = await self.pool.fetchrow(
            "SELECT * FROM candidates WHERE id = $1 AND tenant_id = $2",
            candidate_id, tenant_id
        )
        if not row:
            raise CandidateNotFoundError(candidate_id)
        return self._to_entity(row)

    async def search(self, query: CandidateQuery, tenant_id: str) -> list[Candidate]:
        """All search queries include tenant filter."""
        ...
```

**Rule:** If `tenant_id` is missing from any DB query, it is a **critical bug**.

---

## 9. Architecture Decision Records (ADRs)

| # | Decision | Rationale |
|---|---|---|
| ADR-001 | **Hexagonal Architecture** | External providers (OpenAI, Proxycurl) must be swappable without code changes |
| ADR-002 | **PostgreSQL + pgvector** (not separate vector DB) | Reduces operational complexity; pgvector satisfies scale at 100k candidates |
| ADR-003 | **n8n for async orchestration** (not Celery/RQ) | Visual workflows easier for team; self-hosted; sufficient at current scale |
| ADR-004 | **OpenAI for resume parsing** (not dedicated parser API) | LLM extraction quality >> regex/ML parsers; one vendor fewer |
| ADR-005 | **Cursor-based pagination** instead of offset | Stable at high volume; offset breaks under concurrent inserts |
| ADR-006 | **Mandatory LinkedIn field in application form** | Eliminates enrichment API cost for new candidates; enrichment only for backfill |
| ADR-007 | **Score written as domain event, not direct DB update** | Decouples scoring from persistence; enables audit trail and replay |

---

## 10. Anti-Patterns to Avoid

| Anti-pattern | Why forbidden here |
|---|---|
| Business logic in controllers | Controllers delegate to use cases only |
| Direct DB calls from use cases | Use cases call repository ports only |
| Hardcoded employer tier scores | Always loaded from `employer_tiers` DB table |
| `tenant_id`-less DB queries | Causes cross-tenant data leaks |
| Synchronous LLM calls in HTTP request | Blocks thread for 2–10s; kills throughput |
| Overwriting existing LinkedIn URL | Enrichment only adds, never overwrites confirmed data |
| Fat repositories (business logic inside) | Repositories map data only; no business rules |

---

## 11. Skill Taxonomy Normalisation (MVP-Required)

Before storing any skill from a parsed resume, it must pass through the normaliser:

```python
# domain/value_objects/skill_set.py
SKILL_ALIASES: dict[str, str] = {
    "js": "JavaScript", "javascript": "JavaScript", "es6": "JavaScript",
    "ts": "TypeScript", "typescript": "TypeScript",
    "py": "Python", "python3": "Python",
    "k8s": "Kubernetes", "kube": "Kubernetes",
    "pg": "PostgreSQL", "postgres": "PostgreSQL",
    "ml": "Machine Learning",
    # ... extend with provided sector templates
}

@dataclass(frozen=True)
class SkillSet:
    skills: frozenset[str]

    @classmethod
    def from_raw(cls, raw_skills: list[str]) -> "SkillSet":
        normalised = {
            SKILL_ALIASES.get(s.lower().strip(), s.strip().title())
            for s in raw_skills
            if s.strip()
        }
        return cls(skills=frozenset(normalised))
```

---

## 12. Validation Checklist (Pre-Implementation)

Before starting any feature:

- [ ] Which bounded context does this belong to?
- [ ] Does the domain entity handle the business rule, or is it in the wrong layer?
- [ ] Is the external dependency behind an interface (port)?
- [ ] Does every DB query include `tenant_id`?
- [ ] Is the LLM call async (via n8n or background task)?
- [ ] Is there retry + circuit breaker on the external call?
- [ ] Does the use case emit a domain event for downstream consumers?
- [ ] Are skill strings normalised before storage?
