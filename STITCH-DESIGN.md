# STITCH-DESIGN.md — AI Recruitment Platform MVP

> **Tool:** Google Stitch (stitch.withgoogle.com)  
> **Workflow:** Copy each prompt block directly into Stitch to generate the screen.  
> **Design system** is defined once in Section 0 — reference it in every prompt.

---

## 0. Global Design System (use in every prompt)

```
DESIGN SYSTEM (REQUIRED):
- Platform: Web, Desktop-first (1440px), responsive down to 375px mobile
- Theme: Light with glass-accent elements
- Background: Soft Slate (#f8fafc)
- Surface / Card: White (#ffffff) with subtle shadow (0 2px 8px rgba(0,0,0,0.06))
- Primary Accent: Indigo (#4f46e5) for buttons, active states, links
- Secondary Accent: Violet (#7c3aed) for gradient highlights
- Success: Emerald (#10b981)
- Warning: Amber (#f59e0b)
- Danger: Rose (#f43f5e)
- Text Primary: Slate-900 (#0f172a)
- Text Secondary: Slate-500 (#64748b)
- Border: Slate-200 (#e2e8f0)
- Typography: Inter font family — 32px H1, 24px H2, 18px H3, 14px body
- Buttons: Rounded-lg (8px), full-width on mobile, icon + label
- Cards: Rounded-xl (12px), hover lift shadow
- Sidebar: 240px fixed, white, border-right
- Tone: Professional, clean, SaaS-grade — inspired by Linear and Notion
```

---

## Screen 1 — Landing Page (Public)

```
SaaS landing page for an AI-powered recruitment automation platform targeting
IT recruitment agencies and IT companies in Southeast Asia.

DESIGN SYSTEM (REQUIRED): [paste system from Section 0]

Page Structure:
1. Navigation Bar: Logo "HireAI" left, menu items (Features, Pricing, Blog),
   Sign In + "Start Free Trial" CTA button (indigo) right. Sticky on scroll.

2. Hero Section: Left-aligned headline "Hire Smarter. 10x Faster."
   Subheadline: "AI parses resumes, scores candidates, and writes job ads
   automatically. Built for IT recruiters." Two CTAs: "Start Free Trial"
   (indigo filled) and "Watch Demo" (outline). Right side: product screenshot
   mockup of recruiter dashboard in a browser frame with soft drop shadow.

3. Social Proof Bar: "Trusted by leading IT companies" + 5 greyscale
   company logos in a horizontal row.

4. Features Grid: 3-column card grid with icon, title, description:
   - Resume Parsing (document icon)
   - AI Candidate Scoring (star/chart icon)
   - Auto Job Ad Generation (pen/sparkle icon)
   - LinkedIn Enrichment (LinkedIn icon)
   - Career Update Monitoring (refresh icon)
   - Multi-tenant Agency Support (building icon)

5. How It Works: 3-step horizontal flow with numbered circles:
   Upload Resume → AI Scores & Ranks → Recruiter Reviews Top 20

6. Pricing Table: 3 tiers side-by-side
   - Starter $49/mo: 1 user, 500 resumes/mo
   - Agency $149/mo: 10 users, 5000 resumes/mo (highlighted, "Most Popular")
   - Enterprise Custom: Unlimited. Each with feature list and CTA button.

7. Testimonial: Single large quote card with avatar, name, role, company.

8. Footer: Logo, product links, legal links, "© 2026 HireAI", socials.

Visual Style: Modern, clean, trust-building. Subtle indigo-to-violet gradient
on hero background. Cards with hover lift. Generous whitespace.
Platform: Responsive web, desktop-first.
```

---

## Screen 2 — Recruiter Dashboard (Home)

```
Main recruiter dashboard for an AI recruitment SaaS — the home screen
after login showing pipeline overview and recent activity.

DESIGN SYSTEM (REQUIRED): [paste system from Section 0]

Layout:
- Left sidebar (240px): Logo, nav links (Dashboard, Jobs, Candidates,
  Applications, Reports, Settings), user avatar and tenant name at bottom.
- Top bar: Page title "Dashboard", date, notification bell, user avatar.
- Main content: 2 column layout (wide left, narrow right).

Main Content:
1. Stats Row (4 metric cards, top): Active Jobs, New Applications Today,
   Candidates Scored, Top-20 Shortlisted. Each card shows number (large,
   bold), label, and a small trend arrow (up/down with % vs last week).

2. Active Jobs Table (left, below stats): Columns: Job Title, Department,
   Applications, Top Score, Status (badge: Active/Paused/Closed), Actions.
   5 rows visible, "View all" link. Each row clickable.

3. Recent Applications Feed (right column): Vertical list of the 6 most
   recent applicants. Each item: candidate avatar initials circle, name,
   job applied to, AI score badge (0-100 coloured green/amber/red),
   "Review" button. Timestamp shown small below name.

4. Score Distribution Chart (left, bottom): Horizontal bar chart showing
   candidate score distribution: 0-20, 21-40, 41-60, 61-80, 81-100.
   Indigo bars. Shows which score band has most candidates.

Visual Style: Clean, data-focused, professional. Cards with subtle shadows.
Indigo accent on active nav item. Score badges: green ≥70, amber 40-69,
rose <40.
Platform: Responsive web, desktop-first (1440px).
```

---

## Screen 3 — Job Detail + Application List

```
Job detail screen showing a recruiter the candidates who applied to a specific
job, sorted by AI suitability score, with shortlist controls.

DESIGN SYSTEM (REQUIRED): [paste system from Section 0]

Layout:
- Same left sidebar as Dashboard.
- Top: Breadcrumb "Jobs / Senior Backend Engineer". Job status badge (Active).
  "Edit Job" and "View Ad" buttons top right.

Page Sections:
1. Job Summary Card: Job title (H1), department, location (remote), salary
   range, posted date. Short job description (3 lines, truncated). "View Full
   Ad" link.

2. Scoring Weights Panel (collapsible): Horizontal sliders for each signal —
   Keyword Match (25%), Job Title (20%), Employer Tier (20%), Sector (20%),
   Tenure (10%), Negatives (5%). "Recalculate Scores" button below.

3. Controls Bar: Search input, filter dropdown (All / Shortlisted / Reviewed /
   Rejected), sort selector (Score ↓, Date ↓), "Export CSV" button.
   Count: "127 applications · 20 shortlisted".

4. Candidate Table: Columns — Rank (#), Candidate Name + avatar initials,
   AI Score (badge, coloured), Job Title Match, Top Skill matches (3 pills),
   Shortlisted (star toggle), Actions (View, Reject). Top 20 rows have
   a gold star icon auto-filled in the shortlist column.
   Clicking a row opens side panel (see Screen 4).

Visual Style: Table rows have hover highlight (slate-50). Shortlisted rows
have a subtle indigo-left-border accent. Score badges are large (40px circle).
Platform: Responsive web, desktop-first.
```

---

## Screen 4 — Candidate Profile Side Panel

```
Candidate detail side panel that slides in from the right when a recruiter
clicks a candidate in the application list. Full-height overlay panel,
not a new page.

DESIGN SYSTEM (REQUIRED): [paste system from Section 0]

Panel Width: 480px, slides in from right, rest of page dimmed.

Panel Content (top to bottom):
1. Header: Candidate initials avatar (large, indigo circle), Full name (H2),
   Current job title, Current employer. LinkedIn icon button (links to URL).
   Close (X) top right. "Download Resume" and "Download Formatted Resume"
   icon buttons.

2. AI Score Row: Large circular score gauge (0-100) in indigo. Next to it:
   score breakdown table with 5 signals (keyword, title, tier, sector,
   tenure) showing percentage bar per signal. AI summary text below (2-4
   sentences explaining why candidate scored this way, in a light grey
   callout box with sparkle icon).

3. Contact Info: Email, Phone, LinkedIn URL (clickable), Applied date.

4. Employment History: Timeline-style list. Each entry: company name,
   employer tier badge (Tier 1/2/3/4/5 coloured chip), job title,
   date range, tenure in months shown as small tag.

5. Skills: Chip grid of normalised skills (indigo outlined pills).
   Skills matching the JD are highlighted (indigo filled).

6. Action Bar (sticky bottom): "Shortlist" button (star, indigo),
   "Schedule Interview" button, "Reject" button (outline, rose).
   Dropdown: "Move to stage →".

Visual Style: Clean white panel. Subtle animations on slide-in.
Timeline has indigo vertical line. Matching skills pop with filled style.
```

---

## Screen 5 — Resume Upload + Application Form (Candidate-Facing)

```
Job application form for candidates applying to an IT role. Clean, minimal,
focused. Candidate submits resume and profile details.

DESIGN SYSTEM (REQUIRED): [paste system from Section 0]

Layout: Centered single-column form, max-width 640px, white card on slate
background. Company logo and job title at top.

Form Steps (multi-step with progress bar at top, 3 steps):

Step 1 — Personal Details:
- Full name (text input)
- Email address (text input, with validation)
- Phone number (text input)
- LinkedIn Profile URL (text input, required — asterisk + tooltip:
  "Required for all applications")
- "Next" button (indigo, full-width)

Step 2 — Resume Upload:
- Large drag-and-drop upload zone (dashed border, indigo on hover):
  "Drop your resume here or click to upload"
  "Accepts PDF or Word (.docx). Max 5MB."
- File selected state: show filename, size, green checkmark, "Remove" link.
- Below: Optional cover note textarea (4 rows, placeholder: "Anything
  you'd like us to know?")
- "Back" (outline) and "Submit Application" (indigo) buttons.

Step 3 — Confirmation:
- Large green checkmark circle animation.
- "Application Received!" heading.
- "We'll review your profile and be in touch within 5 business days."
- "Browse other jobs" link.

Visual Style: Minimal, distraction-free. Progress bar in indigo.
Error states: rose border + error message below field.
Mobile-first layout (fits 375px perfectly).
Platform: Responsive web, mobile-first.
```

---

## Screen 6 — AI Job Ad Generator

```
Job ad generation screen inside the recruiter dashboard. Recruiter fills in
job details, AI generates the ad, recruiter reviews and approves.

DESIGN SYSTEM (REQUIRED): [paste system from Section 0]

Layout: Same sidebar. Two-column layout (form left, preview right).

Left Column — Job Details Form (inputs):
1. Job Title (text input)
2. Department (select dropdown)
3. Location (text + Remote toggle switch)
4. Salary Range (min–max text inputs, currency selector)
5. Key Responsibilities (textarea, 5 rows)
6. Required Skills (tag input — type and press enter to add pills)
7. Nice-to-have Skills (tag input)
8. "Generate Job Ad" button (indigo, with sparkle icon, full-width)

Right Column — Generated Ad Preview:
- Initially: Empty state with illustration and "Fill in details and click
  Generate to create your AI job ad" message.
- After generation: White card with generated ad text (formatted with
  headings: About the Role, Responsibilities, Requirements, What We Offer).
  Word count shown. "Approve & Publish" button (emerald, full-width).
  "Regenerate" button (outline). "Edit manually" toggle.

Status banner: "Generating your job ad..." with indigo spinner (shows
during 3-5s generation).

Visual Style: Split panel. Left form area slate-50 background.
Right preview area white with border-left. Generated text uses
readable body typography. Indigo sparkle icon on generate button.
Platform: Responsive web, desktop-first.
```

---

## Screen 7 — Candidate Intelligence Search

```
Semantic search + filter screen for searching the candidate database using
natural language queries and structured filters.

DESIGN SYSTEM (REQUIRED): [paste system from Section 0]

Layout: Same sidebar. Full-width content area.

Top Search Bar (large, prominent):
- Wide search input (full row width): "Search candidates by skills, job title,
  experience..." Magnifying glass icon left. Clear button right.
  Indigo border on focus. Subtext below: "Try: 'Senior DevOps with Kubernetes
  and AWS, 5+ years'"

Filters Row (below search, horizontal):
- Skill chips (multi-select dropdown): e.g. Python, React, DevOps
- Experience (slider: 0–20 years)
- Employer Tier (1–5 checkbox group)
- Sector (IT, Fintech, E-commerce...)
- Score ≥ (number input)
- "Reset Filters" link

Results Grid (card grid, 3 columns):
Each card shows:
- Candidate initials avatar (circle, coloured by score)
- Name, current job title, current employer (with tier badge)
- Top 4 skill pills
- AI Score badge (large, coloured circle)
- Tenure indicator: "Avg 2.3 yrs / role"
- "View Profile" button

Empty state: Illustration + "No candidates match your search.
Try different keywords or filters."

Visual Style: Search bar is Hero-level, stands out. Card grid uses
hover lift animation. Skill pills are tightly spaced. Score badge
is centre-right of card (large, circle, coloured).
Platform: Responsive web, desktop-first.
```

---

## Screen 8 — Settings: Scoring Weights (Tenant Config)

```
Settings page for a recruitment agency admin to configure default AI scoring
weights, upload the employer tier database, and manage tenant preferences.

DESIGN SYSTEM (REQUIRED): [paste system from Section 0]

Layout: Same sidebar (Settings highlighted). Top tabs: General | Scoring |
Employer Tiers | Users | Billing.

Active Tab: Scoring

Page Content:
1. Header: "AI Scoring Configuration" (H2). Subtext: "These weights apply
   globally for all jobs in your account. Overrides can be set per job."

2. Scoring Weights Table: 5 rows with signal name, description, and
   a horizontal slider (0–100) + live percentage display.
   Signals: Keyword Relevance, Job Title Match, Employer Tier,
   Sector Experience, Tenure Stability.
   Below each slider: small grey description text.
   Live "Total: 100%" shown — turns rose if not equal 100%.

3. Negative Signals Panel: Toggle switches for:
   - Penalise unexplained gaps (> 6 months)
   - Penalise mismatched industry
   Cap input: "Maximum penalty: -5%"

4. Employer Tier Database Section: Title + "Upload Excel" drop zone (small,
   compact). Shows last uploaded date and row count:
   "4,521 employers loaded · Last synced 3 days ago". "Re-upload" button.

5. Save Button: "Save Configuration" (indigo, bottom right).

Visual Style: Clean settings layout. Each section in a white card.
Sliders use indigo thumb and track. Total percentage shows validation
state (emerald if 100%, rose if not).
Platform: Responsive web, desktop-first.
```

---

## Stitch Prompt Order Recommendation

| # | Screen | Priority | Start here? |
|---|---|---|---|
| 1 | Landing Page | 🔴 High | After Dashboard |
| 2 | Recruiter Dashboard | 🔴 High | **Start here** |
| 3 | Job Detail + Application List | 🔴 High | 2nd |
| 4 | Candidate Profile Side Panel | 🔴 High | 3rd |
| 5 | Application Form (Candidate) | 🟠 Medium | 4th |
| 6 | AI Job Ad Generator | 🟠 Medium | 5th |
| 7 | Candidate Intelligence Search | 🟡 Low | 6th |
| 8 | Settings: Scoring Weights | 🟡 Low | Last |

> **Tip:** Start with **Screen 2 (Dashboard)** to establish the visual system,
> then generate all other screens referencing the same design tokens.
> Export to Figma after Screen 2 to lock the design system before continuing.
