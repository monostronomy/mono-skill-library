# Create new artwork as layers from the start

## Establish the composition before generating final assets

1. Read the creative brief and identify every element that must be moved, recolored, hidden, or edited independently.
2. Define a shared canvas, camera angle, perspective, scale, palette, lighting direction, light softness, material treatment, and visual style.
3. Build a layout specification with stacking order, approximate bounds, and alignment anchors. Use a mockup as a composition reference when useful; do not treat a flattened mockup as the final layered deliverable.
4. Reuse the same accepted references and asset descriptions across related generations. Inspect identity and geometry rather than assuming repeated prompts guarantee consistency.
5. Budget generation calls and retries. Generate coarse layout assets first when appropriate; avoid spending final-quality effort on a composition that has not been checked.
6. Create geometric frames, ordinary typography, and simple graphic elements natively when that better supports editing than image generation.

## Generate independent components

1. Generate each required independently editable visual component as a separate asset, or use a tool that explicitly returns independently addressable layered assets and validate those outputs.
2. Request real alpha transparency for foreground assets, and enable the tool's actual transparency setting where available. Use an alpha-capable lossless output workflow, ordinarily PNG.
3. Reject a painted checkerboard, white backdrop, black backdrop, or montage of parts as a substitute for actual transparency and separate assets.
4. Preserve the returned alpha channel during downloads, resizing, color management, and assembly.
5. Generate sufficient object extent and overlap margin for the intended edits, including complete hidden portions when the creative brief calls for movable objects. Do not crop a hand or prop merely because it is hidden in the initial arrangement.
6. Generate a separate background or clean scene plate without the foreground objects when needed.
7. Keep contact shadows, cast shadows, reflections, and emissive glows separate when independent editing requires them. Specify their blend modes and dependent objects; avoid claiming that separation makes those interactions correct after arbitrary movement.
8. Preserve intended semi-transparency inside smoke, mist, and similar components when possible. Treat complex refraction and background-dependent glass appearance as an explicit limitation or a candidate for a different rendering method.
9. Create readable design copy as native type during assembly rather than baking it into generated assets. Keep explicitly requested sculpted or illustrative lettering as artwork and note the exception.

## Enforce alignment and coherence

1. Store every component in a common coordinate system: use full-canvas assets, or preserve cropped dimensions together with exact placement offsets and transforms.
2. Inspect the actual generated bounds and anchors. Correct placement deterministically during assembly rather than trusting the generator to hit exact pixel coordinates.
3. Compare subject identity, perspective, lighting, scale, edge quality, and depth relationships across all components.
4. Reuse accepted assets when revising the scene. Regenerate only the affected component when possible, retaining its target bounds and references.
5. Reassess object contacts and light interactions after any replacement or move.
6. Keep adjustments as native adjustment layers or separate editable effects when supported; otherwise document any baked corrections at the asset level.
7. Avoid a final generative repaint of the complete composite when it would no longer match the independent layers. Apply the needed correction to components and rebuild the composite instead.

## Assemble and report

1. Assemble the assets, native graphics, and native text using the common export and validation workflow.
2. Render the deliverable preview from the assembled layer stack rather than generating an unrelated finished illustration.
3. Provide transparent assets with a manifest when requested; include the separate background as its own asset or fill layer.
4. Report which components were generated, drawn natively, extracted from supplied sources, or reconstructed.
5. State that layer-first production avoids recovering layers from a final flattened scene, but still requires coherence and compositing review.

## Ground the capabilities

Consult sources S2 and S3 in `sources.md` for current transparency support and documented consistency/composition limitations. Recheck the active tool's contract: PNG alpha output is not itself a Photoshop layer tree, and model-specific output formats may differ.
