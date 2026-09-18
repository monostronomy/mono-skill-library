# Separate an existing image

## Inspect and classify the input

1. Inspect the actual file type, dimensions, orientation, profile, bit depth, and existing alpha data before processing.
2. Prefer original editable files, vectors, or existing layers when the user supplies them; avoid flattening useful structure merely to recreate it.
3. Treat photographs, scans, paintings, screenshots, and generated images as supported source categories only where the available decoder and processing tools can handle their formats. Base method selection on visual content and the requested edit, not on whether AI created the source.
4. Inventory meaningful subjects, props, background regions, lettering, graphics, and optical effects. Distinguish tightly connected structures from independently movable objects.
5. Choose a target fidelity contract: preserve the supplied composition, create movable complete components through authorized reconstruction, or explicitly combine both in separate groups.

## Preserve visible source pixels by default

1. Extract source-derived components using selections and non-destructive layer masks wherever possible. Retain original source pixels under the mask when the exporter supports them.
2. Refine edges at the final working resolution. Inspect soft and hard boundaries separately; avoid converting every edge to the same binary cutout or applying indiscriminate feathering.
3. Inspect each isolated component against light and dark backgrounds. Check for clipped details, colored fringes, opaque rectangles, residual background pixels, and duplicate edge coverage.
4. Preserve scene-dependent effects in their original group when independent physical separation cannot be justified. Do not claim that a mask alone recovers glass transmission, refraction, reflections, or light contributions.
5. Preserve photographic faces, product labels, and identifying shapes during source-faithful extraction. Use generation only when the brief authorizes changing or reconstructing content.
6. Keep unclear tiny glyphs as raster detail unless the user supplies readable source text. Do not invent words and label them transcription.
7. Distinguish pixel-preserving extraction from estimated foreground-color decontamination and reconstructed surfaces; record the latter changes.

## Handle occlusion and missing information

1. Mark visible-only cutouts as `complete_object: false` when portions are obscured or cropped by the source.
2. Explain that moving these cutouts may expose gaps or stale interactions in the underlying scene.
3. Request authorization before creating unseen anatomy, hidden object surfaces, a clean background behind a subject, or replacement textures under removed lettering, unless the existing brief explicitly authorizes that reconstruction.
4. When reconstruction is authorized, retain the extracted source in one group and put invented completions or clean-plate repairs in separately named layers or groups.
5. Label completions as generated or reconstructed rather than recovered originals. Preserve the original source for comparison.
6. Reassess shadows, reflections, perspective, and contacts when objects are moved. Do not promise arbitrary recomposition merely because the original stack can be reconstructed.

## Rebuild requested typography

1. Transcribe readable text accurately and resolve uncertainty before making a supposedly exact replacement.
2. Choose fonts according to letterforms, width, weight, style, and the document's purpose. Record the selected PostScript names, fallback names, and whether identification is verified or the font is a visual substitute.
3. Create native type layers for text that must be edited. Preserve raster or vector treatment for lettering explicitly exempted by the user.
4. Keep original lettering in a hidden comparison layer. Remove or cover its baked-in source pixels only through a disclosed, authorized local surface reconstruction.
5. Use a native text-on-path implementation when continuous curved text editing is required and the backend supports it. Otherwise disclose a per-character layout or alternative instead of presenting it as equivalent.
6. Treat scripts requiring contextual shaping, bidirectional layout, combining characters, or non-Latin glyph coverage as separate compatibility cases; avoid splitting shaped text into isolated characters.
7. Put non-native bevel, chrome, glow, or texture treatments on clearly named effect layers when necessary; explain which effects will not update automatically after editing the text.
8. Provide font names and acquisition/activation information when appropriate, but do not package font binaries.

## Verify fidelity honestly

1. Recompose the document from its actual layers with the reference layer hidden.
2. Compare the recomposed pixels against the intended target. Use exact equality only when the extraction and rendering contract actually permits it; account for alpha blending, color conversion, and intentional typography or cleanup changes.
3. Record intentionally altered regions separately rather than hiding their difference in a single overall similarity score.
4. Toggle and move representative components to expose duplicate pixels, missing regions, mask-linkage problems, or interactions that remain baked into neighboring layers.
5. Deliver partial separations with clear scope when the source does not support a faithful full decomposition; preserve useful work rather than silently replacing the source with a newly generated interpretation.

## Ground the limits

Consult sources S5 and S6 in `sources.md` for PSD structure and the ambiguity of foreground/alpha recovery from a single flattened image. Use the source's own pixels as evidence of appearance; do not treat inferred hidden content as observed information.
