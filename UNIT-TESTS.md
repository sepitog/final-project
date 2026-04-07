# ClarusMD MVP Testing Strategy

## Testing Status
The ClarusMD MVP was validated through manual end-to-end testing of the questionnaire, scoring, results, and dashboard flows. This document defines the automated testing strategy planned for v1.1 and beyond. Automated test implementation is tracked in FutureClarusMD.md under Phase 7.

## Purpose
This document defines testing for MVP logic in ClarusMD. Testing is focused on validating scoring logic, tier classification, and recommendation outputs for consistency and correctness. It supports the system direction in [PLAN.md](./PLAN.md) and should evolve with active logic, data structures, and feature scope.

## Current Testing Focus
- Verify end-to-end questionnaire -> results -> dashboard flow in the functioning single-file MVP
- Validate score calculation consistency across results and simulator views
- Confirm tier badge, school match, and recommendation outputs remain aligned for the same inputs
- Catch regressions in known edge cases before future cleanup or refactoring

## Test Categories
### Input Validation
Testing should confirm that questionnaire data is complete, correctly formatted, and suitable for downstream evaluation.

### Evaluation Criteria
Input validation passes when all required fields are present, consistently formatted, and acceptable for system processing.

### Logic Accuracy
Testing should confirm that the scoring function, rule comparisons, and match score calculations behave consistently with the intended evaluation model.

### Evaluation Criteria
Logic accuracy passes when the same inputs produce consistent outputs and those outputs follow the defined comparison rules.

### Output Correctness
Testing should confirm that recommendation output and readiness results match the logic produced by the system.

### Evaluation Criteria
Output correctness passes when recommendations clearly reflect the evaluated strengths, gaps, and match score produced by the processing layer.

## Planned Test Areas
- Validation of required academic and extracurricular input fields.
- Scoring function behavior for GPA, MCAT, and extracurricular evaluation.
- Matching logic that compares user information against school requirements.
- Recommendation outputs for consistency, relevance, and alignment with identified gaps.
- Output consistency across repeated runs with the same inputs.
- Dashboard rendering consistency across The Chart, Treatment Plan, Differential, and Lab Results.

## Example Test Cases
- A complete user profile with all required fields should pass input validation and move into processing without missing-data errors.
- A user profile with weaker academic metrics but strong extracurricular involvement should produce a match score that reflects both strengths and gaps.
- A user profile that does not meet key requirements should receive recommendations that clearly target the missing or weaker areas.
- The same questionnaire response set should produce the same score, matches, and recommendations each time it is processed.

## MVP Testing Note
Testing is intended to support the active ClarusMD MVP build. Automated coverage should focus first on the scoring function, matching logic, and output consistency so implementation work can expand without breaking core evaluation behavior.
