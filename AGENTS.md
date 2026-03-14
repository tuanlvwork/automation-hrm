# AGENTS.md — AI-Powered Recruitment Automation Platform

> **Platform vision:** A multi-tenant SaaS recruitment platform targeting ITViec, IT companies, and recruitment agencies. Designed to scale to **100 000+ job postings and applications**. All core services are self-built (no dependency on JobAdder or Affinda).

Read this file **first** before making any changes to the codebase.

---

## 1. Project Overview

**Type:** Multi-tenant SaaS  
**Target customers:** IT recruitment agencies, IT companies, job boards (e.g. ITViec)  
**Scale target:** 100 000+ job postings and resume applications  
**Automation engine:** n8n (self-hosted)  
**AI engine:** OpenAI GPT-4o (or equivalent LLM)

### What this platform replaces
| External service | Replaced by |
|---|---|
| JobAdder (ATS) | Self-built ATS module |
| Affinda (resume parser) | Self-built LLM-powered resume parser |
| Make.com | n8n (self-hosted) |

---

## 2. System Architecture

### 2.1 Multi-Tenancy

Every data record must be scoped to a `tenant_id`.

- Each tenant = one agency or company
- Tenants are isolated: they cannot see each other's candidates, jobs, or scores
- A super-admin panel manages tenant provisioning and billing

### 2.2 High-Level Modules

```
┌─────────────────────────────────────────────────────┐
│                  SaaS Platform                      │
│                                                     │
│  ┌───────────┐  ┌───────────┐  ┌────────────────┐  │
│  │  Self-    │  │  AI Score │  │  Self-built    │  │
│  │  built    │  │  Engine   │  │  Resume Parser │  │
│  │  ATS      │  │           │  │  (LLM-powered) │  │
│  └─────┬─────┘  └─────┬─────┘  └───────┬────────┘  │
│        │              │                │            │
│  ┌─────▼──────────────▼────────────────▼────────┐  │
│  │              API Gateway (REST)               │  │
│  └─────────────────────┬─────────────────────────┘  │
│                        │                            │
│       ┌────────────────▼──────────────┐             │
│       │     n8n Automation Engine     │             │
│       └───────────────────────────────┘             │
└─────────────────────────────────────────────────────┘
```

---

## 3. Core Modules

### 3.1 Self-Built ATS

Replaces JobAdder. Core features required:

**Jobs**
- Create / edit / publish job postings
- Attach job ad (AI-generated)
- Job pipeline stages (applied → screened → shortlisted → interviewed → offered → hired)

**Candidates**
- Candidate profile (structured fields — see §6)
- Application history per candidate
- `suitability_score` field per application
- LinkedIn URL field (mandatory on application form)

**Applications**
- Link candidate ↔ job
- Store score, score breakdown, AI summary
- Tag top-20 flag per job

**Recruiter workspace**
- Sort applications by `suitability_score`
- View AI-generated ranking summary
- Shortlist / reject actions

---

### 3.2 Self-Built Resume Parser

Replaces Affinda. Built on **LLM-powered extraction**.

**Pipeline:**
1. Accept PDF or DOCX upload
2. Extract raw text using `PyMuPDF` (PDF) or `python-docx` (DOCX)
3. Send extracted text to OpenAI with a structured JSON extraction prompt
4. Validate and normalise output (skill taxonomy normalisation — see TO-DO)
5. Persist structured fields to the candidate database

**Extracted fields:**
| Field | Type |
|---|---|
| `name` | string |
| `email` | string |
| `phone` | string |
| `linkedin_url` | string |
| `skills` | string[] |
| `qualifications` | string[] |
| `employment_history` | EmploymentRecord[] |
| `sector_experience` | string[] |

**EmploymentRecord:**
```
{
  employer: string,
  employer_tier: int,        ← looked up from tier DB after parsing
  job_title: string,
  start_date: date,
  end_date: date | null,
  tenure_months: int
}
```

**Output:** Standardised Word resume using the provided template.  
**Language:** English first. Multilingual support in roadmap.

---

### 3.3 AI Candidate Scoring Engine

**Scoring inputs and default weights (recruiter-adjustable per job):**

| Signal | Default weight | Notes |
|---|---|---|
| Keyword relevance | 25% | JD keywords vs. resume skills |
| Job title match | 20% | Exact or adjacent title match |
| Employer tier | 20% | From employer tier DB (Excel, monthly sync) |
| Sector experience | 20% | Industry alignment |
| Tenure stability | 10% | Penalise < 12 months avg tenure |
| Negative signals | −5% cap | Unexplained gaps, mismatched industry |

**Output:** `suitability_score` (0–100) + per-signal breakdown  
**Weights:** Configurable per job by the recruiter. Global defaults set at tenant level.  
**Employer tier DB:** Excel file uploaded manually; auto-synced monthly by n8n.

---

### 3.4 Automated Candidate Shortlisting

Per job, after scoring completes:
- Tag top-20 candidates with `is_shortlisted = true`
- Enable sort by `suitability_score` in recruiter UI
- Generate AI summary (OpenAI) explaining why the candidate ranked highly

---

### 3.5 AI Job Ad Generation

Triggered when a recruiter publishes a job.

**Steps:**
1. n8n detects new job creation via webhook
2. Sends job details + company description to OpenAI
3. OpenAI generates ad following the **writing style guide** (provided document)
4. Generated ad is stored and shown to recruiter for one-click approval
5. Recruiter approves → ad goes live on the platform

---

### 3.6 LinkedIn Candidate Enrichment

**Recommended approach (tiered, cost-optimised):**

| Tier | Method | Cost |
|---|---|---|
| 1 (free) | Require LinkedIn URL as a **mandatory field** on all new application forms | $0 |
| 2 (paid fallback) | For historical candidates without a URL, call **Proxycurl API** to find by name + email | ~$0.01–0.03 per lookup |
| 3 (bulk enrichment) | For bulk historical candidate backfill, use **People Data Labs (PDL)** batch API | Usage-based |

**Decision:** Start with Tier 1 (mandatory field). Integrate Tier 2 as an optional on-demand enrichment button. Tier 3 for periodic batch jobs via n8n.

**Storage:** LinkedIn URL stored in candidate profile. Do not re-enrich if URL already exists.

---

### 3.7 Automatic Career Update Monitoring

- **Frequency:** Weekly (n8n cron job every Monday)
- **Lookback window:** Candidates active in the system within the last **2 years**
- **Data source:** Proxycurl LinkedIn profile refresh (Tier 2 above)
- **On change detected:** Update employer, job title, employment dates in candidate profile

---

### 3.8 n8n Automation Layer

All workflow orchestration runs on self-hosted **n8n**.

| Workflow | Trigger |
|---|---|
| Resume parse + score | Webhook on new application submitted |
| Job ad generation | Webhook on new job published |
| Top-20 tagging | After scoring workflow completes |
| Employer tier DB sync | Monthly cron |
| LinkedIn enrichment | On-demand webhook + weekly cron |
| Career update monitor | Weekly cron (Monday) |

---

## 4. Data Inputs (Provided Externally)

| Asset | Format | Update frequency |
|---|---|---|
| Employer Tier Database | Excel | Monthly (manual upload + auto-sync) |
| Sector Scoring Templates | Excel / JSON | As needed |
| Resume Output Template | Word (.docx) | Designed as part of this project |
| Job Ad Writing Style Guide | PDF / Doc | Designed as part of this project |

---

## 5. Database Schema (Core Tables)

All tables include `tenant_id` for multi-tenancy isolation.

```sql
tenants            (id, name, plan, created_at)
users              (id, tenant_id, role, email, ...)
jobs               (id, tenant_id, title, description, ad_text, status, ...)
candidates         (id, tenant_id, name, email, phone, linkedin_url,
                    skills[], qualifications[], sector_experience[],
                    last_career_check_at, ...)
employment_history (id, candidate_id, employer, employer_tier, job_title,
                    start_date, end_date, tenure_months)
applications       (id, job_id, candidate_id, suitability_score,
                    score_breakdown jsonb, ai_summary, is_shortlisted,
                    applied_at, ...)
scoring_weights    (id, job_id, tenant_id, keyword_weight, title_weight,
                    tier_weight, sector_weight, tenure_weight)
employer_tiers     (id, tenant_id, employer_name, tier, updated_at)
```

---

## 6. Technology Stack

| Layer | Technology |
|---|---|
| Backend API | Python (FastAPI) or Node.js (NestJS) |
| Database | PostgreSQL + pgvector extension |
| Resume text extraction | PyMuPDF (PDF), python-docx (DOCX) |
| AI / LLM | OpenAI GPT-4o |
| Automation | n8n (self-hosted) |
| LinkedIn enrichment | Proxycurl API / People Data Labs |
| File storage | S3-compatible (AWS S3 or MinIO) |
| Auth | JWT + tenant-scoped RBAC |
| Frontend | Next.js |

---

## 7. Critical Technical Requirements

1. **API-first:** All inter-service communication via REST APIs. No scraping.
2. **Modular:** Each module (parser, scorer, enricher) has a defined interface. Swapping a provider = replacing one adapter.
3. **Structured data only:** Candidate data always stored as structured fields, never free-text blobs.
4. **Multi-tenant isolation:** Every query must filter by `tenant_id`.
5. **Score write-back:** `suitability_score` must always be persisted to the `applications` table after scoring.
6. **No hardcoded secrets:** All API keys via environment variables.
7. **n8n workflows documented:** Every scenario must have a clear name and module labels.
8. **Employer tier DB respected:** Tier scores always read from DB, never hardcoded.

---

## 8. Agent Guidelines

When working in this repository:

- Read this file before any change
- Respect the multi-tenant `tenant_id` scope on every DB query
- Keep modules decoupled — one file/class per integration adapter
- Use the employer tier DB for all employer scoring (no hardcoding)
- All AI prompts must reference the writing style guide document
- New n8n workflows must be documented in `/docs/workflows/`
- English-only resume parsing for now — no multilingual handling yet
- LinkedIn URL is **mandatory** on new application forms — do not make it optional
