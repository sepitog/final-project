# ClarusMD Feature Reference

This document is the contributor-facing reference for the current ClarusMD application. It describes what the app does today, how the major surfaces behave, which logic powers the experience, and which issues are still pending.

## 1. Product Overview

ClarusMD is a pre-medical school readiness tool for Ontario students. It is currently implemented as a single HTML file with all UI, styling configuration, and JavaScript behavior contained in `Index.html`.

### Stack

| Area | Implementation |
|------|----------------|
| Markup | Single `HTML` file |
| Styling | Tailwind CSS via CDN |
| Fonts | DM Sans via Google Fonts |
| Logic | Vanilla JavaScript |
| Frameworks | None |
| External libraries | None beyond CDN-loaded Tailwind and Google Fonts |

### Design System

| Token | Value | Usage |
|------|-------|-------|
| Primary color | `#003366` | Branding, headings, active tabs, navbar accents |
| Accent color | `#10B981` | Primary buttons, highlights, progress states, positive badges |
| Background | `#FAFAF9` | Base page background |
| Font family | `DM Sans` | Global application font |
| Font weights | `400`, `500`, `600`, `700` | Body, labels, headings, badges |

## 2. Application Flow

The main user flow is:

`Landing page -> Start My MD Plan -> 3-step questionnaire -> Results page -> Create My Dashboard -> Dashboard`

### Primary State Transitions

| Trigger | Result |
|--------|--------|
| `Start My MD Plan` | Hides landing page and reveals questionnaire |
| Questionnaire `Next` buttons | Advance through steps 1 to 3 |
| Questionnaire `Finish` | Calculates score and shows results page |
| `Start Over` | Resets questionnaire state and returns to input flow |
| `Create My Dashboard` | Opens dashboard and populates all dashboard tabs |
| `Back to Results` | Returns from dashboard to results view |

## 3. Landing Page

The landing page is the public-facing marketing and onboarding surface.

### 3.1 Navbar

Features:

- Fixed navbar
- ClarusMD logo
- Navigation links: `Features`, `How It Works`, `Ontario Pre-Meds`, `Pricing`, `FAQ`
- `Log In` ghost button
- `Get Started` primary button
- Scroll behavior that changes the navbar to white with blur
- Mobile hamburger menu with collapsible navigation

### 3.2 Hero Section

The hero uses a two-column layout.

#### Left Column

- Heading: `Your Clearest Path to Medical School`
- Supporting description paragraph
- CTA buttons:
- `Start My MD Plan`
- `See a Sample Roadmap`
- Stats bar beneath the CTAs

#### Right Column

Animated dashboard mockup card containing:

- GPA display with gradient progress bar
- Weekly study schedule grid
- Hours logged grid for `Volunteer`, `Clinical`, and `Research`
- School match badge

### 3.3 Additional Landing Sections

The landing page includes six major sections after the hero, followed by footer content.

| Section | Contents |
|--------|----------|
| Pain Points | 4 cards with hover-lift animation |
| Features | 4 cards: `Med School Tracker`, `AI Study Schedule Builder`, `Experience and Hours Log`, `Mindset Hub` |
| Ontario Section | Chips for all 7 Ontario schools, a 3-stage timeline roadmap, and an expansion note |
| How It Works | 3 alternating steps with mockup panels |
| Testimonials | 4 testimonial cards |
| Pricing | Single pricing card with founding cohort badge, monthly and yearly pricing, 8 feature items, and CTA |
| FAQ | 6 accordion items with chevron rotation animation |
| Final CTA | Gradient card with floating sparkles icon |
| Footer | Navy background, 3-column link layout, animated heart icon |

## 4. Questionnaire

The questionnaire replaces the landing page once the user begins the assessment.

### 4.1 Structure

- 3 steps total
- Dot-based progress indicator
- Step label updates as the user advances
- Dots fill green as progress is made

### 4.2 Inputs

| Step | Prompt | Input Type | Constraints | Placeholder / Options |
|------|--------|------------|-------------|------------------------|
| 1 | GPA | Number input | `0` to `4.0`, step `0.1` | `3.87` |
| 2 | MCAT score | Number input | `472` to `528`, step `1` | `515` |
| 3 | Clinical and extracurricular hours | Select dropdown | 3 fixed options | `low`, `medium`, `high` |

### 4.3 Hours Dropdown Mapping

| Visible Label | Value |
|--------------|-------|
| Less than 50 hours | `low` |
| 50-150 hours | `medium` |
| 150+ hours | `high` |

### 4.4 Interaction Rules

- Each step uses a `Next` button except the final step, which uses `Finish`
- Focused inputs use an emerald border highlight
- Questionnaire is designed as a guided, linear flow

## 5. Results Page

The results page is the first personalized output surface after the questionnaire.

### 5.1 Main Components

- Animated SVG circular progress indicator
- Readiness score out of `100`
- Tier badge
- School match panel
- Recommendation panel
- `Start Over` button
- `Create My Dashboard` button

### 5.2 Circular Score Indicator

| Property | Behavior |
|----------|----------|
| SVG circumference | `440` |
| Initial state | `stroke-dashoffset: 440` |
| Animation target | Offset corresponding to score percentage |
| Duration | `1.2s` |
| Stroke color below `60` | Red `#EF4444` |
| Stroke color `60-79` | Yellow `#FBBF24` |
| Stroke color `80+` | Green `#10B981` |
| Score number animation | Counts from `0` to final score over `1.2s` using `requestAnimationFrame` |

## 6. Scoring System

The readiness score is the core output metric and is rounded to the nearest integer.

### 6.1 GPA Scoring

| GPA Range | Points |
|----------|--------|
| `3.9+` | `50` |
| `3.85+` | `47` |
| `3.7+` | `42` |
| `3.5+` | `35` |
| `3.3+` | `28` |
| `3.0+` | `20` |
| Below `3.0` | `10` |

Penalty rule:

- Apply multiplier `0.85` if GPA is below `3.3`

### 6.2 MCAT Scoring

| MCAT Range | Points |
|-----------|--------|
| `520+` | `30` |
| `515+` | `27` |
| `510+` | `23` |
| `505+` | `18` |
| `500+` | `12` |
| Below `500` | `5` |

Penalty rule:

- Apply multiplier `0.9` if MCAT is below `500`

### 6.3 Clinical Hours Scoring

| Hours Range | Points |
|------------|--------|
| `150+` | `20` |
| `100-149` | `15` |
| `50-99` | `10` |
| Below `50` | `5` |

### 6.4 Total Score Formula

1. Convert GPA, MCAT, and hours into point values.
2. Sum the three values.
3. Apply GPA penalty if GPA is below `3.3`.
4. Apply MCAT penalty if MCAT is below `500`.
5. Round the final value to the nearest integer.

## 7. Tier Classification

| Score Range | Tier | Badge Color |
|------------|------|-------------|
| `85+` | `Highly Competitive` | Green |
| `75-84` | `Competitive` | Green |
| `65-74` | `Borderline Competitive` | Yellow |
| Below `65` | `Not Competitive` | Red |

## 8. Results Page School Matching

The first-pass school matching on the results page is score-tier driven.

| Score Range | Match Output |
|------------|--------------|
| `85+` | Top Matches: `UofT`, `McMaster`, `Queens`; Also Apply: `Western` |
| `75-84` | Strong Matches: `Western`, `Queens`; Also Consider: `Ottawa` |
| `65-74` | Realistic: `Ottawa`, `TMU`; Stretch: `Western` |
| Below `65` | Options: `TMU`, `NOSM`; guidance to improve profile before applying broadly |

## 9. Gap Analysis and Recommendations

The recommendation system is based on benchmark gap analysis.

### 9.1 Targets

| Metric | Target |
|-------|--------|
| GPA | `3.85` |
| MCAT | `515` |
| Clinical Hours | `150` |

### 9.2 Gap Formulas

| Metric | Formula | Normalization |
|-------|---------|---------------|
| GPA | `max(0, 3.85 - GPA)` | Divide by `0.5` |
| MCAT | `max(0, 515 - MCAT)` | Divide by `15` |
| Hours | `max(0, 150 - actual hours)` | Divide by `100` |

### 9.3 Recommendation Rule

- The largest normalized gap determines the primary recommendation
- The second-largest normalized gap adds a secondary suggestion
- If no gaps remain, the output shifts to a maintenance-oriented message

## 10. Dashboard

The dashboard is the deeper planning and analysis view.

### 10.1 Top Bar

- Sticky top bar
- ClarusMD logo on the left
- User tier badge toward the center-right
- `Back to Results` button on the right

### 10.2 Tab System

The dashboard uses four pill-style tabs.

| State | Visual Style |
|------|--------------|
| Active | Navy background with white text |
| Inactive | White background, navy text, bordered |

### Dashboard Tabs

1. `The Chart`
2. `Treatment Plan`
3. `Differential`
4. `Lab Results`

## 11. Tab 1: The Chart

Subtitle: `Your Profile at a Glance`

Heading: `The Chart`

### 11.1 Stat Cards

The tab contains four stat cards in a responsive grid.

| Card | Main Value | Secondary Label |
|------|------------|-----------------|
| GPA | Value to 2 decimals | `/ 4.0 scale` |
| MCAT | Integer score | `/ 528 max` |
| Clinical Hours | Numeric value | `logged so far` |
| Readiness Score | Integer | `/ 100` |

### 11.2 Status Tag Rules

| Target Attainment | Color | Label Intent |
|------------------|-------|--------------|
| `90%+` of target | Green | Should indicate strength |
| `70-89%` | Yellow | `Moderate` |
| Below `70%` | Red | `Needs Work` |

Contributor note:

- The strongest label should not be `Strong OK`
- Preferred wording is closer to `On Track`, `Competitive`, or `Strong`

### 11.3 Progress Toward Target

This section contains three animated progress bars.

| Metric | Target | Right-Side Label |
|-------|--------|------------------|
| GPA | `3.85` | User GPA vs target |
| MCAT | `515` | User MCAT vs target |
| Clinical Hours | `150` | User hours vs target |

Bar color rules:

| Range | Color |
|------|-------|
| `90%+` of target | Green `#10B981` |
| `70-89%` | Yellow `#FBBF24` |
| Below `70%` | Red `#EF4444` |

Animation behavior:

- Bars animate from `0%` width to their target width
- Animation duration is `1s`
- Animation is triggered when the tab is first viewed

Contributor note:

- The current MCAT bar logic is percentage-based
- A score of `500` reads as roughly `97%` of `515`, which appears green
- This is misleading because `500` is average rather than competitive
- Threshold logic should be recalibrated so that:
- Scores below `505` appear yellow
- Scores below `500` appear red

### 11.4 School Match Section

- Displays match chips for all 7 Ontario medical schools
- Each chip includes a school name and match status badge

## 12. Tab 2: Treatment Plan

Subtitle: `Your Personalised Action Plan`

Heading: `Treatment Plan`

### 12.1 Focus This Month

Highlighted card with:

- Emerald gradient border
- Highest-priority action title
- One concrete first-step sentence

### 12.2 Gaps at a Glance

- Mini progress bars for GPA, MCAT, and Clinical Hours
- Each row shows current value versus target on the right

### 12.3 Action Cards

Three action cards appear in priority order:

1. `Critical`
2. `Important`
3. `Maintain`

Each card includes:

- Colored left border
- Priority label in matching color
- Title
- Timeline estimate
- Advice paragraph
- Bulleted list of `3-4` action steps

### 12.4 Severity Logic by Domain

#### GPA Advice Tiers

| GPA Range | Advice Intent |
|----------|---------------|
| `3.85+` | Maintain current approach |
| `3.7-3.84` | Push over threshold in one semester |
| `3.5-3.69` | Use upper-level science courses and consider post-bac |
| `3.3-3.49` | Consider formal post-bac program |
| Below `3.3` | Special Master's Program or master's degree path |

#### MCAT Advice Tiers

| MCAT Range | Advice Intent |
|-----------|---------------|
| Not taken | Register for MCAT |
| `515+` | Maintain strength and note McMaster CARS emphasis |
| `510-514` | Reach `515+` in one prep cycle |
| `505-509` | Structured retake with full study plan |
| `500-504` | Significant improvement with full strategy overhaul |
| Below `500` | Largest barrier; recommend professional support |

#### Hours Advice Tiers

| Hours Range | Advice Intent |
|------------|---------------|
| `150+` | Convert hours into strong stories via clinical journaling |
| `100-149` | Push to `150` milestone |
| `50-99` | Urgently build clinical foundation |
| Below `50` | Treat hours as critical gap requiring immediate action |

### 12.5 Combo Insight Card

This card appears conditionally based on profile combinations.

| Condition | Insight |
|----------|---------|
| GPA `3.7+` and MCAT below `505` | `Your GPA shows you can do hard academic work — the MCAT is your unlock.` |
| Hours below `100` and score below `65` | Clinical hours are the fastest win |
| Score `72-77` | Advises against applying this cycle and suggests waiting one semester |
| Score `85+` | Redirects focus toward ABS and CASPer preparation |
| GPA `3.85+` with no or low MCAT below `510` | GPA plus MCAT pairing insight |

### 12.6 Progress Tracker

White panel containing:

- Label: `X of 3 goals in progress`
- Progress bar based on number of checked action items
- Checklist of all three action item titles

Interaction rules:

- Clicking a checkbox row toggles checked state
- Checked items strike through their label
- Progress bar updates in real time

## 13. Tab 3: Differential

Subtitle: `How You Compare to Each School`

Heading: `Differential`

### 13.1 School Data

| School | GPA Minimum | GPA Average | MCAT Standard | CASPer | Notes |
|-------|-------------|-------------|---------------|--------|-------|
| University of Toronto | `3.6` | `3.89` | MCAT average `520`, full MCAT required | No | Hard GPA cutoff on OMSAS scale and 4 short essays required |
| McMaster | `3.0` | `3.95` | CARS only, minimum `123` | Yes | Only MCAT CARS is considered; uses problem-based learning |
| Queen's University | `3.0` | `3.78` | MCAT average `515`, full MCAT required | Yes | Roughly `100-140` seats and panel plus MMI interview |
| Western Schulich | `3.0` | `3.82` | MCAT average `515`, full MCAT required | No | No CASPer; leadership and advocacy written statements required |
| University of Ottawa | `3.0` | `3.78` | MCAT average `510`, full MCAT required | Yes | French stream available |
| TMU | `3.0` | `3.70` | MCAT average `506`, full MCAT required | No | Newer school with more holistic review |
| NOSM | `3.0` | `3.65` | No MCAT required | No | Prioritises Northern Ontario and rural applicants |

### 13.2 Badge Logic

#### GPA Badge

| Condition | Badge Color |
|----------|-------------|
| User GPA >= school average minus `0.05` | Green |
| Above minimum but below average threshold | Yellow |
| Below minimum | Red |

#### MCAT Badge

| Condition | Badge Color |
|----------|-------------|
| User MCAT >= school average | Green |
| Within `8` points below average | Yellow |
| More than `8` points below average | Red |
| School does not require MCAT | Green `N/A` |

#### Overall Fit Badge

| Rule | Output |
|------|--------|
| Both GPA and MCAT green | Green `Strong Fit` |
| Either badge yellow | Yellow `Possible` |
| Either badge red | Red `Out of Range` |

### 13.3 Ontario Tips Panel

The panel lists the following facts:

- McMaster only considers MCAT CARS with minimum `123`
- NOSM does not require the MCAT and prioritises Northern Ontario applicants
- UofT has a hard GPA cutoff of `3.6` on the OMSAS scale
- CASPer is required by McMaster, Queens, and Ottawa
- Ontario schools accept under `10%` of applicants on average

## 14. Tab 4: Lab Results

Subtitle: `What-If Simulator`

Heading: `Lab Results`

### 14.1 Inputs

The tab is pre-filled with the user's questionnaire values.

| Input | Type | Constraints | Note |
|------|------|-------------|------|
| GPA | Number | `0` to `4.0`, step `0.1` | Target note `3.85+` |
| MCAT | Number | `472` to `528`, step `1` | Target note `515+` |
| Clinical Hours | Select | Same 3 options as questionnaire | Target note `150+ hours` |

### 14.2 Live Recalculation

- All three inputs trigger recalculation on every change
- Score, tier, delta, and school-match output update live

### 14.3 Live Result Card

Contains:

- Projected score as large number out of `100`
- Projected tier badge
- Delta indicator

Delta behavior:

| Condition | Delta Output |
|----------|--------------|
| Same score as current | `(current)` |
| Higher than current | Green upward indicator with positive difference |
| Lower than current | Red downward indicator with negative difference |

### 14.4 Live School Match List

- Shows all 7 Ontario schools
- Status badges update in real time as inputs change

Contributor note:

- There is a known issue in this tab
- Perfect benchmark inputs such as GPA `3.85`, MCAT `515`, and `150+` hours still leave some schools in weaker categories
- Maximum or near-maximum profiles should show all schools as strong positive matches

## 15. Known Issues and Pending Fixes

### Issue 1: MCAT Bar Color in The Chart

Problem:

- A score of `500` currently displays green because `500 / 515` is approximately `97%`
- The visual system interprets this as above the `90%` threshold
- In practice, `500` is average and not competitive

Expected fix:

- Recalibrate bar thresholds so that:
- Scores below `505` show yellow
- Scores below `500` show red

### Issue 2: Status Tag Label

Problem:

- The strongest status tag currently reads `Strong OK`

Expected fix:

- Replace with clearer wording such as:
- `On Track`
- `Competitive`
- `Strong`

### Issue 3: Lab Results School Matching

Problem:

- The `schoolsFromScore` logic groups schools too conservatively in the highest tier
- At maximum inputs, the score reaches `97`
- Despite this, Western and Ottawa may still appear as weaker outcomes, while TMU and NOSM remain stretch-tier outputs

Expected fix:

- At score `85+`, all schools should show an appropriate positive match state
- The `Highly Competitive` tier should show all schools as at minimum `Possible` or `Reach`, not `Out of Range`

## 16. Animations and Interactions

### 16.1 Named Animations

| Animation | Behavior |
|----------|----------|
| `fade-in-up` | Hero columns animate on load over `0.6s` ease-out |
| `float` | CTA sparkles icon floats with `3s` infinite animation |
| `pulse-dot` | Dashboard active indicator pulses every `2s` |
| `heartbeat` | Footer heart animates every `1.5s` |

### 16.2 Hover Interactions

| Element | Behavior |
|--------|----------|
| Cards | Translate up `4px` and increase shadow over `300ms` |
| Primary buttons | Darken and lift `2px` |
| Ghost buttons | Gain navy-tinted background |

### 16.3 Progress and Motion

| Element | Behavior |
|--------|----------|
| Progress bars | Animate from `0` to target width over `1s` ease |
| Circular score indicator | Animates `stroke-dashoffset` over `1.2s` |
| Score number | Counts up over `1.2s` via `requestAnimationFrame` |
| FAQ accordion | Expands/collapses with `max-height` transition over `300ms` |
| FAQ chevron | Rotates `180deg` on toggle |

## 17. JavaScript Architecture

All JavaScript currently lives in a single `<script>` tag at the bottom of `Index.html`.

### 17.1 Shared State

The shared state object `DB` stores:

| Key | Purpose |
|-----|---------|
| `gpa` | Current GPA |
| `mcat` | Current MCAT |
| `hoursVal` | Current hours bucket value |
| `hoursNum` | Numeric hours mapping |
| `score` | Current readiness score |
| `tier` | Current readiness tier |
| `checkboxStates` | Treatment Plan checklist state |

### 17.2 Source-of-Truth Logic

- `calcScore` is the single source of truth for scoring
- It is reused by `finishApp`, `openDashboard`, and `recalcLab`
- This keeps score calculations consistent across results and dashboard surfaces

### 17.3 Key Functions

| Function | Responsibility |
|---------|----------------|
| `startApp` | Show questionnaire |
| `goToStep2` | Advance from step 1 to step 2 |
| `goToStep3` | Advance from step 2 to step 3 |
| `finishApp` | Calculate score and show results |
| `restartApp` | Reset state and return to questionnaire |
| `openDashboard` | Populate dashboard and show all tabs |
| `backToResults` | Return from dashboard to results |
| `switchTab` | Handle tab changes and trigger tab-specific animations |
| `buildChart` | Render The Chart tab |
| `animateChartBars` | Animate chart progress bars |
| `buildTreatment` | Render Treatment Plan tab |
| `animateTpBars` | Animate Treatment Plan bars |
| `buildActionItems` | Create severity-based treatment items |
| `getComboInsight` | Select conditional insight card |
| `toggleCheck` | Toggle progress tracker checkbox state |
| `updateProgress` | Recalculate checklist progress UI |
| `buildDifferential` | Render school-by-school comparison tab |
| `buildLab` | Render Lab Results simulator |
| `recalcLab` | Recompute lab outputs live |

### 17.4 Event Wiring

| Behavior | Trigger |
|---------|---------|
| FAQ accordion | Event listeners initialized at script load / DOM-ready timing |
| Navbar scroll effect | `scroll` listener toggling `scrolled` class |
| Tab visibility | Tab click handlers |
| Progress tracker | Checkbox row click handlers |
| Lab simulator | Input change handlers |

## 18. Contributor Guidance

When making changes, keep these constraints in mind:

- The app is still single-file, so UI, styling, and logic are tightly coupled
- `calcScore` should remain the single scoring authority
- Results, dashboard, and simulator outputs should stay logically aligned
- Threshold labels and color states need to remain semantically accurate, not just numerically convenient
- Known issues in `The Chart` and `Lab Results` should be treated as near-term cleanup work, not background polish
