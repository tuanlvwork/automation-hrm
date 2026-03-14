# STITCH-DESIGN.md — AI Recruitment Platform (Full Screen Inventory)

> **Tool:** Google Stitch (stitch.withgoogle.com)
> **Workflow:** Copy each prompt block directly into Stitch to generate the screen.
> **Rule:** Always paste the Global Design System from §0 into every prompt.

---

## Screen Index

| # | Screen | Flow | Priority |
|---|---|---|---|
| **AUTH** | | | |
| 1 | Login Page | Auth | 🔴 |
| 2 | Sign Up — Create Agency Account | Auth | 🔴 |
| 3 | Forgot Password + Email Verification | Auth | 🟠 |
| **PUBLIC / CANDIDATE** | | | |
| 4 | Public Job Board (Candidate job listing) | Candidate | 🔴 |
| 5 | Public Job Detail (pre-apply) | Candidate | 🔴 |
| 6 | Candidate Application Form (3-step) | Candidate | 🔴 |
| 7 | Application Confirmation / Thank You | Candidate | 🟠 |
| **ONBOARDING** | | | |
| 8 | Agency Onboarding Wizard (post-signup) | Onboarding | 🔴 |
| **RECRUITER — CORE** | | | |
| 9 | Recruiter Dashboard (Home) | Recruiter | 🔴 |
| 10 | Jobs List & Management | Recruiter | 🔴 |
| 11 | Create / Edit Job Form | Recruiter | 🔴 |
| 12 | AI Job Ad Generator | Recruiter | 🔴 |
| 13 | Job Detail + Application List (scored) | Recruiter | 🔴 |
| 14 | Application Pipeline — Kanban Board | Recruiter | 🔴 |
| 15 | Candidate Profile Side Panel | Recruiter | 🔴 |
| 16 | Candidate Intelligence Search | Recruiter | 🟠 |
| 17 | Bulk Resume Import | Recruiter | 🟠 |
| 18 | Reports & Analytics | Recruiter | 🟠 |
| 19 | Notification Center | Recruiter | 🟠 |
| **SETTINGS** | | | |
| 20 | Settings — General | Settings | 🟠 |
| 21 | Settings — Team & Users | Settings | 🟠 |
| 22 | Settings — Scoring Weights | Settings | 🟠 |
| 23 | Settings — Employer Tier Database | Settings | 🟠 |
| 24 | Settings — Billing & Subscription | Settings | 🟠 |
| 25 | Settings — Agency Branding | Settings | 🟠 |
| **MULTI-AGENCY** | | | |
| 26 | Agency / Workspace Switcher | Multi-agency | 🟠 |
| **SUPER ADMIN** | | | |
| 27 | Super Admin — Tenant Overview | Super Admin | 🟡 |
| 28 | Super Admin — Tenant Detail Drilldown | Super Admin | 🟡 |
| **UTILITY** | | | |
| 29 | Empty State Dashboard (first login) | Utility | 🟠 |
| 30 | Landing Page (public marketing) | Public | 🔴 |

**Total: 30 screens**

---

## 0. Global Design System (paste into every prompt)

```
DESIGN SYSTEM (REQUIRED):
- Platform: Web, Desktop-first (1440px), responsive to 375px mobile
- Theme: Light with glass-accent elements
- Background: Soft Slate (#f8fafc)
- Surface / Card: White (#ffffff), shadow: 0 2px 8px rgba(0,0,0,0.06)
- Primary Accent: Indigo (#4f46e5) — buttons, active states, links
- Secondary Accent: Violet (#7c3aed) — gradient highlights
- Success: Emerald (#10b981)
- Warning: Amber (#f59e0b)
- Danger: Rose (#f43f5e)
- Text Primary: Slate-900 (#0f172a)
- Text Secondary: Slate-500 (#64748b)
- Border: Slate-200 (#e2e8f0)
- Typography: Inter — 32px H1, 24px H2, 18px H3, 14px body
- Buttons: Rounded-lg (8px), icon + label
- Cards: Rounded-xl (12px), hover lift shadow
- Sidebar: 240px fixed, white, border-right
- Tone: Professional SaaS — inspired by Linear and Notion
```

---

## ─── AUTH FLOW ───────────────────────────────────────

## Screen 1 — Login Page

```
Login page for HireAI, an AI-powered recruitment SaaS for IT agencies.
Clean, centred, trustworthy.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Split screen. Left half: indigo-to-violet gradient with product
tagline "Hire Smarter. Powered by AI." and 3 micro-feature bullets with
checkmarks. Right half: white login card, vertically centred.

Login Card:
1. HireAI logo + "Welcome back" heading (H2)
2. Social login buttons: "Continue with Google" (full-width, outlined)
3. Divider: "or continue with email"
4. Email input field
5. Password input field + "Show/hide" eye icon
6. "Forgot password?" link (right-aligned, small)
7. "Sign In" primary button (indigo, full-width)
8. Footer: "Don't have an account? Start free trial" link

Visual Style: Right panel pure white. Input fields slate-50 bg.
Indigo button with subtle gradient. Left panel has abstract geometric
mesh pattern at 10% opacity over the gradient.
Platform: Responsive web, desktop-first.
```

---

## Screen 2 — Sign Up — Create Agency Account

```
Sign-up page for a new recruitment agency creating a HireAI account.
Simple, fast, low-friction.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same split as Login. Left: gradient panel with social proof
"Join 500+ IT recruitment teams". Right: sign-up card.

Sign Up Card:
1. HireAI logo + "Start your free trial" heading
2. "Continue with Google" (full-width, outlined)
3. Divider: "or sign up with work email"
4. Full name (text input)
5. Work email (text input)
6. Agency name (text input)
7. Password (text input, strength indicator bar below)
8. "Create Account" button (indigo, full-width)
9. Fine print: "By signing up you agree to our Terms and Privacy Policy."
10. "Already have an account? Sign in" link

Visual Style: Same as login. Password strength bar fills from rose →
amber → emerald as password gets stronger.
Platform: Responsive web.
```

---

## Screen 3 — Forgot Password + Email Verification

```
Two-state page: Forgot password form → and email verification/OTP state.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Centred card, max-width 440px, on slate-50 background.
HireAI logo at top.

State A — Forgot Password:
1. "Reset your password" heading + "Enter your email and we'll send a
   reset link." subtext.
2. Email input field.
3. "Send Reset Link" button (indigo, full-width).
4. "Back to login" link below.

State B — Check Your Email (shown after submit):
1. Large envelope icon with indigo glow (illustration).
2. "Check your inbox" heading.
3. "We sent a password reset link to user@agency.com"
4. "Resend email" link (with 60-second cooldown timer).
5. "Back to login" link.

State C — Email Verification (new user):
Same layout as State B but copy reads:
"Verify your email to activate your HireAI account."
Emerald checkmark animation once link is clicked.

Visual Style: Clean, minimal, focused. States transition smoothly.
Success state shows emerald animated checkmark circle.
Platform: Responsive web, mobile-friendly.
```

---

## ─── PUBLIC / CANDIDATE FLOW ────────────────────────

## Screen 4 — Public Job Board

```
Public-facing job listing page where candidates browse open IT jobs
posted by a recruitment agency using HireAI. Agency-branded header.

DESIGN SYSTEM (REQUIRED): [paste §0]

Header: Agency logo left, agency name, "View all jobs" nav link.
No HireAI branding visible (white-labelled).

Hero Section: Agency-branded banner. Headline: "IT Careers at [Agency Name]"
Large search bar: "Search job title, skills, or keyword" + Location dropdown
+ "Search" button.

Filters Sidebar (left, 220px):
- Job Type (Full-time, Contract, Remote)
- Seniority (Junior, Mid, Senior, Lead)
- Tech Stack (React, Python, DevOps, Java...)
- Salary Range (slider)
- Posted within (7 days, 30 days, All time)
- "Clear filters" link

Job Cards Grid (right, 2-column):
Each card:
- Job title (H3, bold)
- Agency / Company name
- Location + Remote badge
- Salary range
- Required skills (3 pills)
- Posted date (relative: "3 days ago")
- "Apply Now" button (indigo, outline)
Pagination at bottom.

Visual Style: Clean job board. Hovering a card lifts it slightly.
Remote badge: emerald. Posted date in slate-500.
Platform: Responsive web, mobile-first.
```

---

## Screen 5 — Public Job Detail Page (Pre-Apply)

```
Public job detail page. Candidate reads the AI-generated job ad and
decides to apply. Agency-branded, no HireAI branding shown.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Two-column. Left (wide): job ad content. Right (narrow): sticky
apply sidebar.

Left Column:
1. Breadcrumb: "Jobs / Senior Backend Engineer"
2. Job title (H1), company logo + name, location, salary range, job type.
3. Posted date + "47 applicants" indicator.
4. Full AI-generated job ad (formatted markdown):
   - About the Role section
   - Key Responsibilities (bulleted)
   - Requirements (bulleted)
   - Nice to Have (bulleted)
   - What We Offer section
5. Required Skills section: chip grid of skills.
6. "Share this job": copy link + LinkedIn + Twitter icon buttons.

Right Sticky Sidebar (300px):
- Company card: logo, name, industry, size, "View all jobs" link.
- "Apply for this role" CTA card:
  - "Apply Now" button (indigo, full-width, large)
  - "Save Job" button (outline, bookmark icon)
  - Deadline date if set

Visual Style: Generous reading typography. Right sidebar has shadow card.
Skill chips in slate outlined style. CTA button large and prominent.
Platform: Responsive web, desktop-first.
```

---

## Screen 6 — Candidate Application Form (3-Step)

```
Job application form for a candidate. Agency-branded header. Multi-step
wizard. Clean, minimal, low-friction.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Centred card (max 640px). Agency logo + job title at top.
3-step progress bar (indigo filled, grey remaining).

Step 1 — Personal Details:
- Full name
- Email address (with validation)
- Phone number
- LinkedIn Profile URL (required — red asterisk + tooltip
  "We use your LinkedIn to verify your career history")
- "Next →" button (indigo)

Step 2 — Resume Upload:
- Large drag-and-drop upload zone (dashed indigo border on hover):
  "Drop your CV here or click to browse"
  "PDF or Word · Max 5MB"
  File selected state: filename + size + green tick + "Remove" link
- Optional cover note (textarea, 4 rows)
- "← Back" (outline) and "Submit Application →" (indigo) buttons.

Step 3 — Application Received:
- Large animated emerald checkmark circle.
- "You're in! Application Submitted." heading (H2).
- "We'll review your application and be in touch within 5 business days."
- "Browse more jobs" button (outline) + "Back to [Agency] website" link.

Visual Style: Distraction-free. Mobile-first. Progress bar fills indigo.
Error states: rose border + error message. Upload zone scales well on mobile.
Platform: Responsive web, mobile-first.
```

---

## Screen 7 — Application Confirmation / Thank You

```
Standalone thank-you page shown after application is submitted.
Also used for email link verification ("Your application is confirmed").

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Full-screen centred, slate-50 background.

Content:
1. Agency logo at top.
2. Large animated emerald checkmark (illustrated, with glow ring).
3. "Application Received!" heading (H1).
4. Candidate name personalisation: "Thanks, [Name]!"
5. "We've received your application for Senior Backend Engineer at
   [Agency Name]. Our team will be in touch within 5 business days."
6. What happens next — 3-step timeline:
   - "Application Under Review" (current, indigo)
   - "Phone Screen" (upcoming, slate)
   - "Interview" (upcoming, slate)
7. Two buttons: "Browse More Jobs" (outline) and "Visit Agency Website" (link).

Visual Style: Clean, celebratory but professional. Emerald animation.
Timeline uses indigo/slate dots connected by vertical line.
Platform: Responsive web, mobile-friendly.
```

---

## ─── ONBOARDING FLOW ─────────────────────────────────

## Screen 8 — Agency Onboarding Wizard (Post-Signup)

```
Full-screen 4-step guided setup wizard for a new agency after they sign up.
No sidebar. Entire viewport is the wizard.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Left panel (280px) with vertical step progress list. Right panel:
step content (max-width 560px, centred within the right side).

Left step list:
1. Agency Details
2. Invite Your Team
3. Employer Tier Database
4. You're Ready!
Each step: number circle (filled indigo = done, outline = current, grey = future)
+ step label.

Step 1 — Agency Details:
- Agency name (large input)
- Industry (select: IT Services / IT Staffing / HR Consultancy / Other)
- Country (select)
- Agency logo upload (drag-and-drop circle preview, 120px)
- "Continue" (indigo, full-width)

Step 2 — Invite Your Team:
- "Add your recruiters" heading.
- Repeating row: email input + "Admin / Recruiter" role select + "Add" button.
- Added invites list (avatar initials, name, role tag, remove ×).
- "Skip for now" link
- "Continue" button.

Step 3 — Employer Tier Database:
- Heading: "Upload your employer tier database"
- Sub: "This lets our AI score candidates by company prestige."
- Drag-and-drop Excel upload zone.
- "Download sample template" link.
- "Use HireAI default database" checkbox for agencies without their own.
- "Continue" button.

Step 4 — Ready!:
- Large animated indigo star/sparkle illustration.
- "HireAI is set up for [Agency Name]!" heading.
- 3 quick-start action cards in a row:
  "Post Your First Job" · "Import Candidate CVs" · "Configure Scoring"
  Each with icon + outline button.
- "Go to Dashboard →" (indigo, full-width).

Visual Style: Clean wizard. Left panel slate-50. Right panel white.
Completed step circles have checkmark. Smooth step transitions.
Platform: Responsive web, desktop-first.
```

---

## ─── RECRUITER — CORE FLOW ───────────────────────────

## Screen 9 — Recruiter Dashboard (Home)

```
Main home screen for a recruiter after login. Shows pipeline summary,
recent activity, and AI insights.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout:
- Left sidebar (240px): HireAI logo + agency name dropdown (chevron →
  opens workspace switcher). Nav: Dashboard, Jobs, Applications,
  Candidates, Reports, Settings. User avatar + name at bottom.
- Top bar: "Dashboard" title, date, search icon, notification bell
  (with badge count), user avatar.
- Main: 2-column (wide left, narrow right).

Main Content:
1. Stats Row — 4 metric cards:
   Active Jobs · New Applications Today · Candidates Scored · Shortlisted
   Each: large number, label, trend arrow (↑ +12% vs last week).

2. Active Jobs Table (left):
   Columns: Title, Department, # Applications, Top Score, Status (badge),
   Actions. 5 rows. "View all jobs →" link.

3. Recent Applications Feed (right):
   6 latest applicants. Each row: initials avatar, name, job title applied,
   AI score badge (green/amber/rose by range), timestamp, "Review" button.

4. Score Distribution Chart (left, below table):
   Horizontal bar chart: score bands 0-20 / 21-40 / 41-60 / 61-80 / 81-100.
   Indigo bars. Title: "Candidate Score Distribution — All Active Jobs"

Visual Style: Cards with subtle shadow. Indigo active nav highlight.
Score badge: ≥70 emerald, 40-69 amber, <40 rose.
Platform: Web, desktop-first.
```

---

## Screen 10 — Jobs List & Management

```
Full list of all jobs for this agency with search, filters, and bulk actions.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Full-width content.

Top Bar: "Jobs" heading (H1). Tabs: All · Active · Draft · Closed.
Right side: "Import Jobs" (outline) + "Post New Job" (indigo) buttons.

Controls Row: Search input, "Filter" dropdown (Department, Location,
Status), "Sort" selector (Newest / Most Applications / Highest Score).
Count: "34 jobs total"

Jobs Table:
Columns: Job Title, Department, Location (+ remote badge), Applications (#),
Top Score, Status (badge: Active / Draft / Closed / Paused),
Created date, Actions (Edit, View Ad, Close, ···).
Row click → opens Job Detail (Screen 13).

Status badges: Active = emerald, Draft = amber, Closed = slate,
Paused = rose.

Empty state (0 jobs): Illustration + "No jobs posted yet."
+ "Post your first job" button.

Visual Style: Standard table, hover row highlight. Status badges pill-shaped.
Bulk select checkboxes on left of each row when hovering.
Platform: Web, desktop-first.
```

---

## Screen 11 — Create / Edit Job Form

```
Full-page form for a recruiter to create or edit a job posting.
Two modes: Create (blank) and Edit (pre-filled).

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Centred form, max-width 720px. Two-column inputs
where space allows. Sticky "Save Draft" + "Publish" buttons at bottom.

Form Sections (vertical):

1. Basic Info:
   - Job title (large text input)
   - Department (select)
   - Employment type (select: Full-time / Part-time / Contract / Internship)
   - Location (text + "Remote" toggle switch)

2. Compensation:
   - Salary min + max (side-by-side inputs) + currency selector
   - "Hide salary from candidates" checkbox

3. Job Description:
   - Rich text editor (toolbar: bold, italic, bullet list, heading)
   - Character count below

4. Requirements:
   - Required skills (tag input — type + enter to add pill)
   - Nice-to-have skills (tag input)
   - Years of experience (number input)
   - Education level (select)

5. Scoring Overrides (collapsible panel, "Advanced"):
   - "Override tenant scoring weights for this job?" toggle
   - If on: same 5 sliders as Settings screen

6. Pipeline Stages:
   - Drag-and-drop list of stages for this job. Default 6 stages pre-filled.
   - "Add stage" + "Remove" per row.

Bottom Sticky Bar: "Save as Draft" (outline) + "Publish Job" (indigo).
Autosave indicator: "Autosaved 2 min ago" (small, slate-500).

Visual Style: Sectioned form with H3 section headers and dividers.
Rich text editor has light border. Tag pills remove on ×.
Platform: Web, desktop-first.
```

---

## Screen 12 — AI Job Ad Generator

```
Job ad creation screen. Recruiter fills job details, AI generates the ad,
recruiter reviews and approves. Split-panel layout.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Two columns (form left 45%, preview right 55%).

Left — Job Details Form:
1. Job title
2. Department (select)
3. Location + Remote toggle
4. Salary range (min-max)
5. Key responsibilities (textarea, 5 rows)
6. Required skills (tag input)
7. Nice-to-have skills (tag input)
8. "✨ Generate Job Ad" button (indigo, full-width, sparkle icon)

Right — Ad Preview Panel:
- Empty state: illustration + "Fill in job details and click Generate."
- Generating state: indigo spinner + "Generating your job ad..." banner.
- Generated state: white card with ad text, formatted:
  About the Role / Responsibilities / Requirements / What We Offer.
  Word count. Tone selector: "Professional / Casual / Enthusiastic".
  "✓ Approve & Publish" (emerald). "↺ Regenerate" (outline).
  "✎ Edit Manually" toggle (enables inline editing).

Visual Style: Left: slate-50 bg. Right: white with indigo left-border.
Sparkle icon animates on hover. Panel divider is draggable.
Platform: Web, desktop-first.
```

---

## Screen 13 — Job Detail + Application List

```
Job detail screen inside the recruiter dashboard showing all candidates
who applied to a specific job, sorted by AI suitability score.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Full content area.

Top: Breadcrumb "Jobs / Senior Backend Engineer". Status badge (Active).
"Edit Job" + "View Job Ad" + "Switch to Kanban" buttons top right.

Job Summary Card: Title (H1), department, location, salary, posted date.
Description truncated (3 lines). "View full description" expand link.

Scoring Weights Panel (collapsible):
5 sliders (Keyword, Title, Tier, Sector, Tenure). "Recalculate Scores" button.

Controls Bar: Search candidates, filter (All / Shortlisted / Reviewed /
Rejected), sort (Score ↓, Date ↓), "Export CSV".
Count: "127 applications · 20 shortlisted"

Candidate Table:
Columns: Rank, Name + avatar, AI Score (badge circle), Job Title Match,
Top Skills (3 pills), Employer Tier (badge), Shortlist (star toggle),
Actions (View, Reject). Top 20 rows have gold star pre-filled.

Footer: Pagination.
Click any row → opens Candidate Profile Side Panel (Screen 15).

Visual Style: Shortlisted rows: indigo left-border accent. Score badge: 40px.
Table rows hover: slate-50.
Platform: Web, desktop-first.
```

---

## Screen 14 — Application Pipeline — Kanban Board

```
Kanban board view of all candidates across pipeline stages for a specific job.
Alternative view to the scored table. Recruiter drags cards between stages.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Horizontal scroll for stage columns.

Top: Same breadcrumb as Job Detail. "Switch to List View" toggle top right.

Kanban Columns (6, horizontal scroll):
Applied · Screened · Shortlisted · Interviewed · Offered · Hired
Each column header: stage name + candidate count badge.

Candidate Cards (inside each column):
- Candidate initials avatar (indigo circle)
- Candidate name (bold)
- AI Score badge (small, coloured pill)
- Current job title
- Top 2 skill chips
- "View →" small link
Drag handle on left edge of each card.

Stage column colours: Applied = slate, Screened = amber, Shortlisted = indigo,
Interviewed = violet, Offered = emerald, Hired = emerald-dark.

Empty column: dashed border, "Drop candidates here" placeholder.

Visual Style: Kanban columns fixed width (240px). Horizontal scroll.
Drag-in-progress: card lifts with shadow-xl, column highlights.
Platform: Web, desktop-first.
```

---

## Screen 15 — Candidate Profile Side Panel

```
Candidate detail slide-in panel from the right. Full height overlay.
Opens from Job Application List or Search results.

DESIGN SYSTEM (REQUIRED): [paste §0]

Panel: 480px width, slides from right, rest of page dimmed (backdrop-blur).

Panel Content:
1. Header Row:
   - Large initials avatar (64px, indigo circle gradients)
   - Full name (H2), current job title, current employer
   - LinkedIn icon (opens URL), Close ×
   - "↓ Original CV" + "↓ Formatted CV" icon buttons

2. AI Score Section:
   - Large circular score gauge (0-100, indigo arc, number centred)
   - Score breakdown table: 5 signals, each with label + % bar
   - AI Summary callout box (sparkle icon, slate-50 bg):
     "This candidate ranks in the top 15% for this role because..."

3. Contact Info:
   Email · Phone · LinkedIn URL · Applied date — each with small icon.

4. Employment History — Timeline:
   Vertical indigo line, each entry:
   - Company name + Tier badge (Tier 1–5, coloured pill)
   - Job title
   - Date range + tenure tag ("2y 3m")

5. Skills Section:
   Chip grid. JD-matching skills: indigo filled. Others: slate outlined.

6. Sticky Bottom Action Bar:
   "★ Shortlist" (indigo) · "📅 Schedule Interview" · "✕ Reject" (rose outline)
   "Move to stage →" dropdown

Visual Style: White panel. Slide-in with ease-out animation.
Timeline indigo line. Matching skills pop visually.
Platform: Web, desktop-first.
```

---

## Screen 16 — Candidate Intelligence Search

```
Full-page semantic candidate search with natural language + structured filters.
Searches across all candidates in the tenant's database.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Full-width content.

Hero Search Bar (large, top):
Giant search input (full width): "Search candidates by skills, role, experience..."
Magnifying glass icon left. Clear × right. Indigo border on focus.
Below input: suggestion chips — "Senior DevOps AWS" · "React Lead 5yr" · "Python ML"

Filters Row (below search):
Skill (multi-select) · Experience (slider 0-20yr) · Employer Tier (1-5 checkboxes)
Sector · Min Score · "Reset" link.

Results Grid (3-column card grid):
Each card:
- Initials avatar (circle, coloured by score tier)
- Name + current title + employer (with tier badge)
- 4 skill pills (matching skills indigo-filled)
- AI Score badge (large circle, coloured)
- "Avg tenure 2.3yr" tag
- "View Profile →" button

0 results: illustrated empty state + "No match. Try different keywords."
Loading: shimmer skeleton cards.

Visual Style: Search bar hero-sized, commands attention. Cards hover-lift.
Matching skills stand out visually.
Platform: Web, desktop-first.
```

---

## Screen 17 — Bulk Resume Import

```
Bulk upload screen for importing many CVs at once (agency onboarding or
batch processing). Supports ZIP upload or individual multi-file select.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Centred content (max 800px).

Page Header: "Bulk Resume Import" (H1). Subtext:
"Upload up to 500 CVs at once. AI will parse and score each candidate."

Upload Zone (large, prominent):
Dashed border box (full width, 220px tall):
"Drop CVs or a ZIP file here · PDF or Word · Max 500 files · 200MB total"
Upload icon + "Or click to browse" link.

File List (below zone, once files are selected):
Scrollable table. Columns: Filename, Size, Status (icon).
Status states: Queued (clock) / Parsing (indigo spinner) /
Parsed ✓ (emerald) / Error ✗ (rose, with hover tooltip showing reason).

Progress Panel (right sidebar within page):
- Total files: 127
- Parsed: 84 (emerald progress bar)
- Errors: 3 (rose)
- Queued: 40 (slate)
- "Pause" / "Resume" buttons
- ETA: "~4 min remaining"

Bottom Actions:
"Start Import" (indigo, full-width) before upload.
"View All Imported Candidates →" link after completion.

Visual Style: Progress panel has live updating numbers. Status icons
animate while parsing. Error rows rose-tinted.
Platform: Web, desktop-first.
```

---

## Screen 18 — Reports & Analytics

```
Analytics dashboard for a recruiter or agency admin. Shows hiring funnel,
top scoring candidates, job performance, and AI scoring accuracy metrics.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Full-width content. Date range picker top right.

Page Header: "Reports" (H1). Tabs: Overview · Jobs · Candidates · AI Insights

Active Tab: Overview

1. KPI Cards Row (5 cards):
   Total Applications · Average Score · Shortlist Rate · Time to Shortlist ·
   Resumes Parsed This Month.

2. Applications Over Time chart (line chart, 30 days):
   Indigo line. Hover tooltip shows daily count.

3. Hiring Funnel (horizontal funnel chart):
   Applied → Screened → Shortlisted → Interviewed → Offered → Hired
   With count and drop-off % at each stage.

4. Top Jobs by Score (table, left):
   Job title / Avg score / Top applicants / Status.

5. Score Distribution by Job (stacked bar chart, right):
   Shows how score spread differs per job.
   Helps recruiters see which jobs attract better-fit candidates.

6. AI Insights Panel (bottom, amber-tinted card):
   "Based on scoring patterns, candidates with Kubernetes skills score
   22% higher for your DevOps roles." — AI-generated observation.

Date range filter: Last 7d / 30d / 90d / Custom. "Export PDF" button.

Visual Style: Data-focused. Charts use Inter typography. Indigo as primary
chart colour. Amber AI insight callout stands out.
Platform: Web, desktop-first.
```

---

## Screen 19 — Notification Center

```
Full notification panel that opens when recruiter clicks the bell icon
in the top bar. Slide-in from right or dropdown panel under bell.

DESIGN SYSTEM (REQUIRED): [paste §0]

Panel: 360px wide, full browser height, slides from right.

Header: "Notifications" + "Mark all as read" link + close ×.
Tabs: All · Unread · Mentions.

Notification Items (vertical list):
Each item:
- Left: avatar initials or system icon (indigo/amber/emerald)
- Content: short bold title + description (1 line, truncated)
- Time: "2 min ago" (slate-500)
- Unread indicator: indigo dot on left edge
- Hover: slate-50 bg

Notification types (different icons/colours):
🔵 New application: "John Nguyen applied to Senior DevOps"
🟢 Scoring done: "AI scored 12 new candidates for React Lead"
🟡 Job ad ready: "Ad draft ready for your review — React Lead"
🔵 Career update: "Alice Tran changed jobs at VNG Corporation"
🔴 Quota warning: "You've used 85% of your monthly CV quota"

Empty state: bell illustration + "You're all caught up!"

Visual Style: Unread items have subtle indigo-left-border. Icons use
coloured circles matching notification type.
Platform: Web component (desktop + mobile).
```

---

## ─── SETTINGS FLOW ───────────────────────────────────

## Screen 20 — Settings — General

```
General settings page for an agency admin to manage company profile,
timezone, and notification preferences.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Settings sub-nav tabs at top:
General (active) | Scoring | Employer Tiers | Team | Billing | Branding

Left content column (max 680px).

Sections (each in a white card):

1. Agency Profile:
   - Agency logo (current + upload button)
   - Agency name (text input)
   - Industry (select)
   - Country / Timezone (select)
   - Website URL
   "Save" button.

2. Notification Preferences:
   Toggle switches for:
   - Email: New application received
   - Email: AI scoring complete
   - Email: Career update detected
   - Email: Weekly digest
   - In-app: All notifications / Mentions only / None
   "Save" button.

3. Danger Zone (red-bordered card):
   "Delete Agency Account" — outline rose button + confirmation warning text.

Visual Style: Each section in a separate white card with H3 heading.
Toggles use indigo when on. Danger zone card has rose border.
Platform: Web, desktop-first.
```

---

## Screen 21 — Settings — Team & Users

```
User management page for an agency admin to invite, manage roles,
and remove team members.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar + settings tabs. Content max 800px.

Top: "Team Members" heading + "Invite Member" button (indigo, top right).

Team Table:
Columns: Member (avatar + name + email), Role (Admin / Recruiter badge),
Status (Active / Invited / Suspended), Joined date, Actions (···menu).
Actions menu: Change Role / Suspend / Remove.

Invite Modal (triggered by button):
- Email input
- Role select (Admin / Recruiter)
- "Send Invite" button.
Pending invites shown in table as amber "Invited" badge.

Roles section (below table, card):
Role descriptions:
- Admin: Full access including settings, billing, all jobs.
- Recruiter: Access to assigned jobs and candidates only.

Seats usage bar:
"7 of 10 seats used" (indigo progress bar).
"Upgrade to add more members →" link if at limit.

Visual Style: Table with avatar column feels human and recognisable.
Amber pending badge. Seat usage bar visual.
Platform: Web, desktop-first.
```

---

## Screen 22 — Settings — Scoring Weights

```
Per-tenant default AI scoring configuration page.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar + settings tabs.

Page sections (each in white card):

1. "Default Scoring Weights" card:
   5 rows. Each: signal name, description (1 line, slate-500),
   horizontal slider (indigo thumb), live % display.
   Signals: Keyword Relevance / Job Title Match / Employer Tier /
   Sector Experience / Tenure Stability.
   Live "Total: 100%" — emerald if 100%, rose if not.
   Info tooltip: "These are defaults. You can override per job."

2. "Negative Signals" card:
   Toggle switches:
   - Penalise unexplained employment gaps (>6 months) [on by default]
   - Penalise sector mismatch [on by default]
   Input: "Maximum negative cap: -5%"

3. Save button (indigo, bottom right).
   "Reset to HireAI defaults" link (slate, small).

Visual Style: Sliders indigo throughout. Live total turns rose to warn.
Tooltips on each signal name explain what it measures.
Platform: Web, desktop-first.
```

---

## Screen 23 — Settings — Employer Tier Database

```
Employer tier database management. Upload, view, preview, and sync
the Excel file that powers employer prestige scoring.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar + settings tabs.

Sections:

1. "Current Database" status card:
   - Last sync: "January 31, 2026 · 09:14"
   - Employers loaded: 4,521
   - Status badge: "Up to date" (emerald) or "Stale >30 days" (amber)
   - "Re-upload" button + "Download current file" link

2. Upload Zone:
   Drag-and-drop Excel zone. Compact (120px tall).
   "Drop .xlsx file here"
   After upload: preview table (first 5 rows):
   Columns: Employer Name · Tier (1–5) · Country · Industry

3. Auto-Sync Schedule (card):
   "n8n syncs this file automatically on the 1st of each month."
   Last n8n run: timestamp + status (Success ✓ / Failed ✗).
   "Re-run sync now" button.

4. Tier Legend (card):
   Tier 1: Top-tier global tech (Google, Meta, Shopee)
   Tier 2: Large SEA tech companies
   Tier 3: Mid-size IT companies
   Tier 4: Small agencies / startups
   Tier 5: Non-IT / unknown employers

Visual Style: Status badge prominent. Preview table in light mode.
Tier legend shows each tier with coloured pill.
Platform: Web, desktop-first.
```

---

## Screen 24 — Settings — Billing & Subscription

```
Billing management page showing current plan, usage, invoices, and
upgrade options.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar + settings tabs.

Sections:

1. Current Plan card (indigo gradient border):
   - Plan name: "Agency" badge
   - "$149/month · Renews March 31, 2026"
   - Quota bars:
     CVs Parsed: 3,241 / 5,000 (indigo progress bar)
     Active Jobs: 7 / unlimited
     Team Seats: 7 / 10
   - "Upgrade to Enterprise →" link
   - "Cancel Plan" link (small, slate-500)

2. Payment Method card:
   - Visa card ending 4242
   - "Update card" button (outline). Stripe-secured badge.

3. Invoices table:
   Columns: Date, Invoice # (link), Amount, Status (Paid ✓ / Pending).
   "Download PDF" icon per row. Last 6 invoices shown.

4. Plan Comparison (expandable "View all plans" accordion):
   3-column table: Starter / Agency / Enterprise. Feature rows with
   ✓/✗ or value per cell.

Visual Style: Quota bars urgency: emerald <70%, amber 70-90%, rose >90%.
Current plan card has indigo left-accent border.
Platform: Web, desktop-first.
```

---

## Screen 25 — Settings — Agency Branding

```
White-label branding settings so candidates see the agency's identity
instead of HireAI branding on the application form.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar + settings tabs. Two-column: settings left, live
phone-frame preview right (sticky).

Left Column (settings):

1. Logo Upload card:
   Current logo preview (rectangular, 160×48 area, bordered).
   "Upload Logo" button (SVG / PNG, max 1MB).
   "Agency name text fallback" input (shown if no logo).

2. Brand Colour card:
   "Primary Button Colour" — hex input + colour swatch picker popup.
   Preview: "Apply Now" button rendered in the selected colour.

3. Custom Domain card (Agency plan+):
   "Candidate Application URL"
   Input: https://apply. [subdomain input] .hireai.io
   Status: "Not configured" (amber) or "Active · Verified" (emerald).
   "Verify Domain" button.

4. Hide HireAI Branding: toggle switch.
   "Available on Agency and Enterprise plans." note.

5. Save button.

Right Column (live preview, sticky):
Phone frame (iPhone-style, 375px width) showing Screen 6 (Application Form)
with the agency logo, primary colour, and domain applied in real time.
Updates on every change.

Visual Style: Live preview is the centrepiece — it convinces admins.
Colour picker shows hex + named swatches. Unverified domain = amber badge.
Platform: Web, desktop-first.
```

---

## ─── MULTI-AGENCY ────────────────────────────────────

## Screen 26 — Agency / Workspace Switcher

```
Workspace switcher dropdown. Appears when recruiter clicks their agency name
chevron in the bottom-left sidebar. Supports multiple agency memberships.

DESIGN SYSTEM (REQUIRED): [paste §0]

Trigger element: Sidebar footer row — agency logo (24px) + agency name +
chevron icon. Chevron rotates on open.

Dropdown Panel (280px wide, slides up from trigger):
1. "Switch workspace" label (uppercase, xs, slate-500).

2. Agency List (scrollable if >5):
   Each row:
   - Agency logo (32px circle, letter avatar if no logo)
   - Agency name (medium, slate-900)
   - Role badge (Admin = violet, Recruiter = slate)
   - Active indicator: indigo dot + "Current" label on active row
   - Hover: slate-50

3. Divider.

4. Actions:
   "+ Create New Workspace" (indigo text + plus icon)
   "⚙ Manage All Workspaces" (slate text + settings icon)

Animation: Slides up with shadow-xl. Outside click dismisses.
Current agency row: indigo-50 bg + indigo left border.

Platform: Web component.
```

---

## ─── SUPER ADMIN ─────────────────────────────────────

## Screen 27 — Super Admin — Tenant Overview

```
Platform owner super admin dashboard. Shows all agencies, usage, revenue,
and health across the entire HireAI platform.

DESIGN SYSTEM (REQUIRED): [paste §0]

IMPORTANT VISUAL DISTINCTION: Amber (not indigo) top accent bar (8px)
across full viewport width. Sidebar header reads "⚙ Platform Admin"
in amber. "Super Admin" amber badge in top bar. Makes it unmistakably
clear this is not a normal recruiter view.

Platform: Web, desktop-first.

Left sidebar: Platform Admin nav — Overview, Tenants, Usage & Billing,
Support, Platform Settings. Amber active states.

Main Content:

1. Platform KPI cards (5):
   Total Agencies · Active Subscriptions · MRR ($) ·
   Resumes Parsed This Month · Platform Uptime %

2. Tenants Table:
   Columns: Agency (logo + name), Plan badge, Seats, CV Usage / Quota
   (progress bar), Status (Active/Trial/Suspended), Joined,
   Actions (View · Impersonate · Suspend · Upgrade).
   - "Impersonate" = amber button. Logs admin in as that agency's admin
     for support without knowing their password.
   - "Suspend" = rose outlined.

3. Quota Alerts Card (amber-tinted):
   "3 agencies at >90% CV quota" — list with "Notify" button per agency.

4. Search + filter: Name, plan, status. "Export CSV".

Visual Style: Amber distinguishes admin zone. Impersonate button amber.
Progress bars: rose when >90%.
```

---

## Screen 28 — Super Admin — Tenant Detail Drilldown

```
Detailed view of a single agency when a super admin clicks "View" from
the Tenant Overview table.

DESIGN SYSTEM (REQUIRED): [paste §0]

Same amber admin accent (8px top bar, amber sidebar highlights).

Top: Breadcrumb: "Tenants / TechHire Vietnam". Back button. Agency logo.
"Impersonate" amber button + "Suspend" rose outline button top right.

Tab bar: Overview · Usage · Jobs · Team · Billing

Active Tab: Overview

1. Agency Info card:
   Logo, name, plan badge, country, joined date, primary admin email.

2. Usage Stats:
   CVs parsed this month / quota (bar). Jobs active. Team headcount.

3. Billing card:
   Stripe customer ID. Plan. Next billing date. Last invoice status.
   "View in Stripe →" link (opens Stripe dashboard in new tab).

4. Recent Activity Log (last 10 events):
   Timestamp, event type, detail.
   e.g. "Resume parsed — John Nguyen, DevOps Lead"
   e.g. "Job published — Senior React Developer"

5. Support Notes (textarea):
   "Internal notes about this agency — not visible to customer."
   Save notes button.

Visual Style: Amber accent through all admin chrome. Info cards in grid.
Activity log monospace timestamps, left-border accent.
```

---

## ─── UTILITY ─────────────────────────────────────────

## Screen 29 — Empty State Dashboard (First Login)

```
Dashboard shown to a brand-new recruiter who just completed onboarding
and has no data yet. Guides them to take the first action.

DESIGN SYSTEM (REQUIRED): [paste §0]

Layout: Same sidebar. Main content area shows empty state.

Centre of Page (large, welcoming):
1. Illustrated welcome graphic: abstract geometric shapes with an
   AI-themed icon (sparkles + document + person) in indigo/violet.
2. "Welcome to HireAI, [First Name]! 👋" heading (H1).
3. Sub: "You're all set. Start by posting your first job or importing
   candidate CVs."

3 Quick-Start Action Cards (horizontal row, large):
Each card: icon (64px), title, 1-line description, CTA button.
- 📝 "Post a Job" → Create Job Form
- 📂 "Import CVs" → Bulk Import
- ⚙ "Configure Scoring" → Settings Scoring

Sidebar nav items show 0 counts everywhere (empty badges) — normalised.

Visual Style: Warm, encouraging. Illustration uses brand indigo/violet.
Cards have hover lift. No "empty table" — replace with positive CTA.
Platform: Web, desktop-first.
```

---

## Screen 30 — Landing Page (Public Marketing)

```
Public marketing landing page for HireAI. Converts IT recruiters and
agency owners into trial sign-ups.

DESIGN SYSTEM (REQUIRED): [paste §0]

Page Structure:

1. Navigation Bar (sticky):
   HireAI logo left. Links: Features · Pricing · Blog · Customers.
   "Sign In" (outline) + "Start Free Trial" (indigo) right.

2. Hero Section:
   Left: H1 "Hire IT Talent. 10× Faster with AI."
   Subheadline: "Auto-parse CVs, score candidates, and generate job ads
   in seconds. Built for IT recruitment agencies."
   Two CTAs: "Start Free Trial — No card required" (indigo large) +
   "Watch 2-min Demo" (outline + play icon).
   Right: Animated product screenshot in browser frame (Dashboard).

3. Social Proof Bar:
   "Trusted by 500+ IT teams across Southeast Asia"
   5 greyscale company logos.

4. Feature Grid (3 columns, 6 cards):
   📄 AI Resume Parsing · ⭐ Smart Candidate Scoring
   ✍ Job Ad Generation · 🔗 LinkedIn Enrichment
   📊 Career Monitoring · 🏢 Multi-Agency Platform

5. How It Works (3 steps, horizontal):
   Upload CVs → AI Scores & Ranks → Review Top 20

6. Pricing (3-tier table):
   Starter $49 · Agency $149 (highlighted) · Enterprise Custom.

7. Testimonials: 2-column quote cards, avatar + name + company.

8. Final CTA Section: Indigo gradient bg, white text.
   "Ready to transform your hiring?" + "Start Free Trial" button.

9. Footer: Logo, columns (Product, Company, Legal), socials, copyright.

Visual Style: Modern SaaS. Indigo-violet gradient hero overlay. Cards hover.
Pricing middle tier elevated (ring + "Most Popular" badge).
Platform: Responsive web, desktop-first.
```

---

## Stitch Generation Order

> Start with Screen 9 (Dashboard) to lock the global design system.
> Export to Figma after Screen 9 before continuing.

| Priority | Screen | Flow |
|---|---|---|
| **1st** | 9 — Recruiter Dashboard | Sets design system |
| **Core Recruiter** | 13 — Job Detail + Application List | |
| | 14 — Kanban Pipeline | |
| | 15 — Candidate Profile Panel | |
| | 10 — Jobs List | |
| | 11 — Create/Edit Job | |
| **Auth** | 1 — Login | |
| | 2 — Sign Up | |
| | 3 — Forgot Password | |
| **Onboarding** | 8 — Agency Onboarding Wizard | |
| | 29 — Empty State Dashboard | |
| **Candidate-Facing** | 4 — Public Job Board | |
| | 5 — Job Detail (Public) | |
| | 6 — Application Form | |
| | 7 — Confirmation Page | |
| **AI Features** | 12 — Job Ad Generator | |
| | 16 — Candidate Search | |
| | 17 — Bulk Import | |
| **Reporting** | 18 — Reports & Analytics | |
| | 19 — Notification Center | |
| **Settings** | 20 — General | |
| | 21 — Team & Users | |
| | 22 — Scoring Weights | |
| | 23 — Employer Tier DB | |
| | 24 — Billing | |
| | 25 — Branding | |
| **Multi-Agency** | 26 — Workspace Switcher | |
| **Super Admin** | 27 — Tenant Overview | |
| | 28 — Tenant Detail | |
| **Public** | 30 — Landing Page | |
