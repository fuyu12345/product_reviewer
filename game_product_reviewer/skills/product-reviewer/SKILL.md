---
name: Game Product Reviewer
version: 1.3.0
description: Review playable game builds for gameplay quality/readiness, find missing systems, and propose prioritized next-iteration improvements.
autoload: true
---

# Game Product Reviewer

## Purpose

Use this skill when a game build is "done" but needs a serious release review.
Your job is to judge whether the game feels complete, fun, and readable,
identify what is missing, and propose high-level improvements that increase
player retention and game quality.

## EVO Strict Mode (Prompt-Only Policy)

When task text contains any of the controls below, enable strict EVO gate behavior:

- `[AI_REVIEW_ROUNDS=N]`
- `[AI_REVIEW_BLOCKER=P0|P1|P2]`
- `[AI_REVIEW_MODE=EVO]`

Rules:

1. Blocker issues are hard gates.
   - Any open issue at or above blocker threshold => verdict must be `Not Ready`.
2. Do not use vague wording.
   - Every key finding must include Issue ID, severity, evidence, impact, and recheck criteria.
3. Keep improvements in-iteration by default.
   - Recommendations are for same-iteration correction loops unless CEO explicitly requests a new iteration.
4. Enforce non-negotiable readiness gates.
   - Audio, asset/UI integration, gameplay complexity, and transparency integrity gates must all pass before any `Ready` verdict.
5. Do not issue soft pass language when hard gates fail.
   - If any non-negotiable gate fails, verdict must be `Not Ready` and include refinement instructions.

## Non-Negotiable Readiness Gates

These gates are mandatory. Any failed gate means release status is `Not Ready`.

1. Audio gate
   - Relevant music/SFX must exist for critical gameplay events.
   - Minimum event coverage check: attack/fire, hit confirmed, player damaged, enemy defeated,
     success/fail state, and core UI actions (confirm/cancel/warning).
   - Audio mix must keep critical cues audible during active gameplay.

2. Asset/UI integration gate
   - Core entities must have integrated visual assets, not isolated mockups.
   - Required core entities: main character, primary weapon class, and enemy roster.
   - For each required entity, verify related assets exist and are connected to gameplay/UI:
     in-game visual representation, iconography, and UI usage state (HUD/menu/status/inventory
     where applicable).
   - Art direction across character/weapon/enemy/icon/UI must be style-consistent.

3. Gameplay complexity gate
   - Build must provide more than a trivial single-action loop.
   - Require meaningful player decisions, interacting mechanics, escalating challenge,
     and progression/reward structure.
   - If gameplay is flat, repetitive, or lacks tactical tradeoffs, fail the gate.

4. Transparency integrity gate
   - Cutout assets must not use fake checkerboard/grid backgrounds as a transparency illusion.
   - Transparent regions should be truly alpha-cleared and remain clean on black/white/gray backdrops.
   - If edge halos, grid residue, or opaque background patches remain, fail the gate.

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
8. Asset/UI integration completeness
   - Main character, primary weapons, and enemy designs have related art/image/icon/UI assets.
   - Those assets are integrated into real gameplay and UI states (not standalone references).
9. Visual feedback and polish
   - Animations/VFX clearly signal success, failure, danger, and rewards.
   - Important interactions have immediate, perceivable feedback.
10. Stability and performance
   - No release-blocking crashes, freezes, or save corruption.
   - Frame rate and load times are acceptable for target platform.
11. Accessibility baseline
   - Text legibility and contrast are reasonable.
   - Subtitles/captions and basic control customization are considered.
12. Retention hooks and progression
   - The build provides goals, progression, unlocks, or milestones to return for.
13. Gameplay complexity and decision depth
   - Multiple mechanics interact to create tactical choices.
   - Risk/reward and timing/positioning/resource tradeoffs are present and readable.
14. Transparent asset background integrity
   - No fake checkerboard backgrounds or residual matte artifacts in exported PNG assets.
   - Edges remain clean when composited on dark/light backgrounds.
15. Release-scope completeness
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

3. Build evidence matrices for hard gates.
   - Audio event coverage matrix: list critical events and whether each has clear SFX/music cue.
   - Core entity asset integration matrix: main character, weapon, enemy -> in-game visual, icon, UI touchpoint, integration status.
   - Gameplay complexity matrix: decisions, mechanic interactions, escalation, progression.
   - Transparency integrity matrix: per-asset alpha quality result on black/white/gray background checks.

4. Run a practical playtest pass.
   - First-time-player pass (onboarding clarity).
   - Core-loop repetition pass (3-10 loops).
   - Stress pass (combat peak/menu transitions/restart flows).
   - Record evidence with scenario + observed impact.

5. Evaluate each quality dimension.
   - Score each dimension from 0-5.
   - Attach concrete evidence (what happened, where, and player impact).

6. Classify findings by severity.
   - P0 Critical: release blocker, major logic break, or frequent crash.
   - P1 High: significantly harms fun/readability/retention.
   - P2 Medium: noticeable but acceptable short term.
   - P3 Low: polish improvements.

7. Propose high-level improvements.
   - For every P0/P1 issue, propose one practical direction.
   - Include what to add/change, why it matters, and expected player impact.
   - Avoid implementation-level code unless specifically asked.

8. Produce an iteration recommendation.
   - Decide: reject release / ship with conditions / ship.
   - Provide the top next-iteration priorities.

9. Produce EVO gate summary.
   - Report current round status and whether pass gate is satisfied for this round.
   - Explicitly list unresolved blocker issues count.

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

4. Asset/UI design disconnected from gameplay
   - Example signals: character/weapon/enemy concept exists but is not reflected in
     in-game assets, icons, or UI states.
   - Flag when visual design deliverables are missing, inconsistent, or not integrated.

5. Feedback mismatch
   - Example signals: input happens but no clear VFX/SFX confirmation,
     delayed feedback, unclear success/failure states.
   - Flag when player actions do not feel connected to outcomes.

6. Empty progression/retention structure
   - Example signals: no unlocks, no milestones, no build goals, no session-to-session
     motivation.
   - Flag when the game gives little reason to return after first session.

7. Fake transparency / bad background removal
   - Example signals: checkerboard pattern baked into RGB pixels, opaque background residue,
     jagged halo edges after compositing.
   - Flag when "transparent" assets fail compositing quality on contrasting backgrounds.

## Output Format

Return reviews in this structure:

0. EVO Gate Summary
   - `target_rounds`
   - `current_round`
   - `blocker_threshold`
   - `blocker_open_count`
   - `pass_gate` (`true` / `false`)
   - `note` (one short sentence)

1. Game verdict
   - `Release status`: `Not Ready` / `Conditional` / `Ready`
   - `Confidence`: low / medium / high
   - `Hard gate check`: Audio gate pass/fail, Asset/UI integration gate pass/fail, Gameplay complexity gate pass/fail, Transparency integrity gate pass/fail
   - If any hard gate fails, `Release status` must be `Not Ready`.
   - One-paragraph summary.

2. Scorecard (0-5)
   - Gameplay logic integrity
   - Core gameplay loop quality
   - Controls/responsiveness
   - Difficulty/balance
   - UI/HUD/icon clarity
   - Onboarding/goal clarity
   - Audio quality (music/SFX)
   - Asset/UI integration completeness
   - Visual feedback/polish
   - Stability/performance
   - Accessibility
   - Retention/progression
   - Gameplay complexity and decision depth
   - Transparent asset background integrity
   - Scope completeness

3. Key findings (prioritized)
   - `[P0/P1/P2/P3]` issue title
   - `Issue ID` (e.g. `EVO-001`)
   - Evidence
   - Player/business impact
   - Recheck criteria (clear pass/fail condition)

4. Missing capabilities not in original plan
   - List high-level features that should exist for a complete game build.
   - Explain why each one is necessary now vs later.

5. Refinement instructions (must-do before re-review)
   - Provide 3-10 concrete instructions.
   - Each instruction must include: objective, required output, and pass condition.
   - Focus on unresolved hard gates first.
   - For transparency failures, require explicit background-removal recovery plan:
     single solid key-color generation background, removal step with tolerance tuning,
     and compositing validation on dark/light backgrounds.

6. Next-iteration recommendations
   - Top 3-7 initiatives with priority order.
   - Expected impact and rough effort (S/M/L).

7. Acceptance criteria for re-review
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
