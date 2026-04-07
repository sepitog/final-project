# NeoMD Project Plan

NeoMD is currently a planning-phase project with no implementation yet. This document defines the system direction that guides [AGENTS.md](./AGENTS.md), task tracking in [TODO.md](./TODO.md), repository structure in [FILE-INDEX.md](./FILE-INDEX.md), and future testing in [UNIT-TESTS.md](./UNIT-TESTS.md).

## Project Description
NeoMD is a conceptual web-based application designed to help pre-med students in Ontario evaluate their readiness for medical school using academic, extracurricular, and admissions-related information.

## Project Goals
- Collect relevant user academic and extracurricular data through a structured intake process.
- Compare user profiles against Ontario medical school expectations in a consistent, explainable way.
- Generate a high-level match score that summarizes readiness.
- Provide targeted recommendations that help users improve future competitiveness.

## System Architecture Overview
### Input Layer
The input layer gathers user profile data through a guided questionnaire covering academics, activities, and other readiness indicators.

### Processing Layer
The processing layer evaluates submitted data against structured Ontario medical school criteria and transforms inputs into a match score and supporting logic outcomes.

### Output Layer
The output layer presents readiness results, improvement recommendations, and future progress-oriented guidance.

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

This flow keeps NeoMD organized as a pipeline rather than a set of disconnected features.

## Assumptions and Constraints
- The system assumes that users provide accurate and complete self-reported information.
- NeoMD is focused on Ontario medical school readiness only in the current project scope.
- The current design does not include real-time requirement updates or external system integrations.

## Scope Boundaries
- The current phases do not include live admissions data, automated school data syncing, or external account connections.
- The project does not yet include production implementation, deployment planning, or operational infrastructure.
- The current scope is limited to planning the questionnaire, matching, recommendations, and progress tracking at a conceptual level.

## Future AI Integration
- NeoMD may later use AI to explain match results in clearer language, surface personalized recommendation themes, or summarize progress patterns over time.
- Any future AI capability should remain supportive and interpretive, not a replacement for the system's structured comparison logic.

## Development Phases
### Phase 1: Setup and Structure
Establish the project foundation, documentation system, conceptual file organization, and project controls.

### Phase 2: User Input
Design the questionnaire module and define the academic, extracurricular, and profile fields required for evaluation.

### Phase 3: Matching System
Define the matching engine, scoring logic, and comparison framework for Ontario medical school readiness.

### Phase 4: Recommendations and Tracking
Plan the recommendation system and progress tracking workflow so users can interpret results and identify next steps.
