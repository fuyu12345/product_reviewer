---
name: icon_system_design
description: Build consistent, readable icon systems optimized for small sizes and transparent delivery.
---

# Icon System Design

Use this workflow for icons and small-format assets:

1. Start from the action or object the icon must communicate.
2. Strip detail until the core silhouette remains readable at small sizes.
3. Keep stroke weight, corner radius, perspective, and shading style consistent across the set.
4. Reserve high contrast for the important edge or focal detail.
5. Test mentally at 16px, 32px, and 64px sizes before finalizing the prompt.
6. Keep the frame clean: one icon subject, minimal supporting detail, and no unrelated objects.

Prompting guidance:

- specify whether the icon is flat, outlined, filled, isometric, glossy, pixel-art, or skeuomorphic;
- specify background transparency or solid tile treatment;
- specify whether it must fit an existing product palette or design system.
- add negative constraints: no text, no watermark, no border frame, no extra symbols, no decorative clutter.
- for cutout icon sources, require one solid key background color (no gradient/pattern/checkerboard) visible at all four corners.

If the request is for a set of icons, design the system first, then generate each icon as part of the same family.
If a single icon reads like clip art or loses clarity at small size, simplify before regenerating.

Mandatory tool sequence:

1. Expand the raw user request into a detailed icon production prompt.
2. Generate with `image_generation` / `generate_image` using that expanded prompt.
3. Always run `remove_image_background` to produce the final transparent PNG cutout.
4. If background removal is weak, tune tolerance (28 -> 40 -> 60) and keep the cleanest edge result.
5. If checker/grid artifacts or fake transparency appears, regenerate with stricter key-color background constraints.
6. If any extra element appears, tighten the negative constraints and regenerate before delivery.
