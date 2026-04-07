# Changelog

## April 7, 2026

### Added
- Built the ClarusMD landing page in a single `Index.html` application
- Integrated Tailwind CSS via CDN, DM Sans from Google Fonts, and vanilla JavaScript
- Implemented the `Start My MD Plan` flow from landing page to questionnaire
- Implemented the `Create My Dashboard` transition from results to dashboard
- Added a persistent dashboard top bar with logo, tier badge, and Back to Results control

### Questionnaire
- Implemented a 3-step intake flow for GPA, MCAT score, and clinical hours
- Added step-based questionnaire navigation
- Added clinical hours dropdown options for `less than 50`, `50-150`, and `150+`

### Scoring
- Implemented a `0-100` readiness score
- Added tiered GPA scoring with a low-GPA penalty multiplier
- Added tiered MCAT scoring with a sub-500 penalty multiplier
- Added tiered clinical hours scoring
- Implemented final score rounding
- Implemented four readiness tiers: `Highly Competitive`, `Competitive`, `Borderline Competitive`, and `Not Competitive`

### Results
- Added animated circular progress visualization
- Added results page score display
- Added tier badge rendering
- Added school match output
- Added recommendation output based on benchmark gaps

### Dashboard
- Added `The Chart` tab with stat cards, status tags, progress bars, and Ontario school match chips
- Added `Treatment Plan` tab with focus card, gap bars, prioritized actions, contextual insights, and progress tracker
- Added `Differential` tab with all seven Ontario schools and Ontario-specific admissions notes
- Added `Lab Results` tab with live what-if simulation and projected score updates

### Ontario School Coverage
- Added school comparison coverage for University of Toronto (`UofT`), McMaster, Queen's University, Western (`Schulich`), University of Ottawa, TMU, and NOSM

### Known Issues
- MCAT progress bar threshold coloring still needs adjustment so `500` does not appear green
- One stat tag still shows `Strong OK` and needs clearer wording
- Lab Results school matching still underrates top-input scenarios for Western, Ottawa, TMU, and NOSM
