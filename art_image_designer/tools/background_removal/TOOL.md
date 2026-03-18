---
name: remove_image_background
description: Remove solid or near-solid edge-connected backgrounds and export a transparent PNG.
---

# Background Removal

Remove image backgrounds from generated assets and output a transparent PNG.

## Usage Notes

- Run this immediately after image generation for cutout assets.
- If edge quality is weak, adjust tolerance progressively (for example: 28, then 40, then 60).
- Reject outputs with fake transparency or visible checkerboard artifacts.
