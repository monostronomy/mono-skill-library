# Expand the tested scope

Use this file for maintenance and planned scope-expansion testing, not as a prerequisite for ordinary image jobs. Treat it as a proposed test plan, not as completed test results or a statistical certification. Apply the per-job checks in `references/export-and-validation.md`, relative to the skill root, during production.

## Exercise varied content

1. Separate a non-generated product photograph with clean opaque edges; verify source fidelity and alpha edges against white and black backgrounds.
2. Separate a non-generated portrait or animal photo with fine hair or fur; inspect foreground color contamination, small gaps, and soft boundaries.
3. Separate a cluttered scene with overlapping objects; verify visible-only labels and ensure unapproved hidden content is not invented.
4. Separate a scene with glass, smoke, motion blur, or reflections; verify that the workflow flags optical dependencies instead of calling binary cutouts physically independent.
5. Separate a scanned illustration or poster with fine linework and typography; check text transcription, local cleanup disclosure, line retention, and requested live type.
6. Produce a new illustration layer-first with several interacting subjects or props; verify consistent scale/perspective, genuine alpha assets, separate typography, and a composite built from those assets.

## Exercise exporter features independently

1. Export tiny synthetic fixtures covering nested groups, off-canvas pixels, masks, hidden layers, normal and supported non-normal blending, empty groups, and unique IDs.
2. Export text fixtures covering multiline text, transformations, missing fonts, curved text, combining marks, non-Latin shaping, and right-to-left layout as supported; flag unsupported features before export.
3. Test boundary cases for format, dimensions, memory use, bit depth, profiles, and file size without silently converting unsupported requests.
4. Open the exact fixtures in each Photoshop version claimed as supported; test edit, save, close, and reopen rather than opening alone.
5. Change a writer dependency only after rerunning the relevant fixtures and retaining output identities.

## Check skill behavior

1. Trigger decomposition for a photograph, a scan, or generated source without assuming the image's origin.
2. Trigger layer-first generation for a new-art brief rather than producing a single flattened final image.
3. Refuse to claim completed image or PSD processing when a required tool is absent; report the precise missing capability and preserve useful completed outputs.
4. Ask for an actual source when an image-editing target is missing.
5. Keep public-source upload, overwrite, extra-cost, and reconstruction approvals within the host's requirements.
6. Record success separately for native opening, native editing, and visual quality. Avoid treating any finite set of examples as proof of perfect recovery for every image.
