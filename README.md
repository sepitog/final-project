# ClarusMD

ClarusMD is a single-file MVP web application that helps Ontario pre-med students estimate medical school readiness from GPA, MCAT performance, and clinical experience. The current app is built in a single `Index.html` file using Tailwind CSS via CDN, DM Sans via Google Fonts, and vanilla JavaScript.

## Current Application Flow
`Landing page -> Start My MD Plan -> 3-step questionnaire -> Results -> Create My Dashboard -> Dashboard`

### Questionnaire
- Step 1: GPA input
- Step 2: MCAT score input
- Step 3: Clinical hours dropdown: `less than 50`, `50-150`, `150+`

### Results Experience
- Animated circular progress indicator
- Readiness score out of `100`
- Tier badge
- School match summary
- Personalized recommendation output

## Scoring System

### GPA
- `3.9+` = `50` points
- `3.85+` = `47` points
- `3.7+` = `42` points
- `3.5+` = `35` points
- `3.3+` = `28` points
- `3.0+` = `20` points
- Below `3.0` = `10` points
- Penalty multiplier: `0.85` if GPA is below `3.3`

### MCAT
- `520+` = `30` points
- `515+` = `27` points
- `510+` = `23` points
- `505+` = `18` points
- `500+` = `12` points
- Below `500` = `5` points
- Penalty multiplier: `0.9` if MCAT is below `500`

### Clinical Hours
- `150+` = `20` points
- `100+` = `15` points
- `50+` = `10` points
- Below `50` = `5` points

### Tier Classification
- `85+` = `Highly Competitive`
- `75-84` = `Competitive`
- `65-74` = `Borderline Competitive`
- Below `65` = `Not Competitive`

## Dashboard

### Top Bar
- ClarusMD logo
- User tier badge
- Back to Results button

### Tab 1: The Chart
- Four stat cards: GPA, MCAT, Clinical Hours, Readiness Score
- Color-coded status tags
- Animated progress bars toward GPA `3.85`, MCAT `515`, and hours `150`
- Progress bars use green for `90%+` of target, yellow/orange for `70-89%`, and red for below `70%`
- School match chips for all seven Ontario schools

### Tab 2: Treatment Plan
- Focus This Month hero card with top priority and concrete first step
- Mini gap bars for GPA, MCAT, and clinical hours
- Three priority-based action cards: `Critical`, `Important`, `Maintain`
- Timeline estimate, severity-based advice, and concrete action steps
- Contextual insight card for key input combinations
- Progress tracker with checkboxes, goal count, and progress bar

### Tab 3: Differential
- School-by-school comparison for University of Toronto (`UofT`), McMaster, Queen's University, Western (`Schulich`), University of Ottawa, TMU, and NOSM
- Each row includes admissions notes, GPA badge, MCAT badge, and overall fit badge
- Ontario-specific tips include McMaster using MCAT CARS only with a minimum of `123`, NOSM not requiring the MCAT and prioritizing Northern Ontario applicants, UofT using a hard OMSAS GPA cutoff of `3.6`, CASPer being required by McMaster, Queen's, and Ottawa, and Ontario schools accepting under `10%` of applicants on average

### Tab 4: Lab Results
- What-if simulator prefilled with the user's questionnaire answers
- Live GPA, MCAT, and clinical hours inputs
- Live projected score out of `100`
- Live projected tier badge
- Delta indicator versus current score
- Live school match list for all seven Ontario schools

## Recommendation System
The current recommendation layer is benchmark-based. It prioritizes the user's largest gap, provides a concrete next step, and expands advice inside the dashboard using source-backed guidance from AAMC, BeMo, Med School Insiders, Kaplan, Shemmassian Consulting, and Blueprint MCAT.

## Project Status
The ClarusMD MVP is complete as of April 7 2026. All known issues have been resolved. The MCAT progress bar color thresholds have been corrected, the stat card tag label has been updated with clearer wording, and Lab Results school matching now correctly reflects top-match status at maximum inputs. Future development is tracked in FutureClarusMD.md.
