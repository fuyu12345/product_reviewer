---
name: art_direction_briefing
description: Convert rough visual requests into structured briefs and production prompts before generation.
---

# Art Direction Briefing

Before generating anything, reduce the request into a design brief with:

1. Deliverable type: character sheet, icon, splash art, UI illustration, sticker, logo mark, or other asset.
2. Usage context: game UI, app icon, website hero, social post, pitch deck, print, or internal concept.
3. Audience and tone: playful, premium, dark fantasy, family-friendly, retro, corporate, and so on.
4. Visual constraints: aspect ratio, silhouette readability, palette limits, background treatment, and text/no-text rules.
5. References and exclusions: what the asset should feel like and what it must avoid.

If two or more of those are missing, ask short follow-up questions instead of guessing.
When the brief is clear, summarize it back in 3-6 bullet points before image generation.

Then build a production prompt from the brief. The production prompt must:

- describe one clear primary subject and its pose/action;
- define composition and camera framing (centered, close-up, half body, full body, etc.);
- include hard negative constraints to avoid unwanted content;
- explicitly forbid unnecessary elements unless requested.
- for cutout deliverables, include removal-friendly background rules:
  one solid key color, visible in all four corners, with no pattern/gradient/noise.

Suggested hard negatives for clean cutout assets:

- no background scene/environment;
- no extra objects or secondary characters;
- no text, logo, watermark, border, UI frame, or collage layout;
- no visual noise, random particles, or decorative filler.
- no checkerboard/grid background and no fake transparency texture.

Tool sequence for every image task:

1. Call image generation (`image_generation` / `generate_image`) with the expanded production prompt.
2. Always call `remove_image_background` on the generated file.
3. If removal is weak, increase tolerance stepwise (28 -> 40 -> 60) and keep the best edge quality.
4. If fake transparency or background residue remains, regenerate with stricter key-color background constraints and run removal again.
5. Deliver the transparent PNG only after checking clean edges and no background residue on both dark and light preview backgrounds.

For every generated asset, explain:

- why the composition works,
- what visual signals communicate the intended tone,
- what to iterate next if the first pass is close but not final.
