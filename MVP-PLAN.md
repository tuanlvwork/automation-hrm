# 🚀 Ship SaaS MVP — AI Recruitment Platform

> **Workflow:** `ship-saas-mvp` via `@antigravity-workflows`  
> **Project:** AI-powered multi-tenant recruitment automation platform  
> **Target:** ITViec · IT companies · Recruitment agencies  
> **Scale target:** 100 000+ resumes / job postings  

---

## Workflow Execution Status

| Phase | Name | Status |
|---|---|---|
| 1 | Idea Validation | ✅ Validated |
| 2 | Tech Stack Selection | ✅ Decided |
| 3 | Project Scaffold + Architecture | ✅ Designed |
| 4 | Auth + Multi-Tenancy | 🔲 Not started |
| 5 | Core MVP Modules | 🔲 Not started |
| 6 | Automation Layer (n8n) | 🔲 Not started |
| 7 | Pre-Launch Checklist | 🔲 Not started |

---

## Phase 1 — Idea Validation ✅

| Validation gate | Answer |
|---|---|
| Problem in one sentence | Recruiters waste hours manually screening resumes and writing job ads — this platform automates both using AI |
| Exact customer | IT recruitment agencies and HR teams at Vietnamese IT companies (ITViec customer base) |
| What they pay for today | JobAdder (~$150/mo), Affinda, manual recruiter time |
| Talks with customers | **(Action required)** Talk to 5 IT recruiters before building |
| Willingness to pay | Freemium + agency plan at $99–$299/mo |

> [!IMPORTANT]
> **Gate:** Confirm 3 recruiters are willing to pilot before writing code.

---

## Phase 2 — Tech Stack ✅

Adapted for 100k-scale multi-tenant SaaS with self-built ATS:

| Layer | Choice | Why |
|---|---|---|
| **Frontend** | Next.js 15 + TypeScript | Full-stack, App Router, Vercel deploy |
| **Styling** | Tailwind CSS + shadcn/ui | Fast, accessible, recruiter dashboard-ready |
| **Backend API** | FastAPI (Python) | Async LLM calls, type hints, OpenAPI out of the box |
| **Database** | PostgreSQL + pgvector | Structured candidate data + semantic search |
| **ORM** | SQLAlchemy 2.0 (async) + Alembic | Migrations, type safety |
| **Auth** | Clerk (multi-tenant, RBAC) | Tenant-scoped roles, social login, no custom auth |
| **Payments** | Stripe (subscriptions) | Agency plan billing |
| **File storage** | AWS S3 / MinIO | Resume PDF/DOCX + Word output |
| **AI / LLM** | OpenAI GPT-4o | Parse, score, generate, summarise |
| **Enrichment** | Proxycurl API | LinkedIn profile lookup |
| **Automation** | n8n (self-hosted) | All async workflows |
| **Email** | Resend + React Email | Notifications, outreach drafts |
| **Monitoring** | Sentry + PostHog | Error tracking + recruiter analytics |
| **Deployment** | Vercel (frontend) + Railway / Render (FastAPI) | Zero-config CI/CD |

---

## Phase 3 — Project Scaffold + Architecture ✅

Defined in `SYSTEM-DESIGN.md`. Directory structure:

```
automation-hrm/
├── frontend/                  # Next.js 15 recruiter + candidate app
│   ├── app/
│   │   ├── (auth)/            # Login, signup (Clerk)
│   │   ├── (dashboard)/       # Recruiter workspace
│   │   ├── (apply)/           # Candidate application forms
│   │   └── api/               # Next.js API routes (thin — delegate to FastAPI)
│   └── components/
│       ├── ui/                # shadcn/ui
│       └── recruitment/       # ATS-specific components
│
├── backend/                   # FastAPI (Hexagonal Architecture)
│   ├── domain/                # Entities, Value Objects, Ports
│   ├── use_cases/             # Business logic
│   ├── adapters/              # OpenAI, Proxycurl, PostgreSQL, S3
│   └── infrastructure/        # Config, DI, DB pool
│
├── n8n/                       # n8n workflow exports (JSON)
│   ├── parse-resume.json
│   ├── score-candidate.json
│   ├── generate-job-ad.json
│   └── enrich-linkedin.json
│
├── docs/
│   ├── workflows/             # n8n workflow documentation
│   ├── adr/                   # Architecture Decision Records
│   └── api/                   # OpenAPI spec
│
├── AGENTS.md
├── SYSTEM-DESIGN.md
├── ARCHITECTURE.md
└── TO-DO.md
```

---

## Phase 4 — Auth + Multi-Tenancy 🔲

**Artifact:** Working auth flow with tenant isolation

### Steps

- [ ] Install Clerk in Next.js frontend
- [ ] Configure `middleware.ts` to protect all `/dashboard/*` routes
- [ ] Create `tenants` table in PostgreSQL
- [ ] Implement tenant provisioning on first Clerk `user.created` webhook
- [ ] Add `tenant_id` to all DB tables (see `SYSTEM-DESIGN.md §8`)
- [ ] Implement RBAC: `super_admin`, `agency_admin`, `recruiter` roles
- [ ] Sync Clerk user → backend `users` table on login

### Completion Criteria

- [ ] Recruiter A cannot see Recruiter B's candidates
- [ ] Super admin can access all tenants
- [ ] Session survives page refresh

---

## Phase 5 — Core MVP Modules 🔲

Build in this order (each unlocks the next):

### 5.1 Resume Parser (Week 1–2)

**Artifact:** `POST /parse` returns structured `ParsedResume` JSON

- [ ] `PyMuPDF` text extraction for PDF
- [ ] `python-docx` text extraction for DOCX
- [ ] OpenAI GPT-4o structured extraction prompt
- [ ] `SkillSet.from_raw()` normalisation layer (see `SYSTEM-DESIGN.md §11`)
- [ ] Dedup check before candidate insert (fuzzy name + email)
- [ ] Upload original + Word-formatted resume to S3

**Completion criteria:** Upload 10 test resumes — all parse correctly, skills normalised, no duplicates

---

### 5.2 Self-Built ATS (Week 2–3)

**Artifact:** Recruiter can create a job, see applications, and move candidates through pipeline stages

- [ ] Jobs CRUD (create, publish, archive)
- [ ] Application form (candidate-facing) with mandatory LinkedIn URL field
- [ ] Application list view (sort by score)
- [ ] Pipeline stages: Applied → Screened → Shortlisted → Interviewed → Offered → Hired
- [ ] Top-20 tagged candidates highlighted in UI

---

### 5.3 AI Scoring Engine (Week 3)

**Artifact:** `POST /score` returns `SuitabilityScore(0-100)` + breakdown per signal

- [ ] Load employer tier DB from PostgreSQL (`employer_tiers` table)
- [ ] Load scoring weights from job record (`scoring_weights` table)
- [ ] Implement 5 scoring signals (keyword, title, tier, sector, tenure)
- [ ] Cap negative signal at −5%
- [ ] Write score to `applications.suitability_score`
- [ ] Auto-tag top-20 per job after each scoring run

**Completion criteria:** Score 20 sample candidates against 3 jobs — scores are consistent and explainable

---

### 5.4 AI Job Ad Generator (Week 3–4)

**Artifact:** Recruiter publishes job → AI draft auto-generated → one-click approve

- [ ] Load job ad writing style guide (PDF → text)
- [ ] OpenAI prompt: job details + company + style guide → ad text
- [ ] Save draft (status: `pending_approval`)
- [ ] Recruiter approval flow → status: `live`

---

### 5.5 LinkedIn Enrichment (Week 4)

**Artifact:** All new applications auto-populate LinkedIn URL; historical candidates enriched on demand

- [ ] Tier 1: Mandatory LinkedIn field on application form (frontend validation)
- [ ] Tier 2: On-demand "Enrich" button → calls Proxycurl → saves URL
- [ ] Never overwrite existing LinkedIn URL (see `SYSTEM-DESIGN.md §10`)

---

### 5.6 Billing (Week 4–5)

**Artifact:** Agency can subscribe, upgrade, and cancel via Stripe

- [ ] Stripe Products: Starter ($49), Agency ($149), Enterprise (custom)
- [ ] Checkout → webhook → update `subscriptions` table
- [ ] Feature gates per plan (e.g., bulk import = Agency+)

---

## Phase 6 — n8n Automation Layer 🔲

**Artifact:** All 6 core workflows running end-to-end in n8n

| Workflow | Trigger | Steps |
|---|---|---|
| `parse-score` | Webhook: new application | Parse → Dedup → Upsert → Score → Tag top-20 → AI summary |
| `generate-job-ad` | Webhook: job published | Load job → OpenAI → Save draft → Notify recruiter |
| `enrich-weekly` | Cron: Mon 08:00 | Query candidates → Proxycurl → Update careers |
| `tier-db-sync` | Cron: 1st of month | Load Excel → Parse → Upsert `employer_tiers` |
| `bulk-import` | Manual trigger | ZIP upload → S3 → parse-score for each resume |
| `career-monitor` | Cron: Mon 08:00 | Fetch active candidates (2yr) → check for role changes |

### Completion Criteria

- [ ] Upload a resume → score appears in ATS within 60 seconds
- [ ] Publish a job → ad draft appears within 30 seconds
- [ ] Enrich a candidate → LinkedIn URL saved (or graceful skip if not found)

---

## Phase 7 — Pre-Launch Checklist 🔲

### Technical
- [ ] Auth: signup, login, logout, password reset all work
- [ ] Payments: subscribe, cancel, upgrade end-to-end
- [ ] Rate limiting on all API routes (per-tenant token bucket)
- [ ] Input validation (Pydantic on backend, Zod on frontend)
- [ ] Sentry error monitoring configured
- [ ] HTTPS enforced, CORS configured
- [ ] PostgreSQL backups automated (daily)
- [ ] All env vars documented in `.env.example`
- [ ] `tenant_id` on every DB query verified (integration tests)

### Product
- [ ] Landing page with clear value prop for recruiters
- [ ] Pricing page (Starter / Agency / Enterprise)
- [ ] Onboarding: first parsed resume within 5 minutes of signup
- [ ] Welcome email sequence (Resend)
- [ ] Terms of Service + Privacy Policy

### Marketing
- [ ] Domain purchased and configured
- [ ] SEO meta tags on all pages
- [ ] PostHog analytics installed
- [ ] ITViec partnership contact made
- [ ] Product Hunt draft page ready

---

## Risks & Mitigations

| Risk | Likelihood | Mitigation |
|---|---|---|
| OpenAI parsing quality varies by resume format | Medium | Fine-tune extraction prompt; add human review flag for low-confidence parses |
| Proxycurl rate limits at scale | Medium | Cache LinkedIn URLs; batch enrichment; fallback to mandatory field |
| n8n self-hosted reliability | Low | Run on dedicated VPS; monitor with UptimeRobot; add dead-letter queue |
| LLM cost at 100k resumes | High | Batch resumes during off-peak; use GPT-4o-mini for parsing, GPT-4o for scoring summaries |
| Employer tier DB grows stale | Medium | Monthly sync cron + admin alert when tier is missing for new employer |

---

## Suggested Next Action

> **Start Phase 4** — Auth + Multi-Tenancy  
> This unblocks all other phases. Estimated time: **2–3 days**.

Run:
```bash
# Frontend: install Clerk
cd frontend && npx create-next-app@latest . --typescript --tailwind --app
npx shadcn@latest init
npm install @clerk/nextjs

# Backend: scaffold FastAPI
cd backend
uv init && uv add fastapi uvicorn sqlalchemy asyncpg alembic pydantic
```
