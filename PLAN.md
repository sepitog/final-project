# ClarusMD Project Plan

ClarusMD is currently in the MVP Implementation Phase. This document defines the system direction that guides [AGENTS.md](./AGENTS.md), task tracking in [TODO.md](./TODO.md), repository structure in [FILE-INDEX.md](./FILE-INDEX.md), and testing for MVP logic in [UNIT-TESTS.md](./UNIT-TESTS.md).

## Project Description
ClarusMD is a web-based MVP application being built to help pre-med students in Ontario evaluate their readiness for medical school using academic, extracurricular, and admissions-related information.

## Project Goals
- Collect relevant user academic and extracurricular data through a structured intake process.
- Compare user profiles against Ontario medical school expectations in a consistent, explainable way.
- Generate a high-level match score that summarizes readiness.
- Provide targeted recommendations that help users improve future competitiveness.

## System Architecture Overview
### Input Layer
The input layer is being built to gather user profile data through a guided questionnaire covering academics, activities, and other readiness indicators.

### Processing Layer
The processing layer is being implemented to evaluate submitted data against structured Ontario medical school criteria and transform inputs into a match score and supporting logic outcomes.

### Output Layer
The output layer is being prepared to present readiness results, improvement recommendations, and future progress-oriented guidance.

## Current Implementation Scope
- Landing page UI (`index.html`) is integrated as the current application entry point.
- Questionnaire system is in development for collecting GPA, MCAT, and extracurricular inputs.
- Scoring logic is in development for translating questionnaire responses into readiness signals.
- Results dashboard is planned and partially defined for match summaries and recommendation output.

## Core Components
- Questionnaire module for collecting applicant data in a structured format.
- Matching engine for comparing user inputs against medical school requirements.
- Recommendation system for producing improvement guidance based on identified gaps.
- Progress tracking system for supporting future re-evaluation and longitudinal readiness monitoring.

## Data Strategy (Conceptual)
- User data should represent self-reported academic, extracurricular, and profile information collected through the questionnaire.
- School requirement data should represent structured Ontario medical school criteria used for comparison and scoring.
- These data types should remain separate so the system can evaluate readiness consistently and scale without mixing source information with user-specific inputs.

## Data Flow Concept
The intended system flow is:

User Input -> Processing -> Match Score -> Recommendations

This flow keeps ClarusMD organized as a pipeline rather than a set of disconnected features.

## Assumptions and Constraints
- The system assumes that users provide accurate and complete self-reported information.
- ClarusMD is focused on Ontario medical school readiness only in the current project scope.
- The current design does not include real-time requirement updates or external system integrations.

## Scope Boundaries
- The current phases do not include live admissions data, automated school data syncing, or external account connections.
- The project does not yet include production deployment, operational infrastructure, or external integrations.
- The current scope is limited to building the MVP questionnaire, scoring, matching, recommendations, and a partial results experience.

## Future AI Integration
- ClarusMD may later use AI to explain match results in clearer language, surface personalized recommendation themes, or summarize progress patterns over time.
- Any future AI capability should remain supportive and interpretive, not a replacement for the system's structured comparison logic.

## Development Phases
### Phase 1: Setup and Structure
Establish the project foundation, documentation system, initial file organization, and project controls.

### Phase 2: User Input
Build the questionnaire module and define the academic, extracurricular, and profile fields required for evaluation.

### Phase 3: Matching System
Implement the matching engine, scoring logic, and comparison framework for Ontario medical school readiness.

### Phase 4: Recommendations and Tracking
Build the recommendation workflow and expand the results experience so users can interpret outcomes and identify next steps.
