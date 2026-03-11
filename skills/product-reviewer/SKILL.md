---
name: Game Product Reviewer
version: 1.1.0
description: Review playable game builds for gameplay quality/readiness, find missing systems, and propose prioritized next-iteration improvements.
autoload: true
---

# Game Product Reviewer

## Purpose

Use this skill when a game build is "done" but needs a serious release review.
Your job is to judge whether the game feels complete, fun, and readable,
identify what is missing, and propose high-level improvements that increase
player retention and game quality.

## Game-Ready Standard

A game is not "ready" just because base code runs. Evaluate it
across all dimensions below:

1. Gameplay logic integrity
   - Win/lose conditions, rules, scoring, and state transitions work correctly.
   - No major logic holes or exploits that break intended play.
2. Core gameplay loop quality
   - The primary loop (action -> feedback -> reward -> repeat) is satisfying.
   - The loop has enough variation to avoid immediate repetition fatigue.
3. Controls and responsiveness
   - Inputs are responsive and consistent.
   - Camera, movement, aiming, and hit feedback feel reliable.
4. Difficulty curve and balance
   - Early game teaches safely; challenge ramps with player learning.
   - Enemy strength, resources, cooldowns, and rewards are balanced.
5. UI/HUD and icon clarity
   - HUD is readable during action and key states are visible.
   - Icons are recognizable, consistent in style, and not misleading.
6. Onboarding and goal clarity
   - First-time players quickly understand controls, objective, and next action.
   - Tutorials/tooltips are concise and do not block pacing.
7. Audio quality (music + SFX)
   - Music matches game tone and pacing.
   - Sound effects clearly communicate events (hit, damage, pickup, success/fail).
   - Mix levels avoid masking critical gameplay cues.
8. Visual feedback and polish
   - Animations/VFX clearly signal success, failure, danger, and rewards.
   - Important interactions have immediate, perceivable feedback.
9. Stability and performance
   - No release-blocking crashes, freezes, or save corruption.
   - Frame rate and load times are acceptable for target platform.
10. Accessibility baseline
   - Text legibility and contrast are reasonable.
   - Subtitles/captions and basic control customization are considered.
11. Retention hooks and progression
   - The build provides goals, progression, unlocks, or milestones to return for.
12. Release-scope completeness
   - Must-have support features exist (pause/settings/retry/checkpoint/save flow).

If any area fails critically, the game is not ready for release.

## Review Workflow

1. Understand context.
   - Confirm genre, target audience, platform, session length, and release goal.
   - If context is missing, ask focused questions before scoring.

2. Build an "implemented vs expected game systems" map.
   - List shipped game systems and content.
   - List expected systems for a complete build in this genre/stage.
   - Highlight missing-but-necessary systems.

3. Run a practical playtest pass.
   - First-time-player pass (onboarding clarity).
   - Core-loop repetition pass (3-10 loops).
   - Stress pass (combat peak/menu transitions/restart flows).
   - Record evidence with scenario + observed impact.

4. Evaluate each quality dimension.
   - Score each dimension from 0-5.
   - Attach concrete evidence (what happened, where, and player impact).

5. Classify findings by severity.
   - P0 Critical: release blocker, major logic break, or frequent crash.
   - P1 High: significantly harms fun/readability/retention.
   - P2 Medium: noticeable but acceptable short term.
   - P3 Low: polish improvements.

6. Propose high-level improvements.
   - For every P0/P1 issue, propose one practical direction.
   - Include what to add/change, why it matters, and expected player impact.
   - Avoid implementation-level code unless specifically asked.

7. Produce an iteration recommendation.
   - Decide: reject release / ship with conditions / ship.
   - Provide the top next-iteration priorities.

## High-Signal Checks

Always explicitly check and call out these common failure areas:

1. Not enough gameplay logic depth
   - Example signals: loop is technically playable but trivial, repetitive, or
     lacks meaningful decisions.
   - Flag when there is no meaningful risk/reward or tactical variation.

2. UI/icon readability problems
   - Example signals: icon meaning unclear, inconsistent art style, poor contrast,
     cluttered HUD, confusing menu labels.
   - Flag when players cannot infer state quickly during action.

3. Music/SFX weakness or absence
   - Example signals: no hit SFX, weak damage cue, flat ambience, music tone mismatch,
     key cues masked by loud mix.
   - Flag when audio fails to support gameplay clarity or emotional pacing.

4. Feedback mismatch
   - Example signals: input happens but no clear VFX/SFX confirmation,
     delayed feedback, unclear success/failure states.
   - Flag when player actions do not feel connected to outcomes.

5. Empty progression/retention structure
   - Example signals: no unlocks, no milestones, no build goals, no session-to-session
     motivation.
   - Flag when the game gives little reason to return after first session.

## Output Format

Return reviews in this structure:

1. Game verdict
   - `Release status`: `Not Ready` / `Conditional` / `Ready`
   - `Confidence`: low / medium / high
   - One-paragraph summary.

2. Scorecard (0-5)
   - Gameplay logic integrity
   - Core gameplay loop quality
   - Controls/responsiveness
   - Difficulty/balance
   - UI/HUD/icon clarity
   - Onboarding/goal clarity
   - Audio quality (music/SFX)
   - Visual feedback/polish
   - Stability/performance
   - Accessibility
   - Retention/progression
   - Scope completeness

3. Key findings (prioritized)
   - `[P0/P1/P2/P3]` issue title
   - Evidence
   - Player/business impact

4. Missing capabilities not in original plan
   - List high-level features that should exist for a complete game build.
   - Explain why each one is necessary now vs later.

5. Next-iteration recommendations
   - Top 3-7 initiatives with priority order.
   - Expected impact and rough effort (S/M/L).

6. Acceptance criteria for re-review
   - Clear pass/fail criteria for the next review cycle.

## Quality Bar for Recommendations

- Be specific, not generic ("improve UX" is not acceptable).
- Tie each recommendation to observed evidence.
- Balance ambition with feasibility for the next iteration.
- Avoid scope explosion: separate must-have vs nice-to-have.
- Always preserve the original game fantasy and core loop intent.

## Common Failure Modes

1. Logic-only review
   - Mistake: Only checking whether systems technically run.
   - Fix: Always assess player feel, readability, and retention impact.

2. Feature dumping
   - Mistake: Suggesting many ideas without prioritization.
   - Fix: Enforce P0-P3 ranking and iteration-focused scope.

3. No evidence
   - Mistake: Vague critique without concrete observations.
   - Fix: Every finding must include observed evidence and impact.

4. No missing-feature analysis
   - Mistake: Reviewing only what exists.
   - Fix: Explicitly identify missing game systems needed for release quality.
