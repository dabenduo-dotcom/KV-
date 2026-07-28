---
name: build-kv-asset-library
description: "Analyze a reference KV, campaign poster, long infographic, hero image, or brand artwork and turn its visual language into a reusable five-part raster asset library: backgrounds, transparent atmosphere elements, decorative 3D icons, product assets with useful views, and typography treatments. Use when the user asks to extract visual assets, reverse-engineer a brand style, generate isolated design materials, create transparent PNG cutouts, fix checkerboard or mosaic fake-transparency, test an updated image prompt, or organize generated brand assets for downstream design."
---

# Build KV Asset Library

Create reusable visual parts, not a reconstruction of the source poster. Use the source only to infer palette, materials, lighting, shape language, typography behavior, and object evidence.

## Required workflow

1. Read every attached request file completely and inspect every reference image before generating.
2. Summarize observed visual evidence separately from estimates and inferences.
3. Define one shared brand anchor covering palette, material, lighting, camera, edge softness, and negative constraints.
4. Plan the five systems in this order:
   - backgrounds
   - atmosphere elements
   - decorative 3D icons
   - product assets and useful views
   - typography treatments
5. Generate each deliverable as an independent bitmap asset. Do not recreate the original poster or long-page layout.
6. Verify outputs, retry failed transparency or composition, then organize semantic filenames and create a manifest.

Use the image generation capability for all raster creation and editing. Do not create visual pixels with Python, HTML, CSS, SVG, Canvas, Three.js, or procedural graphics unless the user explicitly requests that method.

## Source analysis

Label conclusions as:

- **Observed**: directly visible in the reference.
- **Estimated**: approximate color, lighting, material, or camera interpretation.
- **Inferred**: a reusable extension that fits the visual system but is not literally present.

Extract at minimum:

- theme and audience
- emotional tone
- dominant and supporting colors
- material and surface language
- lighting direction, softness, and shadow behavior
- camera/viewpoint conventions
- shape and corner language
- typography hierarchy and treatment
- product/object evidence

Do not infer unrelated products or decorative motifs when the reference provides stronger evidence.

## Shared brand anchor

Write a compact anchor and prepend it to every prompt. Keep the same:

- palette relationships
- material family
- lighting direction and softness
- camera conventions within an asset family
- background policy
- exclusions: no logo, no watermark, no readable advertising copy, no full poster layout

Allow only the named subject, view, and background mode to change between assets.

## Five-system requirements

### 1. Backgrounds

Generate background-only fields. Remove products, icons, typography, cards, and poster composition. Produce useful variants such as a neutral field, brand gradient, light environment, and subtle material texture.

### 2. Atmosphere elements

Generate one isolated element per file: glow, streak, particles, paper swoosh, ribbon, mist, splash, or shadow patch when supported by the source.

Default to true transparent RGBA PNG. Read [transparency.md](references/transparency.md) before generating any transparent or translucent asset.

### 3. Decorative 3D icons

Use one consistent camera, material, scale, light direction, and background across the icon family. Generate each icon separately with a complete silhouette and generous margins.

### 4. Product assets

Generate the primary evidenced object first. When useful, include:

- three-quarter or 45-degree hero view
- straight front view
- true top view
- side/back view when meaningful
- material or construction detail
- separately usable accessory components

Use a clean catalog background unless transparent output is requested. Keep surfaces free of logos and readable copy.

### 5. Typography treatments

Generate neutral type specimens rather than copying the poster headline. Use the exact sample text `Aa 0123` unless the user supplies another test string. Separate headline, gradient emphasis, small-label, and reverse-white treatments.

## Prompt construction

For every asset specify:

1. subject and quantity
2. relationship to the reference evidence
3. palette and material
4. light and shadow
5. camera/view
6. background mode
7. framing and margins
8. exclusions

Use the reusable prompt patterns in [prompt-blueprints.md](references/prompt-blueprints.md).

## Output organization

Use this folder structure unless the user specifies another:

```text
<project>_asset_library/
├── 01_backgrounds/
├── 02_atmosphere_transparent/
├── 03_icons/
├── 04_product/
├── 05_typography/
└── manifest.md
```

Use filenames such as `bg_01_warm_gradient.png`, `atm_02_light_streak.png`, `icon_03_study_timer.png`, and `product_01_pad_45deg.png`.

Create `manifest.md` containing:

- reference analysis
- shared brand anchor
- one row per asset
- evidence level
- view/background mode
- prompt summary and negatives
- transparency status
- final file path
- QA notes and known limitations

## Validation and retry

Check:

- each file contains only the intended asset
- no source-poster layout has been reproduced
- silhouettes are complete and uncropped
- icon style is consistent
- product views are honestly labeled
- typography test text is correct enough for a visual specimen
- transparent assets pass the alpha checks in [transparency.md](references/transparency.md)

If an output fails, revise only the failing constraint and regenerate that asset. Never label an opaque PNG, checkerboard image, or chroma-key source as transparent.

## User communication

Lead with what was created. State asset counts by system and link the library and manifest. Explicitly disclose any transparency fallback, geometry drift, or text-generation limitation.
