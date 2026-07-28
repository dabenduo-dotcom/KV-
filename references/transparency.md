# Transparent PNG standard

## Goal

Deliver a real PNG with an alpha channel, not an image that visually depicts transparency.

## Required prompt language

Include all relevant clauses:

> Isolated single asset on a true transparent RGBA canvas. Pixels outside the subject are fully transparent (alpha 0). Preserve physically plausible partial alpha inside translucent glass, clear plastic, liquid, mist, glow, and soft edges. No background, no floor, no horizon, no backdrop, no matte, no shadow plate, no checkerboard, no grid, no mosaic, and no pattern representing transparency. Export as a PNG with a real alpha channel.

For opaque cutouts, request a complete silhouette with clean anti-aliased edges and generous transparent margins.

For transparent materials, distinguish:

- **outside the object**: fully transparent
- **solid rims and labels**: opaque where physically appropriate
- **glass, liquid, mist, glow, refraction**: partially transparent, not erased

## Verification

1. Inspect the rendered image. Reject any visible checkerboard, gray-white grid, mosaic, studio background, floor, or rectangular matte.
2. Check metadata for an alpha channel with a non-mutating inspection tool such as `sips -g hasAlpha <file>` on macOS.
3. Treat `hasAlpha: no` as failure.
4. Even when alpha exists, inspect whether the outside canvas is actually transparent and whether translucent internal regions remain usable.
5. Record `true alpha`, `opaque`, or `fallback` in the manifest.

## Retry sequence

1. Retry with the full required prompt language above.
2. Reduce the scene to one centered subject and remove all environmental lighting descriptions that imply a backdrop or floor.
3. Replace cast shadows with internal contact shading only, or remove shadows completely.
4. If the generator still cannot produce usable alpha, tell the user. Ask before generating a flat chroma-key fallback.

## Fallback rules

Use chroma key only with user acceptance. Choose a flat color absent from the subject, keep it uniform, and label filenames with `_greenkey`, `_bluekey`, or `_chromakey`. Never call it transparent PNG. Do not use a checkerboard as a fallback.

Do not remove backgrounds with scripts when the user requires image-generation-only output.

