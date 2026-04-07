# ClarusMD UI Architecture

This document explains how the MVP interface is built inside `Index.html`. It is intended for contributors, instructors, and reviewers who want to understand how the page is structured, how the UI changes between major application states, and how the JavaScript connects the visual surfaces together.

## Purpose

ClarusMD is implemented as a single-file front-end application. That means page structure, styling configuration, animation rules, state transitions, and rendering logic all live in one file. This document explains that build so a reader can open `Index.html` and understand how the interface is assembled.

It should answer:

- How is the file organized?
- What are the major UI surfaces?
- How does the user move between them?
- Which JavaScript functions power each part of the interface?

## High-Level File Organization

`Index.html` is organized into a few major layers.

### 1. `<head>` setup

The head includes:

- document metadata
- responsive viewport setup
- page title
- Google Fonts preload and DM Sans import
- Tailwind CDN
- a small `tailwind.config` extension for brand colors and font family

### 2. Custom Tailwind configuration

Tailwind is extended with:

- `navy`
- `navy-light`
- `sans` font family mapped to DM Sans and fallbacks

This allows the markup to use Tailwind utilities while keeping brand tokens centralized.

### 3. Custom CSS block

The `<style>` block defines:

- global box sizing
- smooth scrolling
- base body styles
- keyframe animations
- reusable interaction classes
- dashboard-specific helper classes
- some focused UI utilities not practical to express entirely with inline utility classes

### 4. Landing page section

Wrapped in `#landing-section`, this contains the marketing-style front page and all public-facing informational sections.

### 5. Questionnaire section

Wrapped in `#questionnaire-section`, hidden by default, then shown after the user clicks `Start My MD Plan`.

### 6. Results section

Wrapped in `#results-section`, hidden by default, then shown after score calculation.

### 7. Dashboard section

Wrapped in `#dashboard-section`, hidden by default, then shown after the user clicks `Create My Dashboard`.

### 8. Bottom script tag

All JavaScript logic lives in a single `<script>` block at the bottom of the file. This script controls:

- navigation state
- score calculation
- dashboard building
- simulator recalculation
- UI animations
- FAQ interaction
- navbar scroll behavior

## Landing Page Build

The landing page is built as a sequence of content sections inside `#landing-section`.

### Navbar

The navbar is fixed at the top of the viewport and built from:

- logo
- desktop navigation links
- desktop action buttons
- mobile hamburger toggle
- hidden mobile menu panel

Behavior:

- the `scrolled` class is toggled by JavaScript once the user scrolls past a small threshold
- that class changes the navbar background, blur, shadow, and bottom border
- mobile navigation is shown and hidden by toggling menu visibility and swapping menu/close icons

### Hero

The hero is a two-column grid:

- left column: headline, paragraph, CTAs, stats strip
- right column: dashboard mockup card

The hero demonstrates both the value proposition and the visual language of the product. It also introduces the user flow by making `Start My MD Plan` the highest-emphasis action.

### Pain Points

This section uses a four-card grid with hover-lift cards. Its role is narrative: it identifies the target user’s problems before the product explanation begins.

### Features

The features section is a two-column card grid describing the app’s four core product concepts:

- med school tracker and match
- AI study schedule builder
- experience and hours log
- mindset hub

Even where a feature is future-facing, the section is still part of the current landing experience.

### Ontario Section

This section reinforces scope and market focus. It is built from:

- an Ontario badge
- Ontario school chips
- a three-stage timeline card
- an expansion note

It gives the product a geographic and strategic frame.

### How It Works

This section uses alternating two-column step blocks. Each row pairs:

- explanatory copy on one side
- a mockup panel on the other

It turns the product into a procedural story rather than a feature list.

### Testimonials

This section is a four-card testimonial grid. The cards reuse the core white-card visual pattern and build social proof using consistent structure.

### Pricing

The pricing section is a single high-emphasis pricing card that includes:

- founding cohort badge
- pricing comparison
- eight feature rows
- CTA button

This section is visually stronger than most landing sections because it uses a thicker border and more explicit value framing.

### FAQ

The FAQ section is a stacked accordion. Each item includes:

- question button
- chevron icon
- hidden answer panel

JavaScript handles open/close state and chevron rotation.

### Final CTA

The final CTA is a bordered gradient-style card with:

- floating sparkles icon
- headline
- support text
- main button

Its purpose is to restate the product promise and funnel the user toward action after the informational sections.

### Footer

The footer uses a dark navy background and a multi-column layout:

- left brand block
- product links
- company links
- legal links

It closes the landing page with a more traditional SaaS-style footer structure.

## Questionnaire Build

The questionnaire lives in `#questionnaire-section`, which is hidden until the user starts the app flow.

### Step Indicator

The top of the card contains:

- three dots
- a step label

As the user advances:

- the visible step panel changes
- the next dot fills green
- the label updates from `Step 1 of 3` to `Step 2 of 3` and `Step 3 of 3`

### Step 1: GPA

This panel includes:

- question heading
- support text
- labeled number input
- `Next` button

### Step 2: MCAT

This panel follows the same pattern with MCAT-specific constraints and placeholder.

### Step 3: Clinical Hours

This panel switches from numeric input to a select field and ends with `Finish`.

### Focus Styling

Each questionnaire input uses:

- neutral border at rest
- emerald border on focus

This creates a clear interaction state without introducing a heavy form UI.

## Results Page Build

The results page lives in `#results-section` and is shown after `finishApp()` calculates outputs.

### Score Circle

The score indicator is an SVG-based circular progress ring built from:

- a gray background ring
- an active foreground ring with `stroke-dasharray` and `stroke-dashoffset`

The foreground ring color changes based on score band.

### Score Count-Up

The numeric score in the middle of the circle is animated separately using `requestAnimationFrame`, so the ring motion and the number increase feel synchronized.

### Tier Badge

The tier badge is populated dynamically and receives inline style updates depending on the score range.

### School Output

The school match panel shows text-based match groupings derived from the readiness score.

### Recommendation Output

The recommendation panel shows the primary and optional secondary gap-based guidance generated from GPA, MCAT, and hours gaps.

### Action Buttons

The results page ends with:

- `Start Over`
- `Create My Dashboard`

These buttons branch the user either back into the flow or into the deeper dashboard experience.

## Dashboard Build

The dashboard lives in `#dashboard-section` and represents the most application-like surface in the MVP.

### Sticky Top Bar

The top bar contains:

- ClarusMD logo on the left
- user tier badge on the right cluster
- back-to-results button

It is sticky so orientation is preserved while moving through deeper dashboard content.

### Pill Tab Navigation

Below the top bar is a horizontally arranged pill-tab system. Each tab button uses the shared `.db-tab` class and switches an associated panel in and out of view.

Tabs:

- The Chart
- Treatment Plan
- Differential
- Lab Results

### The Chart

This panel is the top-level summary view. It includes:

- subtitle and title
- stat cards
- target progress bars
- school match chip group

It functions as the dashboard overview panel.

### Treatment Plan

This panel is built from:

- focus card
- gap bars
- dynamically rendered action cards
- conditional combo insight card
- progress tracker with checklist

It is the most advice-heavy dashboard tab and is where score interpretation becomes actionable planning.

### Differential

This panel contains:

- title and intro copy
- school comparison cards/rows
- Ontario tips panel

It converts the overall readiness score into school-specific comparison logic.

### Lab Results

This panel contains:

- editable GPA/MCAT/hours inputs
- projected score card
- projected tier badge
- score delta indicator
- projected school match list

It functions as a live simulator and depends on the same core scoring logic as the results page.

## UI State Transitions

The MVP is not page-routed. Instead, it swaps between major interface sections by showing and hiding wrappers.

### Major Surface Switching

| From | To | Mechanism |
|------|----|-----------|
| Landing | Questionnaire | `startApp()` hides `#landing-section` and shows `#questionnaire-section` |
| Questionnaire | Results | `finishApp()` hides questionnaire and shows results |
| Results | Questionnaire | `restartApp()` resets form state and reopens questionnaire |
| Results | Dashboard | `openDashboard()` shows dashboard and populates it from shared state |
| Dashboard | Results | `backToResults()` hides dashboard and restores results view |

### Tab Switching

Dashboard panels are activated and deactivated through `switchTab(...)`, which:

- toggles active tab classes
- toggles active panel visibility
- triggers tab-specific animations where needed

### Animation Triggers

Animations are triggered in a few different ways:

- page-load style classes for landing hero content
- scroll-independent hover interactions for cards/buttons/chips
- explicit JS-driven progress animations for score ring and dashboard bars
- accordion state toggles for FAQ items

## Relationship Between UI and JavaScript

The UI is tightly coupled to the script block because the MVP is single-file.

### Shared State

The shared state object `DB` stores current user values and derived state such as:

- GPA
- MCAT
- hours selection and numeric mapping
- readiness score
- tier
- checklist state

This allows different views to stay synchronized.

### `calcScore()` as Core Logic

`calcScore()` is the central scoring engine. It matters because:

- `finishApp()` uses it to generate the first results page
- `openDashboard()` uses it to populate dashboard views consistently
- `recalcLab()` uses it for live simulator updates

That shared dependency is what keeps results, dashboard, and simulator outputs aligned.

### Function-to-Surface Mapping

| Function | UI Responsibility |
|---------|-------------------|
| `startApp()` | Enter questionnaire flow from landing page |
| `goToStep2()` / `goToStep3()` | Advance questionnaire steps and update dots/label |
| `finishApp()` | Calculate score and populate results page |
| `restartApp()` | Reset questionnaire and return to input flow |
| `openDashboard()` | Build and show dashboard |
| `backToResults()` | Return from dashboard to results |
| `switchTab()` | Activate dashboard tabs |
| `buildChart()` | Populate The Chart |
| `animateChartBars()` | Animate chart progress bars |
| `buildTreatment()` | Populate Treatment Plan |
| `animateTpBars()` | Animate treatment gap bars |
| `buildActionItems()` | Create severity-based action item objects |
| `getComboInsight()` | Choose conditional insight text |
| `toggleCheck()` / `updateProgress()` | Drive checklist interaction and completion bar |
| `buildDifferential()` | Populate school comparison panel |
| `buildLab()` / `recalcLab()` | Populate and update simulator panel |

## Notes for Future Maintainers

The current UI works well for the MVP, but it is tightly coupled in ways that matter for future changes.

### Current Tight Coupling

- structural HTML, styling logic, and application logic are all in one file
- several visual states are controlled by inline styles rather than reusable variants
- some status logic is repeated across results, dashboard, and simulator surfaces
- dashboard rendering depends on a coordinated set of build functions rather than isolated components

### Likely Refactor Boundaries

If the project grows, the cleanest future separation would be:

- layout and static sections
- reusable UI primitives
- score and recommendation engine
- school data source
- dashboard tab modules

### Most Sensitive UI Areas

The parts of the UI most likely to break when logic changes are:

- score ring and tier badge synchronization
- progress bars tied to threshold logic
- Differential school comparison rendering
- Lab Results simulator outputs
- Treatment Plan action-card generation

Those areas all depend directly on calculated values rather than mostly static content.

## Summary for a Reader Opening `Index.html`

If you open `Index.html`, you are looking at:

- a landing-page front end
- a guided three-step intake flow
- a score-driven results screen
- a four-tab dashboard
- a single shared JavaScript layer that controls all major UI transitions and derived outputs

The file is not organized as components in a framework sense, but it is organized as a sequence of clear UI sections backed by a shared state and score engine. That structure is what makes the MVP understandable, demo-ready, and still reasonably maintainable at its current scale.
