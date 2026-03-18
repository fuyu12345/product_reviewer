---
name: character_concept_design
description: Design readable character concepts with strong silhouette, shape language, and clean cutout delivery.
---

# Character Concept Design

Use this workflow for new character creation:

1. Define function: protagonist, mascot, enemy, merchant, guide, or NPC class.
2. Define silhouette: broad and sturdy, tall and elegant, compact and cute, sharp and threatening, and so on.
3. Define shape language: circles for friendly, squares for stable, triangles for aggressive.
4. Define costume logic: what materials, props, and accessories explain the character's world and role.
5. Define palette: 2-4 dominant colors and one accent color.
6. Define expression and pose: the character should communicate their purpose immediately.

When prompting image generation:

- mention age range, body type, pose, camera framing, costume details, props, and mood;
- call out what must stay readable at thumbnail size;
- keep composition controlled: one main character, no crowded scene elements unless explicitly requested;
- include explicit exclusions: no random props, no extra characters, no text, no watermark, no UI frame;
- for cutout character assets, force one solid key background color with no checkerboard/pattern/gradient;
- avoid generic filler phrases unless they improve the visual result.

For character work, prefer outputs that are distinctive, easy to describe, and easy to iterate.
If the user wants multiple options, vary silhouette, palette, or era instead of making trivial changes.

Mandatory tool sequence for deliverables:

1. Convert the user order into a detailed production prompt first.
2. Generate with `image_generation` / `generate_image` using that refined prompt.
3. Always process the output with `remove_image_background`.
4. If removal is weak, tune tolerance in small steps and preserve clean subject edges.
5. If fake transparency (grid/checker residue) appears, regenerate with stricter key-color background instructions and retry.
6. Deliver only the clean transparent PNG result with no background residue.
