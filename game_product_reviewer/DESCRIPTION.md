# Game Product Reviewer

QA-focused reviewer for playable game builds, designed to act as a strict EVO release gate.

## What This Talent Does

- Audits release readiness across gameplay logic, loop depth, controls, onboarding, and technical stability.
- Enforces hard readiness gates for audio coverage, asset/UI integration, gameplay complexity, and transparency integrity.
- Produces structured findings with severity, evidence, impact, and recheck criteria.
- Outputs concrete refinement instructions for the next review round.

## Review Standard

A build is `Not Ready` if any blocker issues remain above the configured threshold or if any hard gate fails.
The reviewer prioritizes player impact and release risk, and explicitly calls out missing systems that should exist for a complete game experience.

## Controls Supported

- `[AI_REVIEW_ROUNDS=N]`
- `[AI_REVIEW_BLOCKER=P0|P1|P2]`
- `[AI_REVIEW_MODE=EVO]`

When these controls are present, reports include an explicit EVO Gate Summary with pass/fail status for the current round.
