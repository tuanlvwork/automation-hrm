# TO-DO.md — Future Improvements & Eureka Ideas

This file tracks improvement ideas and future enhancements for the platform. Work through these after the core MVP is stable.

---

## 💡 Eureka Ideas Backlog

### 1. 🧠 Semantic Search over Candidate Database
**What:** Embed all candidate profiles using OpenAI embeddings and store in pgvector. Enable natural-language recruiter search.  
**Example query:** *"Find me a senior DevOps engineer with fintech experience and 5+ years at Tier 1 companies"*  
**Tech:** `pgvector` PostgreSQL extension + OpenAI `text-embedding-3-small`  
**Value:** Eliminates Boolean query skills gap; dramatically improves talent discovery  
**Priority:** High

---

### 2. 📊 Recruiter Dashboard with Score Analytics
**What:** Web dashboard showing score distribution per job, which scoring signals are most impactful, and time-to-shortlist metrics.  
**Value:** Gives recruiters transparency and explainability into AI decisions  
**Priority:** Medium

---

### 3. 🔄 AI-Assisted Score Calibration (Feedback Loop)
**What:** After a recruiter hires someone, feed the outcome back as a training signal. Over time, scoring weights auto-tune to match each recruiter's hiring preferences.  
**Tech:** Collect `hired` outcomes → re-weight scoring signals per tenant  
**Value:** Self-improving system that gets smarter with every hire  
**Priority:** Medium (post-MVP)

---

### 4. 📨 Automated Candidate Outreach Drafts
**What:** After shortlisting top candidates, auto-generate a personalised outreach email per candidate (referencing their specific experience). Recruiter sees a one-click send/edit UI.  
**Tech:** OpenAI GPT-4o + candidate profile data  
**Value:** Saves hours of manual outreach writing per job  
**Priority:** Medium

---

### 5. 🏷️ Skill Taxonomy Normalisation
**What:** Build a normalisation layer that maps raw skill strings to a canonical taxonomy (e.g. "JS" → "JavaScript", "ES6" → "JavaScript"). Dramatically improves scoring accuracy and search consistency.  
**Tech:** Static mapping table + fuzzy match + optional LLM fallback  
**Value:** Prevents skill fragmentation in the DB; makes search and scoring reliable  
**Priority:** High (should be included in MVP parser pipeline)

---

### 6. 🕵️ Duplicate Candidate Detection
**What:** Before creating a new candidate record, run a deduplication check using fuzzy name + email + phone matching. Prevents database pollution from repeat applicants.  
**Tech:** `pg_trgm` fuzzy matching or Levenshtein distance  
**Value:** Keeps candidate DB clean at scale (100k+ records)  
**Priority:** High

---

### 7. ⏱️ Candidate Freshness Score
**What:** Add a "freshness" signal to the suitability score. Candidates who recently changed jobs or updated their profile are more likely to be actively looking. Surface "warm" candidates automatically.  
**Tech:** Combine career update monitor (§2.7) with a recency decay function  
**Value:** Prioritises candidates most likely to respond to outreach  
**Priority:** Medium

---

### 8. 🗂️ Job Ad A/B Testing
**What:** Generate two tone variants of each job ad (e.g. corporate vs. casual). Track which version generates more applications. Use the winning data to refine the style guide over time.  
**Tech:** Store variant + application count; surface winner after N applications  
**Value:** Data-driven job ad optimisation; improves application conversion rate  
**Priority:** Low (post-MVP)

---

### 9. 🌐 Multilingual Resume Parsing
**What:** Extend the resume parser to handle Vietnamese and other Southeast Asian languages (after English MVP is stable).  
**Tech:** OpenAI GPT-4o multilingual prompt + language detection  
**Value:** Critical for ITViec and Vietnam-market expansion  
**Priority:** Medium (roadmap after English MVP)

---

### 10. 🔔 Candidate Re-engagement Alerts
**What:** When a previously rejected candidate's score improves (e.g. new employer, new skills detected via career monitor), alert the recruiter that they are now worth reconsidering.  
**Tech:** Career update monitor → re-score → compare to previous score → trigger alert if Δ > threshold  
**Value:** Recovers value from the existing candidate pool without new sourcing cost  
**Priority:** Medium

---

### 11. 📁 Bulk Resume Import
**What:** Allow tenants to bulk-upload a ZIP of resumes to onboard historical candidate databases. n8n processes each resume through the parse → score pipeline.  
**Tech:** ZIP upload → S3 → n8n bulk processing workflow  
**Value:** Enables warm launch — tenants can onboard their existing candidate DB on day one  
**Priority:** High (needed for onboarding)

---

### 12. 🔗 Job Board API Integration (ITViec / LinkedIn Jobs)
**What:** Push published job ads to external job boards (ITViec, LinkedIn) via their APIs. Pull applications back into the platform automatically.  
**Tech:** ITViec API (if available) / LinkedIn Job Posting API  
**Value:** Removes need for recruiters to manually re-post on every board  
**Priority:** Medium (roadmap)

---

## 📋 MVP Core Checklist (Not improvements — required for launch)

- [ ] Multi-tenant SaaS scaffold (tenant isolation, auth, RBAC)
- [ ] Self-built ATS (jobs, candidates, applications, pipeline)
- [ ] Self-built resume parser (PDF/DOCX → structured data via LLM)
- [ ] Word resume reformatter (standardised output template)
- [ ] AI Scoring Engine (configurable weights per job)
- [ ] Top-20 auto-tagging + AI ranking summary
- [ ] AI Job Ad Generator (with style guide)
- [ ] LinkedIn URL mandatory field + Proxycurl enrichment fallback
- [ ] Career update monitor (weekly n8n cron, 2-year window)
- [ ] Employer tier DB (Excel upload + monthly sync)
- [ ] n8n automation workflows (all core triggers)
- [ ] Recruiter UI (Next.js)
- [ ] Skill taxonomy normalisation layer (Idea #5)
- [ ] Duplicate candidate detection (Idea #6)
