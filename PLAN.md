# ClarusMD Project Plan

ClarusMD has reached MVP completion. This document defines the system direction that guides [AGENTS.md](./AGENTS.md), task tracking in [TODO.md](./TODO.md), repository structure in [FILE-INDEX.md](./FILE-INDEX.md), and testing for MVP logic in [UNIT-TESTS.md](./UNIT-TESTS.md).

## Project Description
ClarusMD is a functioning web-based MVP application that helps pre-med students in Ontario evaluate their readiness for medical school using academic, extracurricular, and admissions-related information.

## Project Goals
- Collect relevant user academic and extracurricular data through a structured intake process.
- Compare user profiles against Ontario medical school expectations in a consistent, explainable way.
- Generate a high-level match score that summarizes readiness.
- Provide targeted recommendations that help users improve future competitiveness.

## System Architecture Overview
### Input Layer
The input layer gathers user profile data through a guided questionnaire covering GPA, MCAT, and experience hours.

### Processing Layer
The processing layer evaluates submitted data against structured Ontario medical school criteria and transforms inputs into a match score, tier classification, school matches, and benchmark-based recommendations.

### Output Layer
The output layer presents readiness results, school matches, benchmark-based recommendations, an animated circular progress indicator, and a multi-tab dashboard for deeper planning.

## Current Implementation Status
- Landing page UI complete
- Multi-step questionnaire complete
- Scoring system complete
- Tier classification complete
- School matching complete
- Recommendation engine complete
- Results visualization (circular animation) complete
- Dashboard complete
- Single-file HTML MVP complete end to end

## Core Components
- Questionnaire module for collecting applicant data in a structured format.
- Matching engine for comparing user inputs against medical school requirements.
- Recommendation system for producing improvement guidance based on identified gaps.
- Dashboard and progress tracking system for supporting re-evaluation and longitudinal readiness monitoring.

## Data Strategy
- User data should represent self-reported academic, extracurricular, and profile information collected through the questionnaire.
- School requirement data should represent structured Ontario medical school criteria used for comparison and scoring.
- These data types should remain separate so the system can evaluate readiness consistently and scale without mixing source information with user-specific inputs.

## Data Flow Concept
The intended system flow is:

Input -> Processing -> Output

This flow keeps ClarusMD organized as a pipeline rather than a set of disconnected features.

## Assumptions and Constraints
- The system assumes that users provide accurate and complete self-reported information.
- ClarusMD is focused on Ontario medical school readiness only in the current project scope.
- The current design does not include real-time requirement updates or external system integrations.

## Scope Boundaries
- The current phases do not include live admissions data, automated school data syncing, or external account connections.
- The project does not yet include production deployment, operational infrastructure, or external integrations.
- The current scope is limited to the implemented MVP landing page, questionnaire, scoring, matching, recommendations, results experience, and dashboard.

## Future AI Integration
- ClarusMD may later use AI to explain match results in clearer language, surface personalized recommendation themes, or summarize progress patterns over time.
- Any future AI capability should remain supportive and interpretive, not a replacement for the system's structured comparison logic.

## Development Phases
### Phase 1: Setup and Structure
Complete

Establish the project foundation, documentation system, initial file organization, and project controls.

### Phase 2: User Input
Complete

Implement the questionnaire module and define the academic, extracurricular, and profile fields required for evaluation.

### Phase 3: Matching System
Complete

Implement the matching engine, scoring logic, and comparison framework for Ontario medical school readiness.

### Phase 4: Recommendations and Tracking
Complete

Implement the recommendation workflow and expand the results experience so users can interpret outcomes and identify next steps.

### Phase 5: Post-MVP Roadmap
Phase 5 and beyond are documented in FutureClarusMD.md.
