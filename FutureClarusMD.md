# Future ClarusMD Roadmap

This document captures the product roadmap and longer-term vision for ClarusMD beyond the current MVP. It should be used as an internal planning reference for development priorities, scope sequencing, and architectural direction. The goal is to make it easy for a developer, collaborator, or stakeholder to understand what exists now, what must be fixed next, and how the product should evolve over time.

## 1. Current MVP Status

The current ClarusMD MVP is a functioning single-file web application built in `Index.html` using Tailwind CSS and vanilla JavaScript. It has no backend, no user login, and no persistence layer. All UI, styling configuration, and application logic currently live in one HTML file.

The MVP currently delivers:

- A landing page
- A 3-step questionnaire covering GPA, MCAT, and clinical hours
- A results page with an animated readiness score
- A 4-tab dashboard:
- `The Chart`
- `Treatment Plan`
- `Differential`
- `Lab Results`
- Coverage for 7 Ontario medical schools

All MVP bugs have been resolved as of April 7 2026. See CHANGELOG.md for the full fix history.

## 2. Resolved Pre-Roadmap Fixes

All three pre-roadmap bugs were resolved before Phase 1 work begins. MCAT progress bar color thresholds corrected so 500 no longer displays as green. Stat card tag label updated from Strong OK to clearer wording. Lab Results school matching corrected so maximum inputs show all schools as top matches. See CHANGELOG.md for the full fix history.

## 3. Phase 1 Roadmap: Authentication and Persistence

- [ ] Add user accounts with login and signup
  Users should be able to create an account, log in securely, and return to their dashboard later.

- [ ] Save questionnaire answers across sessions
  GPA, MCAT, hours, and other future profile fields should persist in a database.

- [ ] Persist dashboard and progress tracker state
  Checkbox states, treatment plan progress, and any saved planning state should survive page refreshes and future visits.

- [ ] Allow users to update inputs and recalculate their score at any time
  The dashboard should become a living planning tool rather than a one-time result page.

- [ ] Add PDF export for dashboard and treatment plan
  Users should be able to export a clean summary for advising, planning, or personal tracking.

### Technical Considerations

- [ ] Add a backend service
  Recommended options: `Node.js` or `FastAPI`

- [ ] Add a database
  Recommended options: `MongoDB` or `PostgreSQL`

- [ ] Add JWT-based authentication
  Authentication should be simple, standard, and easy to extend later.

## 4. Phase 2 Roadmap: Deeper Questionnaire

The current 3-input intake is enough for the MVP, but it is not rich enough for stronger advising logic. The questionnaire should expand into a more complete applicant profile.

- [ ] Add year of study
  Options should include `Year 1`, `Year 2`, `Year 3`, `Year 4`, and `Graduate`.
  This is the highest-priority questionnaire expansion because advice for a first-year student is fundamentally different from advice for a fourth-year applicant.

- [ ] Add MCAT status and timing
  Capture whether the MCAT has already been written or is still planned, and when the planned test date is.

- [ ] Add CASPer readiness as a fourth scored input
  CASPer matters for multiple Ontario schools and should eventually influence matching and recommendations.

- [ ] Add research experience
  Track either publication count, lab hours, or both in a structured way.

- [ ] Separate extracurricular leadership from clinical hours
  Leadership should not remain bundled into general experience because it serves a different advising purpose.

- [ ] Add geographic preference
  Users should be able to indicate:
  `Ontario-only`, `all Canadian provinces`, or `open to U.S. schools`

## 5. Phase 3 Roadmap: Expanded School Data

The current school logic is hardcoded. That is acceptable for the MVP, but it will not scale or stay accurate across admissions cycles.

- [ ] Move school data into a structured source
  Admissions data should be editable without changing application logic.

- [ ] Add medical schools from all Canadian provinces
  Include schools such as `UBC`, `University of Alberta`, `Dalhousie`, `University of Manitoba`, and others.

- [ ] Add U.S. MD school matching
  Use AMCAS-aligned data where available.

- [ ] Add DO school matching
  This should be explicitly presented as an alternative pathway for lower-scoring profiles.

- [ ] Add Caribbean medical schools as a last-resort pathway
  These should be clearly contextualized and not presented as equivalent to Canadian or U.S. MD pathways.

### School Data Requirements

All school records should eventually include:

- [ ] GPA average
- [ ] MCAT average
- [ ] CASPer requirement
- [ ] Out-of-province acceptance rules
- [ ] International applicant acceptance rules
- [ ] Location preference factors

## 6. Phase 4 Roadmap: Treatment Plan Enhancements

- [ ] Persist treatment plan completion state across sessions
  Goal completion should be saved to the user profile once persistence exists.

- [ ] Add expandable resource links to action items
  Example:
  MCAT actions should link to official AAMC prep resources, and clinical hours actions should link to volunteer opportunity directories.

- [ ] Add a weekly check-in flow
  Ask users how the week went and adapt the plan accordingly.

- [ ] Add an application timeline view
  Include OMSAS deadlines and school-specific admissions dates for the current cycle.

- [ ] Build the Mindset Hub journaling feature
  This feature is already promised on the landing page and should include guided prompts such as `What is your why?` plus saved entries.

## 7. Phase 5 Roadmap: Dashboard and UX Improvements

- [ ] Add a fifth dashboard tab: `Application Timeline`
  This should show key OMSAS dates and school-specific deadlines.

- [ ] Add GPA trend input
  Users should be able to show an upward trajectory, which can influence advice and school matching.

- [ ] Add demo mode on the landing page
  Visitors should be able to experience the dashboard with sample data without completing the full questionnaire.

- [ ] Add a shareable results card
  Generate either a shareable link or a shareable image containing the user’s score and tier.

- [ ] Add a What If comparison mode
  Users should be able to save and compare two scenarios side by side.

## 8. Phase 6 Roadmap: Monetisation and Business

- [ ] Add a real Stripe payment flow
  The pricing section already exists visually and should eventually be backed by real billing.

- [ ] Define and enforce free vs paid feature gates
  Suggested structure:
  free tier = questionnaire + results
  paid tier = full dashboard

- [ ] Add founding cohort discount redemption
  This should support early-user pricing and launch promotions.

- [ ] Add a referral system
  Users should be able to invite others and unlock rewards or discounts.

- [ ] Add a waitlist capture flow
  This supports users who are interested but not ready to pay.

- [ ] Add product analytics
  Recommended tools: `Plausible` or `Google Analytics`

## 9. Phase 7 Roadmap: Technical Migration

The current single HTML file architecture is fine for the MVP, but it will not scale well once persistence, richer data, and new product surfaces are introduced.

- [ ] Migrate to a proper frontend framework
  Recommended options: `React` or `Next.js`

- [ ] Move scoring and gap analysis to a backend API
  This will allow versioning, auditing, and better test coverage.

- [ ] Add unit tests for the scoring engine
  This is critical before expanding school data or increasing questionnaire complexity.

- [ ] Set up CI/CD on GitHub
  Automated testing should run on every pull request.

- [ ] Add URL routing
  Each dashboard tab should eventually have a shareable route.

- [ ] Consider a mobile-first redesign pass
  This should happen once the core feature set is more stable.

## 10. Long-Term Vision

ClarusMD’s long-term goal is to become the go-to planning tool for pre-medical students across Canada. The product should keep the same core principle as it expands: turn overwhelming admissions complexity into a clear, personalised, actionable plan.

### Long-Term Milestones

- [ ] Launch the Ontario MVP to early users and gather real feedback
- [ ] Expand coverage to all Canadian provinces
- [ ] Add U.S. school matching
- [ ] Build a community layer
  Students should be able to anonymously compare profiles and share experiences.
- [ ] Explore partnerships with MCAT prep providers and pre-med advising services
- [ ] Build a mobile app

## 11. Guiding Principle

As ClarusMD grows, the product should stay grounded in one consistent principle:

- [ ] Convert confusing admissions information into clear, personalised next steps

That principle should guide roadmap decisions, technical migrations, feature prioritisation, and UX design.
