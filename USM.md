# USM.md — User Story Map
# AI Recruitment Platform

> **Format:** Activity → Task → User Story (prioritized by release)
> **Users:** Candidate · Recruiter · Agency Admin · Super Admin
> **Releases:** 🔴 MVP · 🟠 V1.1 · 🟡 V2.0 · 🔵 V3.0
> **Sources:** STITCH-DESIGN.md · AGENTS.md · SYSTEM-DESIGN.md · TO-DO.md

---

## How to Read This Map

```
ACTIVITY     →  High-level goal the user wants to achieve
  TASK       →  Specific thing they do to accomplish the activity
    Story    →  As a [user], I want to [action] so that [benefit]
```

Each story is tagged: `🔴 MVP` / `🟠 V1.1` / `🟡 V2.0`
and mapped to a **Screen** from `STITCH-DESIGN.md`.

---

## USER 1 — CANDIDATE

### A1 · Discover Jobs

| Task | User Story | Release | Screen |
|---|---|---|---|
| Browse job listings | As a candidate, I want to see all open IT jobs so I can find relevant opportunities | 🔴 MVP | S4 |
| Search by keyword | As a candidate, I want to search jobs by title or skill so I can find matching roles fast | 🔴 MVP | S4 |
| Filter by type/location | As a candidate, I want to filter jobs by remote, type, and seniority so I can narrow down options | 🔴 MVP | S4 |
| View job detail | As a candidate, I want to read the full job description before applying so I can assess fit | 🔴 MVP | S5 |
| Save a job | As a candidate, I want to bookmark a job so I can apply later | 🟠 V1.1 | S5 |

---

### A2 · Apply for a Job

| Task | User Story | Release | Screen |
|---|---|---|---|
| Fill personal details | As a candidate, I want to enter my name, email, and phone so the recruiter can contact me | 🔴 MVP | S6 |
| Provide LinkedIn URL | As a candidate, I want to submit my LinkedIn URL so my career history can be verified automatically | 🔴 MVP | S6 |
| Upload resume | As a candidate, I want to upload my CV (PDF/Word) so AI can parse my details | 🔴 MVP | S6 |
| Add cover note | As a candidate, I want to add an optional cover note to personalise my application | 🔴 MVP | S6 |
| Receive confirmation | As a candidate, I want to see a confirmation page after submitting so I know my application was received | 🔴 MVP | S7 |
| Receive confirmation email | As a candidate, I want to receive a confirmation email so I have a record of my application | 🟠 V1.1 | — |
| Track application status | As a candidate, I want to see where my application is in the pipeline so I feel informed | 🟡 V2.0 | — |

---

## USER 2 — RECRUITER

### A3 · Authenticate & Access Platform

| Task | User Story | Release | Screen |
|---|---|---|---|
| Log in | As a recruiter, I want to log in with my email/password or Google so I can access my workspace | 🔴 MVP | S1 |
| Reset password | As a recruiter, I want to reset my password via email so I'm never locked out | 🔴 MVP | S3 |
| Switch agency | As a recruiter belonging to multiple agencies, I want to switch workspaces so I can manage each separately | 🟠 V1.1 | S26 |

---

### A4 · Manage Jobs

| Task | User Story | Release | Screen |
|---|---|---|---|
| View all jobs | As a recruiter, I want to see all my agency's jobs in one list so I can manage them easily | 🔴 MVP | S10 |
| Create a new job | As a recruiter, I want to fill in a job creation form so the position is posted on the platform | 🔴 MVP | S11 |
| Edit a job | As a recruiter, I want to edit an existing job's details so I can keep it accurate | 🔴 MVP | S11 |
| Publish / unpublish a job | As a recruiter, I want to toggle a job between draft and active so I control when candidates see it | 🔴 MVP | S10 |
| Close a job | As a recruiter, I want to mark a job as closed so no new applications are accepted | 🔴 MVP | S10 |
| Customise pipeline stages | As a recruiter, I want to configure stages for a job so the pipeline matches my process | 🟠 V1.1 | S11 |
| Duplicate a job | As a recruiter, I want to clone an existing job so I can post a similar role quickly | 🟠 V1.1 | S10 |

---

### A5 · Generate AI Job Ads

| Task | User Story | Release | Screen |
|---|---|---|---|
| Enter job details | As a recruiter, I want to fill in key job info so the AI has enough context to write an ad | 🔴 MVP | S12 |
| Generate ad | As a recruiter, I want the AI to produce a job ad draft so I don't write from scratch | 🔴 MVP | S12 |
| Preview the ad | As a recruiter, I want to preview the formatted ad before publishing so I can catch errors | 🔴 MVP | S12 |
| Regenerate ad | As a recruiter, I want to regenerate the ad if I'm unhappy with the first version | 🔴 MVP | S12 |
| Edit ad manually | As a recruiter, I want to manually edit the generated ad so I can personalise it | 🔴 MVP | S12 |
| Approve and publish ad | As a recruiter, I want to approve the final ad so it goes live on the job board | 🔴 MVP | S12 |
| Select ad tone | As a recruiter, I want to choose the tone (professional/casual) so the ad matches our culture | 🟠 V1.1 | S12 |

---

### A6 · Review Applications & Scores

| Task | User Story | Release | Screen |
|---|---|---|---|
| View scored applications | As a recruiter, I want to see all applicants for a job ranked by AI score so I can focus on the best fits | 🔴 MVP | S13 |
| Filter applications | As a recruiter, I want to filter by shortlisted / reviewed / rejected so I manage my workflow | 🔴 MVP | S13 |
| View score breakdown | As a recruiter, I want to see why a candidate scored a certain way so I trust the AI's reasoning | 🔴 MVP | S15 |
| View AI summary | As a recruiter, I want to read an AI-generated summary for each candidate so I can quickly assess them | 🔴 MVP | S15 |
| Override scoring weights | As a recruiter, I want to adjust signal weights per job so I can tune scoring for each role | 🔴 MVP | S13 |
| Recalculate scores | As a recruiter, I want to trigger a rescore after adjusting weights so results update immediately | 🔴 MVP | S13 |
| Shortlist a candidate | As a recruiter, I want to star/shortlist a candidate so the top 20 are clearly marked | 🔴 MVP | S13 |
| Reject a candidate | As a recruiter, I want to reject an application so I keep my pipeline clean | 🔴 MVP | S13, S15 |
| Export applications to CSV | As a recruiter, I want to export scored applications so I can share data with my team | 🟠 V1.1 | S13 |

---

### A7 · Manage Candidate Pipeline

| Task | User Story | Release | Screen |
|---|---|---|---|
| View pipeline as Kanban | As a recruiter, I want to see candidates arranged by pipeline stage so I understand the hiring funnel at a glance | 🔴 MVP | S14 |
| Move candidate to next stage | As a recruiter, I want to drag a candidate card to the next stage so the pipeline stays current | 🔴 MVP | S14 |
| View candidate full profile | As a recruiter, I want to open a candidate's detailed profile so I can review employment history and skills | 🔴 MVP | S15 |
| Download original CV | As a recruiter, I want to download the candidate's original uploaded CV for reference | 🔴 MVP | S15 |
| Download formatted CV | As a recruiter, I want to download the AI-formatted Word resume so I can share it with clients | 🔴 MVP | S15 |
| Schedule interview | As a recruiter, I want to initiate interview scheduling directly from the candidate profile | 🟠 V1.1 | S15 |
| Add notes to a candidate | As a recruiter, I want to add private notes to a candidate so my observations are recorded | 🟠 V1.1 | S15 |
| Send candidate to client | As a recruiter, I want to share a candidate profile link with a client so they can review it | 🟡 V2.0 | — |

---

### A8 · Search & Discover Candidates

| Task | User Story | Release | Screen |
|---|---|---|---|
| Full-text search candidates | As a recruiter, I want to search by name, skill, or job title across all candidates in my database | 🔴 MVP | S16 |
| Semantic / AI search | As a recruiter, I want to search using natural language ("senior DevOps with AWS 5yr") so I find nuanced matches | 🟠 V1.1 | S16 |
| Filter by tier, sector, score | As a recruiter, I want to filter search results by employer tier, sector, and minimum score | 🔴 MVP | S16 |
| View candidate from search | As a recruiter, I want to open the candidate profile from search results without losing my search | 🔴 MVP | S16 |

---

### A9 · Import Candidates in Bulk

| Task | User Story | Release | Screen |
|---|---|---|---|
| Upload multiple CVs at once | As a recruiter, I want to upload a ZIP or batch of CVs so I can onboard historical candidates quickly | 🔴 MVP | S17 |
| Monitor import progress | As a recruiter, I want to see real-time parsing progress so I know the batch is running | 🔴 MVP | S17 |
| View import errors | As a recruiter, I want to see which files failed to parse so I can resubmit or fix them | 🔴 MVP | S17 |

---

### A10 · Monitor Dashboard & Insights

| Task | User Story | Release | Screen |
|---|---|---|---|
| View headline KPIs | As a recruiter, I want to see active jobs, new applications, and shortlisted counts at a glance | 🔴 MVP | S9 |
| See recent applications | As a recruiter, I want to see the latest applicants on my dashboard so I don't miss new CVs | 🔴 MVP | S9 |
| View score distribution | As a recruiter, I want to see how candidates score across bands so I understand the talent pool quality | 🔴 MVP | S9 |
| Get AI-generated hiring insights | As a recruiter, I want the AI to surface patterns (e.g. "DevOps candidates score 22% higher with K8s") | 🟠 V1.1 | S18 |
| View full reports | As a recruiter, I want to see a funnel report (Applied→Hired) so I can optimise my process | 🟠 V1.1 | S18 |
| Receive notifications | As a recruiter, I want to be notified when new applications arrive or scoring completes so I respond quickly | 🔴 MVP | S19 |
| Mark notifications as read | As a recruiter, I want to clear my notification feed so I see only unread items | 🔴 MVP | S19 |

---

## USER 3 — AGENCY ADMIN

### A11 · Onboard the Agency

| Task | User Story | Release | Screen |
|---|---|---|---|
| Sign up for an account | As an agency admin, I want to create a HireAI account with my work email so I can start the trial | 🔴 MVP | S2 |
| Verify email | As an agency admin, I want to verify my email so my account is secure | 🔴 MVP | S3 |
| Enter agency details | As an agency admin, I want to set my agency name, logo, and industry during onboarding | 🔴 MVP | S8 |
| Invite first team members | As an agency admin, I want to invite recruiters to my workspace during setup | 🔴 MVP | S8 |
| Upload employer tier DB | As an agency admin, I want to upload my tier Excel during onboarding so scoring works from day one | 🔴 MVP | S8 |
| See empty dashboard with guidance | As an agency admin, I want to see a helpful empty state on first login so I know what to do next | 🔴 MVP | S29 |

---

### A12 · Manage the Team

| Task | User Story | Release | Screen |
|---|---|---|---|
| View all team members | As an agency admin, I want to see all users and their roles so I understand who has access | 🔴 MVP | S21 |
| Invite a new recruiter | As an agency admin, I want to invite a recruiter by email so they can join my workspace | 🔴 MVP | S21 |
| Change member role | As an agency admin, I want to change a recruiter to admin so I can delegate management | 🔴 MVP | S21 |
| Suspend a member | As an agency admin, I want to suspend a user without deleting them so I preserve their activity history | 🟠 V1.1 | S21 |
| Remove a member | As an agency admin, I want to remove a user from the workspace so they lose access immediately | 🔴 MVP | S21 |
| See seat usage vs plan limit | As an agency admin, I want to see how many seats I've used so I know when to upgrade | 🔴 MVP | S21 |

---

### A13 · Configure AI Scoring

| Task | User Story | Release | Screen |
|---|---|---|---|
| Set default scoring weights | As an agency admin, I want to configure the default signal weights for my agency so all jobs start with my preferred scoring | 🔴 MVP | S22 |
| Enable/disable negative signals | As an agency admin, I want to toggle gap and sector mismatch penalties so scoring reflects our priorities | 🔴 MVP | S22 |
| Reset to default weights | As an agency admin, I want to reset to HireAI defaults if my custom config isn't working | 🟠 V1.1 | S22 |

---

### A14 · Manage Employer Tier Database

| Task | User Story | Release | Screen |
|---|---|---|---|
| View current tier DB status | As an agency admin, I want to see when the tier DB was last synced and how many employers are loaded | 🔴 MVP | S23 |
| Upload a new tier Excel | As an agency admin, I want to upload a new employer tier file to keep scores accurate | 🔴 MVP | S23 |
| Preview uploaded data | As an agency admin, I want to preview the first rows after upload to confirm the file is correct | 🔴 MVP | S23 |
| Download current tier file | As an agency admin, I want to download the active Excel file for reference or editing | 🟠 V1.1 | S23 |
| See auto-sync schedule | As an agency admin, I want to see when n8n last synced the tier DB so I know if it's stale | 🔴 MVP | S23 |

---

### A15 · Configure Branding

| Task | User Story | Release | Screen |
|---|---|---|---|
| Upload agency logo | As an agency admin, I want to add my agency logo so the candidate application form is branded | 🔴 MVP | S25 |
| Set primary brand colour | As an agency admin, I want to customise the button colour so the form matches our identity | 🟠 V1.1 | S25 |
| Preview branded form live | As an agency admin, I want to see a live preview of how candidates will see our branded form | 🟠 V1.1 | S25 |
| Set up custom domain | As an agency admin, I want candidates to apply via apply.ouragency.com instead of hireai.io | 🟡 V2.0 | S25 |
| Hide HireAI branding | As an agency admin, I want to remove HireAI attribution so the platform feels fully ours | 🟠 V1.1 | S25 |

---

### A16 · Manage Billing & Subscription

| Task | User Story | Release | Screen |
|---|---|---|---|
| View current plan | As an agency admin, I want to see my plan name, cost, and renewal date so I can plan budgets | 🔴 MVP | S24 |
| See quota usage | As an agency admin, I want to see CV usage and seat usage vs quota so I know when to upgrade | 🔴 MVP | S24 |
| Upgrade plan | As an agency admin, I want to upgrade my subscription so I get more CV quota and seats | 🔴 MVP | S24 |
| Update payment method | As an agency admin, I want to update my card details so billing continues without interruption | 🔴 MVP | S24 |
| Download invoices | As an agency admin, I want to download PDF invoices so I can submit them for expense reporting | 🟠 V1.1 | S24 |
| Cancel plan | As an agency admin, I want to cancel my subscription so I stop being billed | 🔴 MVP | S24 |

---

### A17 · General Agency Settings

| Task | User Story | Release | Screen |
|---|---|---|---|
| Update agency profile | As an agency admin, I want to edit my agency name, logo, and timezone so our profile stays current | 🔴 MVP | S20 |
| Set notification preferences | As an agency admin, I want to configure which events trigger email notifications so I'm not overwhelmed | 🟠 V1.1 | S20 |
| Delete agency account | As an agency admin, I want to delete the account if we're no longer using the platform | 🟡 V2.0 | S20 |

---

## USER 4 — SUPER ADMIN (Platform Owner)

### A18 · Monitor Platform Health

| Task | User Story | Release | Screen |
|---|---|---|---|
| View total agencies & MRR | As a super admin, I want to see total tenant count, active subscriptions, and MRR so I track business health | 🔴 MVP | S27 |
| View resumes parsed this month | As a super admin, I want to track platform-wide CV volume so I monitor infrastructure load | 🔴 MVP | S27 |
| See platform uptime | As a super admin, I want to see uptime % so I know if there are reliability issues | 🟠 V1.1 | S27 |

---

### A19 · Manage Tenants

| Task | User Story | Release | Screen |
|---|---|---|---|
| View all agencies | As a super admin, I want to see all agencies with their plan, usage, and status in a table | 🔴 MVP | S27 |
| Search / filter tenants | As a super admin, I want to search by agency name and filter by plan/status so I find tenants fast | 🔴 MVP | S27 |
| View tenant detail | As a super admin, I want to drilldown into a single agency to see their usage, team, and billing | 🔴 MVP | S28 |
| Impersonate an agency admin | As a super admin, I want to log in as an agency admin for support without knowing their password | 🔴 MVP | S28 |
| Suspend a tenant | As a super admin, I want to suspend an agency account if they violate terms | 🔴 MVP | S27 |
| Upgrade a tenant's plan | As a super admin, I want to manually change an agency's plan for sales or support reasons | 🟠 V1.1 | S28 |
| See quota warning alerts | As a super admin, I want to be alerted when agencies approach their quota so I proactively reach out | 🔴 MVP | S27 |
| Write internal support notes | As a super admin, I want to record notes about an agency for my team's context | 🟠 V1.1 | S28 |

---

## USER 2 — RECRUITER (continued from A10)

### A20 · AI Candidate Outreach (TO-DO #4)

| Task | User Story | Release | Priority | Screen |
|---|---|---|---|---|
| Generate outreach email | As a recruiter, I want the AI to draft a personalised outreach email per shortlisted candidate so I save hours of writing | 🟠 V1.1 | Medium | S15 |
| Review and edit draft | As a recruiter, I want to review and edit the AI draft before sending so I maintain quality | 🟠 V1.1 | Medium | S15 |
| One-click send | As a recruiter, I want to send the approved email in one click so outreach is instant | 🟠 V1.1 | Medium | S15 |

---

### A21 · Skill Taxonomy & Deduplication (TO-DO #5, #6)

> **Priority: High — required in MVP parser pipeline**

| Task | User Story | Release | Priority | Screen |
|---|---|---|---|---|
| Auto-normalise skills | As a recruiter, I want raw skill strings normalised ("JS" → "JavaScript") so search and scoring are consistent | 🔴 MVP | **High** | — (backend) |
| Detect duplicate candidates | As a recruiter, I want the system to flag a duplicate before creating a new candidate record so my database stays clean | 🔴 MVP | **High** | S6, S17 |
| Review duplicate match | As a recruiter, I want to see the suspected duplicate profile side-by-side so I can decide to merge or keep | 🔴 MVP | **High** | S6, S17 |
| Merge duplicate records | As a recruiter, I want to merge two duplicate candidate profiles into one so I don't lose data | 🟠 V1.1 | High | S16 |

---

### A22 · Candidate Freshness & Re-engagement (TO-DO #7, #10)

| Task | User Story | Release | Priority | Screen |
|---|---|---|---|---|
| Surface freshness signal | As a recruiter, I want to see a "freshness" indicator on candidates who recently changed jobs so I target warm leads first | 🟠 V1.1 | Medium | S13, S16 |
| Receive re-engagement alert | As a recruiter, I want to be alerted when a previously rejected candidate's score improves so I reconsider them automatically | 🟠 V1.1 | Medium | S19 |
| View score delta | As a recruiter, I want to see what changed in a candidate's profile to trigger the alert so I understand the improvement | 🟠 V1.1 | Medium | S15 |

---

### A23 · AI Score Calibration (TO-DO #3)

| Task | User Story | Release | Priority | Screen |
|---|---|---|---|---|
| Mark outcome (hired/rejected) | As a recruiter, I want to record the final outcome for applications so the system can learn from hiring decisions | 🟡 V2.0 | Medium | S15 |
| View auto-tuned weights | As a recruiter, I want to see how the AI has adjusted scoring weights based on past outcomes so I trust the calibration | 🔵 V3.0 | Medium (post-MVP) | S22 |

---

### A24 · Job Ad A/B Testing (TO-DO #8)

| Task | User Story | Release | Priority | Screen |
|---|---|---|---|---|
| Generate two ad variants | As a recruiter, I want the AI to produce two tone variants (professional / casual) so I can test which converts better | 🟡 V2.0 | Low | S12 |
| View variant performance | As a recruiter, I want to see application counts per variant so I know which ad works | 🟡 V2.0 | Low | S12, S18 |
| Set winner as default | As a recruiter, I want to publish the winning variant as the active ad so performance improves over time | 🟡 V2.0 | Low | S12 |

---

### A25 · Multilingual Parsing & Job Board Integration (TO-DO #9, #12)

| Task | User Story | Release | Priority | Screen |
|---|---|---|---|---|
| Parse Vietnamese resume | As a recruiter, I want to upload a Vietnamese-language CV and receive structured data so I can serve the Vietnam market | 🟡 V2.0 | Medium (roadmap) | S17 |
| Push job ad to ITViec | As a recruiter, I want to publish a job to ITViec directly from the platform so I don't have to re-post manually | 🟡 V2.0 | Medium (roadmap) | S10, S12 |
| Push job ad to LinkedIn | As a recruiter, I want to publish a job to LinkedIn Jobs so I reach a wider candidate pool | 🔵 V3.0 | Medium (roadmap) | S10, S12 |
| Pull external applications | As a recruiter, I want external applications imported automatically so I manage all candidates in one place | 🟡 V2.0 | Medium (roadmap) | S13 |

---

## Priority Summary (derived from TO-DO.md)

| Priority | Items | Release target |
|---|---|---|
| 🔴 High — MVP required | Skill taxonomy normalisation (A21) · Duplicate detection (A21) · Bulk import (A9) | 🔴 MVP |
| 🟠 High — Early post-MVP | Semantic search (A8) · Freshness score (A22) · Re-engagement alerts (A22) · Outreach drafts (A20) | 🟠 V1.1 |
| 🟡 Medium — Planned | Score calibration (A23) · Multilingual parsing (A25) · Job board push (A25) | 🟡 V2.0 |
| 🔵 Low / Future | AI A/B testing (A24) · LinkedIn Jobs (A25) · Weight auto-tuning (A23) | 🔵 V3.0 |

---

## Story Count by Release

| Release | Stories | Screens involved |
|---|---|---|
| 🔴 MVP | 58 stories (+3 from TO-DO #5, #6) | 25 screens |
| 🟠 V1.1 | 30 stories (+9 from TO-DO #4, #7, #10) | 17 screens |
| 🟡 V2.0 | 12 stories (+7 from TO-DO #8, #9, #12) | 6 screens |
| 🔵 V3.0 | 3 stories (TO-DO #3 calibration, #12 LinkedIn) | 2 screens |
| **Total** | **103 stories** | **30 screens** |

---

## Screen → Story Mapping

Use this to verify every screen has a backing user story before designing it in Stitch.

| Screen | Stories backing it |
|---|---|
| S1 Login | A3: Log in |
| S2 Sign Up | A11: Sign up |
| S3 Forgot PW | A3: Reset password, A11: Verify email |
| S4 Job Board | A1: Browse, search, filter jobs |
| S5 Job Detail (public) | A1: View job detail, Save job |
| S6 Application Form | A2: Fill details, LinkedIn URL, Upload CV, Cover note |
| S7 Confirmation | A2: Receive confirmation |
| S8 Onboarding Wizard | A11: Enter agency details, Invite team, Upload tier DB |
| S9 Dashboard | A10: View KPIs, recent applications, score distribution |
| S10 Jobs List | A4: View all, publish, close, duplicate jobs |
| S11 Create/Edit Job | A4: Create, edit, customise stages |
| S12 Job Ad Generator | A5: Generate, preview, edit, approve ad |
| S13 Job Detail + App List | A6: View scores, filter, shortlist, reject, override weights |
| S14 Kanban Pipeline | A7: View pipeline, move candidate to stage |
| S15 Candidate Profile Panel | A6: View breakdown & summary, A7: Download CVs, add notes |
| S16 Candidate Search | A8: Search, semantic search, filter |
| S17 Bulk Import | A9: Upload batch, monitor progress, view errors |
| S18 Reports | A10: Funnel report, AI insights |
| S19 Notifications | A10: Receive & clear notifications |
| S20 Settings General | A17: Update agency profile, notifications |
| S21 Settings Team | A12: View, invite, manage, remove members |
| S22 Settings Scoring | A13: Set weights, toggle signals |
| S23 Settings Tier DB | A14: View status, upload, preview, auto-sync |
| S24 Settings Billing | A16: View plan, quota, upgrade, invoices, cancel |
| S25 Settings Branding | A15: Logo, colour, custom domain, hide branding |
| S26 Workspace Switcher | A3: Switch agency |
| S27 Super Admin Overview | A18: Platform KPIs, A19: Tenant table, alerts |
| S28 Super Admin Detail | A19: Tenant detail, impersonate, notes |
| S29 Empty State Dashboard | A11: First login guidance |
| S30 Landing Page | — (Marketing, no user story) |

### New screens from TO-DO backlog

| Screen | Stories backing it |
|---|---|
| S15 (extended) | A20: Outreach draft, review, send · A22: Score delta · A23: Mark outcome |
| S6, S17 (extended) | A21: Duplicate flag + side-by-side review |
| S13, S16 (extended) | A21: Merge duplicates · A22: Freshness indicator |
| S19 (extended) | A22: Re-engagement alert |
| S12 (extended) | A24: A/B variants, set winner |
| S18 (extended) | A24: Variant performance |
| S22 (extended) | A23: Auto-tuned weights |
| S10, S12 (extended) | A25: Push to ITViec / LinkedIn |
