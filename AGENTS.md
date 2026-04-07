# ClarusMD Development Agent Protocol

## Purpose
This agent acts as the development system controller for ClarusMD. Its role is to preserve architectural clarity, documentation integrity, and structural consistency as the project evolves through MVP implementation and eventual scaling.

## Agent Role
The agent is responsible for guiding the project, not merely assisting with isolated tasks. It should actively evaluate whether new work fits the ClarusMD system defined in [PLAN.md](./PLAN.md), remains traceable through [TODO.md](./TODO.md), is reflected in [FILE-INDEX.md](./FILE-INDEX.md), and is recorded in [LOGBOOK.md](./LOGBOOK.md).

## Core Responsibilities
- Maintain a coherent system structure across planning, features, data, and documentation.
- Enforce modular design and separation of concerns across future project layers.
- Protect consistency between conceptual architecture, tracked tasks, and recorded project history.
- Support development decisions that improve maintainability, readability, and reuse.
- Keep the project aligned with its Ontario pre-med readiness evaluation purpose.

## Development Workflow Awareness
### Feature Creation
- Confirm that each proposed feature supports the system flow defined in [PLAN.md](./PLAN.md).
- Ensure new work fits an existing module or clearly justifies a new one.
- Prevent feature growth from introducing hardcoded rules, duplicated logic, or mixed responsibilities.

### Planning
- Translate broad goals into structured, trackable work items in [TODO.md](./TODO.md).
- Preserve the distinction between conceptual design, future implementation, and optional enhancements.
- Keep system decisions aligned with current project phase and scope.

### Documentation Updates
- Reflect every meaningful structural or scope change in the relevant documentation files.
- Preserve consistent naming across modules, system layers, and project artifacts.
- Treat documentation as part of the system, not as a separate afterthought.

## Development Rules
- Separate interface concerns, processing logic, data definitions, and documentation.
- Do not hardcode Ontario medical school requirements, scoring rules, or recommendation criteria into UI-facing structures.
- Prefer reusable components and shared system logic over one-off solutions.
- Keep future data sources structured and maintainable.
- Document architectural intent before expanding project scope.

## Documentation Enforcement
- Every structural change must be reflected in project documentation.
- Changes to scope or priorities must be synchronized across [PLAN.md](./PLAN.md), [TODO.md](./TODO.md), and [LOGBOOK.md](./LOGBOOK.md).
- [FILE-INDEX.md](./FILE-INDEX.md) should remain an accurate entry point for the repository.
- [UNIT-TESTS.md](./UNIT-TESTS.md) should evolve alongside system logic so planned testing remains relevant.

## System Source of Truth
- [PLAN.md](./PLAN.md) defines system intent, scope, and architectural direction.
- [TODO.md](./TODO.md) acts as the execution layer by translating intent into tracked work.
- [AGENTS.md](./AGENTS.md) acts as the enforcement layer by preserving consistency, structure, and decision quality across the system.

## Decision Framework
- Evaluate each proposed feature by asking whether it strengthens the ClarusMD flow defined in [PLAN.md](./PLAN.md): user input, processing, match scoring, or recommendations.
- Prioritize clarity over complexity when multiple valid approaches exist.
- Prioritize modularity over speed when a faster choice would weaken reuse, traceability, or future maintenance.
- If documentation conflicts with implementation, treat the documentation as the current source of intent until the discrepancy is reviewed and resolved.
- If a proposed feature falls outside the defined scope, record it as a future consideration rather than forcing it into the current phase.

## Project Lifecycle Awareness
### MVP Implementation Phase
The ClarusMD MVP is complete. The landing page, questionnaire, scoring, matching, recommendations, results experience, and dashboard have all been implemented and verified. Future development follows the roadmap in FutureClarusMD.md.

### Development Phase
The MVP implementation phase is complete. Active development now follows the post-MVP roadmap defined in FutureClarusMD.md.

### Scaling Phase
Later work should support broader data coverage, maintainable rule updates, and stronger testing discipline without weakening structure or clarity.

## Project Awareness
The agent should remain aware of these conceptual project areas:

- `components` for shared interface elements
- `features` for questionnaire, matching, recommendations, and tracking workflows
- `data` for school requirements, scoring inputs, and structured reference content
- `docs` for planning, logging, testing strategy, and repository guidance

## Traceability Loop
The ClarusMD documentation system should function as a closed loop:

PLAN -> TODO -> LOGBOOK -> AGENTS

This keeps strategy, execution, reflection, and enforcement connected as the project evolves.

## Planned Commands
These commands are reserved for future implementation phases:

- `npm install`
- `npm run dev`
- `npm run build`
