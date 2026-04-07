# ClarusMD TODO

This tracker reflects the current MVP state of the ClarusMD application. The core single-file HTML app is functioning, so this file now focuses on polish, consistency, and the remaining known fixes.

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

## Pending Fixes
- [ ] Adjust MCAT progress bar color thresholds so a score of `500` does not display as green
- [ ] Replace the stat card tag label `Strong OK` with clearer status wording
- [ ] Update Lab Results school matching so maximum inputs (`GPA 3.85`, `MCAT 515`, `150+ hours`) show all schools as top matches

## Next Steps
- [ ] Final UI polish pass across landing, results, and dashboard states
- [ ] Review school-fit logic consistency between Results, Differential, and Lab Results
- [ ] Verify progress and badge thresholds across GPA, MCAT, hours, and readiness views
- [ ] Add lightweight regression checks for scoring, tiers, recommendations, and school matching

## Future Enhancements
- [ ] Expand beyond the current Ontario school set
- [ ] Improve recommendation depth and maintain source-backed guidance
- [ ] Split UI, scoring, and school logic into more maintainable modules when the app moves beyond a single-file structure
