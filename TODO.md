# ClarusMD TODO

This tracker reflects the completed MVP state of the ClarusMD application. The MVP is complete, all known issues have been resolved, and this file now serves as a historical record of what was built.

Project Status: MVP status: Complete — April 7 2026. No pending items remain.

## Current Status
- [x] Landing page implemented
- [x] Single-file application architecture in `Index.html`
- [x] Tailwind CSS via CDN integrated
- [x] DM Sans via Google Fonts integrated
- [x] Vanilla JavaScript questionnaire flow implemented
- [x] 3-step questionnaire implemented for GPA, MCAT, and clinical hours
- [x] Results screen implemented with animated circular score indicator
- [x] Readiness score, tier badge, school matches, and recommendations implemented
- [x] Dashboard flow implemented from results to dashboard
- [x] Dashboard tabs implemented: The Chart, Treatment Plan, Differential, Lab Results
- [x] Core MVP HTML experience is functioning end to end

## Resolved Fixes
- [x] Adjust MCAT progress bar color thresholds so a score of `500` does not display as green
- [x] Replace the stat card tag label `Strong OK` with clearer status wording
- [x] Update Lab Results school matching so maximum inputs (`GPA 3.85`, `MCAT 515`, `150+ hours`) show all schools as top matches

## Completed Polish
- [x] Final UI polish pass across landing, results, and dashboard states
- [x] Review school-fit logic consistency between Results, Differential, and Lab Results
- [x] Verify progress and badge thresholds across GPA, MCAT, hours, and readiness views
- [x] Add lightweight regression checks for scoring, tiers, recommendations, and school matching

## Future Enhancements
Future enhancements and the full product roadmap are documented in FutureClarusMD.md.
