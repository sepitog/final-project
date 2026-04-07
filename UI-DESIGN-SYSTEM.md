# ClarusMD UI Design System

This document explains the visual system behind the ClarusMD MVP in `Index.html`. It is intended for contributors and reviewers who need to understand not just what the UI looks like, but how its design language is structured and why the interface feels consistent across the landing page, questionnaire, results page, and dashboard.

## Purpose

The ClarusMD MVP is built as a single-file interface, so design decisions are expressed directly in Tailwind utility classes, a small custom Tailwind theme extension, and a focused custom CSS block. This document serves as the UI reference for that system.

It should help a reader answer these questions:

- What visual language does ClarusMD use?
- Which design patterns repeat across the app?
- How are color, typography, motion, and interaction states handled?
- How should future UI additions stay visually consistent?

## Visual Identity

ClarusMD uses a visual style that is clean, professional, and optimistic. It is meant to feel medical and academic without becoming cold or overly clinical. The interface leans on soft neutrals, confident navy structure, and emerald accents to create a planning tool that feels credible but still motivating.

### Core Color Tokens

| Token | Value | Primary Use |
|------|-------|-------------|
| Navy | `#003366` | Brand identity, headings, active tabs, important labels, key structural emphasis |
| Navy Light | `#004080` | Supporting brand variation through Tailwind config |
| Emerald | `#10B981` | CTAs, positive states, progress, highlights, active steps |
| Stone Background | `#FAFAF9` | Default page background and soft section framing |
| Yellow Warning | `#FBBF24` | Borderline or moderate states |
| Red Alert | `#EF4444` | Weak/out-of-range states and negative score feedback |
| Gray Text | Tailwind gray range | Secondary copy, labels, and supporting UI text |

### Tone of the Palette

- Navy gives the UI authority and structure.
- Emerald communicates progress, momentum, and encouragement.
- Stone keeps the overall experience warm and less sterile than plain white.
- Yellow and red are used sparingly for status communication rather than brand expression.

## Typography

Typography is built around `DM Sans`, loaded from Google Fonts and set as the default sans-serif family through Tailwind config and the `body` rule.

### Font Strategy

| Usage | Weight / Treatment |
|------|--------------------|
| Body copy | `400` |
| UI labels and medium-emphasis text | `500` |
| Section headings and strong labels | `600` |
| Primary headings, hero messaging, and high-emphasis numbers | `700` |

### Heading Behavior

- `h1` is large, tightly tracked, and uses `clamp(...)` for responsive scaling.
- `h2` is slightly smaller but still prominent, also using `clamp(...)`.
- Both heading levels use navy to keep the page hierarchy anchored to the brand color.

### Copy Style

- Body text is generally gray rather than black, which softens the interface.
- Supporting labels often use uppercase microcopy with increased tracking to create a dashboard-style data language.
- Important figures such as GPA, readiness score, and dashboard stats use strong size and weight contrast.

## Layout System

The UI uses a small set of repeated container widths and spacing conventions rather than a deep component abstraction system.

### Container Widths

| Width | Use |
|------|-----|
| `max-w-[1400px]` | Navbar content |
| `max-w-[1200px]` | Most major landing sections |
| `max-w-[1000px]` / `max-w-[1100px]` | Dashboard and content-heavy areas |
| `max-w-[900px]` / `max-w-[800px]` / `max-w-[620px]` / `max-w-[560px]` | Focused cards, timeline blocks, questionnaire/results containers |

### Spacing Rhythm

- Major sections use `py-20` or `py-24` to create generous vertical pacing.
- Cards commonly use `p-6`, `p-8`, `p-10`, or `p-12` depending on emphasis.
- Gaps between major layout columns are intentionally large, especially in the hero and dashboard sections, to make the MVP feel airy and premium.

### Shape Language

- Rounded corners are used consistently across the interface.
- Small interactive elements tend toward `rounded-lg`.
- Cards generally use `rounded-xl` or `rounded-2xl`.
- High-emphasis CTA shells and match badges often use `rounded-full`.

### Borders and Shadows

- Borders are light and subtle, often using `rgba(0,0,0,0.08)` or `border-black/[0.08]`.
- Cards use soft shadows instead of heavy elevation.
- The visual system prefers thin borders plus soft depth rather than strong contrast outlines.

## Component Styling Patterns

The MVP relies on a handful of recurring component families.

### Navbar Links

- Styled through `.nav-link`
- Use soft gray text by default
- Gain navy text and a faint navy background on hover
- Are intentionally low-contrast until interacted with so the brand and CTA buttons remain primary

### Primary Buttons

- Styled through `.btn-primary`
- Emerald background with white text
- Rounded full-pill shape
- Gain a darker green tone, upward movement, and shadow on hover
- Used for major task-forward actions such as `Start My MD Plan`, `Get Started`, `Finish`, and `Create My Dashboard`

### Ghost Buttons

- Styled through `.btn-ghost`
- Transparent or lightly bordered by default
- Gain a navy-tinted background on hover
- Used for lower-priority actions such as `Log In`, `See a Sample Roadmap`, and `Start Over`

### Cards

Card patterns are the dominant building block across the landing page and dashboard.

Common card traits:

- white background
- light border
- rounded corners
- modest shadow
- generous interior padding

Specialized card types include:

- hover-lift informational cards
- dashboard stat cards
- insight cards with green-tinted emphasis
- action cards with severity-colored left borders
- pricing card with stronger border emphasis

### Chips and Badges

Several badge types appear repeatedly:

- Ontario school chips
- match badges
- tier badges
- active state pills
- founding cohort pill

Common badge behavior:

- rounded-full shape
- compact horizontal padding
- color tied directly to meaning
- moderate font weight to preserve legibility at small size

### Progress Bars

The UI uses multiple progress visualizations:

- hero mockup GPA bar
- weekly chart bars
- results circular score ring
- dashboard target progress bars
- Treatment Plan gap bars
- Treatment Plan checklist completion bar

The consistent pattern is that progress visuals are simple, color-driven, and easy to compare at a glance.

### Tab Pills

Dashboard tabs use a pill pattern:

- active tab: navy background, white text, navy border
- inactive tab: white background, navy text, light border
- hover state adds a faint navy tint to inactive tabs

This keeps navigation compact while still feeling like a segmented control.

### Inputs and Focus States

Questionnaire and simulator inputs share the same visual logic:

- white background
- light neutral border
- rounded corners
- navy text
- emerald border on focus

The emerald focus state is important because it visually ties data entry back to the app’s positive/progress accent.

## Motion and Interaction System

The MVP uses a small but intentional animation system. Motion is used to reinforce hierarchy, not to decorate every element.

### Named Animations

| Animation | Usage | Effect |
|----------|-------|--------|
| `fade-in-up` | Hero content and result card entry | Soft entrance from below with opacity fade |
| `float` | Final CTA sparkles icon | Gentle up/down motion |
| `pulse-dot` | Dashboard “Active” indicator | Subtle pulse to imply ongoing activity |
| `heartbeat` | Footer heart icon | Soft repeating scale pulse |

### Hover Motion

| Pattern | Behavior |
|--------|----------|
| Card hover | Lift by `4px`, stronger shadow, slightly stronger border |
| Primary button hover | Darken, lift by `2px`, gain shadow |
| Ghost button hover | Add tinted background |
| School chip hover | Gain emerald border and soft green shadow |

### Expand / Reveal Motion

- FAQ answers animate through `max-height`
- FAQ chevrons rotate when open
- Chart bars and dashboard bars animate into position
- Results score ring animates using `stroke-dashoffset`
- Score number counts up over time rather than appearing instantly

### Motion Philosophy

The design uses motion to achieve three things:

- make the landing page feel alive
- communicate state change clearly
- reward user progression through the product flow

## State Color Rules

Color is semantic throughout the UI.

### Positive / Success

- Emerald family
- Used for:
- active step dots
- success tier badges
- strong match states
- primary CTAs
- focus indicators
- completed or strong progress states

### Caution / Borderline

- Yellow / amber family
- Used for:
- moderate performance labels
- borderline score states
- cautionary progress bars
- “possible” or middling dashboard outcomes

### Negative / Out of Range

- Red family
- Used for:
- low score ring state
- weak match badges
- needs-work indicators
- low-performance target bars

### Semantic Mapping

| UI Surface | Positive | Caution | Negative |
|-----------|----------|---------|----------|
| Results ring | `80+` | `60-79` | below `60` |
| Tier badges | Highly Competitive / Competitive | Borderline Competitive | Not Competitive |
| Match badges | Strong Fit / Top Match | Possible / Moderate | Out of Range |
| Dashboard bars | On target or strong | Close but not there | Significant gap |

## Responsive Behavior

The MVP is designed primarily as a responsive desktop-first layout with mobile accommodations built into each major section.

### Navbar

- Desktop shows full nav links and action buttons
- Mobile collapses into a hamburger menu
- Mobile menu opens as a stacked white panel beneath the navbar

### Landing Sections

- Hero collapses from two columns to one
- Card grids reduce from four or two columns down to one or two as space tightens
- CTA rows wrap naturally
- Section containers preserve generous padding so content still feels breathable on smaller screens

### Questionnaire and Results

- Both use centered card containers
- Width is capped so forms remain readable
- Inputs remain full-width and touch-friendly

### Dashboard

- Top bar remains compact and sticky
- Tab row can horizontally scroll if space is tight
- Dashboard grids collapse to fewer columns through `auto-fit` and responsive utility classes
- Simulator inputs stack vertically when needed

## Design Consistency Notes

The MVP stays visually coherent because the same patterns repeat across multiple surfaces.

### Intentional Reuse

- Navy is always the structural anchor
- Emerald always signals movement, action, or positive status
- White cards on stone background define most content zones
- Rounded corners and light borders are used almost everywhere
- Dashboard and landing sections share the same card language even when their content differs

### Single-File Tradeoffs

Because everything lives in `Index.html`, some styling is split between:

- Tailwind utility classes
- custom CSS classes
- inline styles for special cases

This creates some duplication, especially in:

- badge styling
- card variants
- dashboard layout blocks
- inline hover behaviors on footer links and utility elements

That tradeoff is acceptable for the MVP, but future refactors should likely extract:

- shared badge variants
- shared card variants
- repeated spacing and panel patterns
- repeated status-color logic

## Guidance for Future UI Additions

If new UI is added to the MVP or post-MVP versions, it should follow these rules:

- Use navy for structure and emerald for action/progress
- Prefer white cards on stone backgrounds over new visual shells
- Reuse rounded-xl and rounded-2xl shapes instead of inventing new corner systems
- Keep borders light and shadows soft
- Use motion sparingly and tie it to interaction or state change
- Preserve semantic color meaning across badges, bars, and score states
- Match the current typography hierarchy before introducing new text styles

The central design principle is consistency with momentum: the UI should feel clear, reassuring, and progression-oriented at every step of the ClarusMD experience.
