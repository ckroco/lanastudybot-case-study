# Experiment 01: Scoring characterization tests

## 1. Context

LanaStudyBot is a live Telegram MVP with real users. Its scoring remains deterministic.

This experiment established a small regression baseline for existing behavior before future changes. Production source code, test fixtures and proprietary scoring methodology remain private.

Repository-level working rules defined product invariants, data protection and approval boundaries for AI coding agents.

## 2. Delivery model

Product Owner / PM
→ Analyst / Planner
→ Implementor
→ Verifier
→ Reviewer
→ Product Owner / PM acceptance

These were responsibility stages carried out through explicit instructions in a controlled AI-assisted workflow. No autonomous multi-agent system or orchestration framework was created.

The human Product Owner retained scope, acceptance criteria and final acceptance. Implementation, verification and review were performed separately.

## 3. Product Owner constraints

- Preserve current product behavior and deterministic scoring.
- Make no changes to production code or questionnaire content.
- Use synthetic data and existing dependencies.
- Limit implementation to one new test file.
- Preserve existing user changes.
- Do not access production data, production configuration, the real database or live Telegram users.
- Do not deploy anything.

No LLM was added to user-facing scoring or result generation.

## 4. Experiment task

Create characterization tests that record selected existing scoring outputs and detect unintended changes.

Expected outputs were fixed in the tests rather than generated from production implementation constants. The experiment did not attempt exhaustive coverage or validate the assessment methodology.

## 5. Analyst / Planner

The planning stage inspected the private implementation and proposed a small set of synthetic cases covering:

- A complete questionnaire.
- Empty or missing responses.
- Multiple selections.
- Tie situations and result ordering.
- Descriptive responses.
- Unrecognized inputs.
- Repeatability and preservation of input data.

Detailed fixtures and expected assessment outputs remain private.

## 6. Implementor

Only one test file was added during implementation, containing 16 parameterized test cases.

No production code, scoring rules, questionnaire definitions or dependencies were changed by that step. Implementation stopped before test execution, leaving verification and review to separate stages.

## 7. Verifier

Verification was performed separately from implementation. Expected results were independently checked against the current private implementation.

Only the focused scoring test file was run in the existing environment.

**Recorded result: 16 tests passed in 0.40 seconds; exit code 0.**

No mismatch was found for the tested expectations. The complete-questionnaire case also confirmed repeatability and preservation of input data after repeated scoring calls. Other cases did not explicitly assert input preservation.

File checks supported the single-file implementation scope and confirmed that checked files remained unchanged during verification. No pre-implementation content snapshot was captured, limiting retrospective proof of preservation of earlier user changes.

This is a recorded local verification result. The private test suite is not published with this case study.

## 8. Reviewer

Review was performed separately from verification, without rerunning tests.

The Reviewer found that the initial tie-break regression cases did not fully distinguish the intended behavior from an alternative ordering. Those cases could still pass despite a regression in tie handling.

A stronger synthetic case was identified and checked during follow-up planning. It has not been implemented.

Review also noted limited input-preservation coverage and incomplete coverage of possible scoring outcomes. The recommendation was to accept the limited baseline with these gaps explicitly recorded.

## 9. Outcome

The Product Owner accepted the first experiment as a limited regression baseline and requested planning for the tie-break follow-up.

The experiment demonstrated planning, scoped implementation, separate verification, separate review and human acceptance.

No production data, live Telegram users or deployment were involved. Passing tests characterize selected existing behaviors; they do not validate the scoring methodology or establish live-product correctness.

## 10. Status and residual risk

**First experiment: completed and accepted as a limited baseline.**

**Tie-break follow-up: identified and planned, not implemented yet.**

The initial tie-break coverage gap remains. Coverage is representative rather than exhaustive, and input preservation is explicitly checked for one complete questionnaire.

The stronger follow-up’s inputs and expected assessment outputs remain private.

No tests were rerun and no deployment was performed while preparing this documentation.
