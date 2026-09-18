# Assemble and validate a Photoshop deliverable

## Select the backend

1. Inspect the active tool schemas and local dependencies before promising native PSD output. Distinguish an image-editing integration from a PSD document/layer-writing capability.
2. Prefer an already tested writer with a pinned version for the required feature subset. Use Photoshop's own document, layer, type, and save APIs when available and appropriate; follow the host's execution and authorization requirements.
3. Keep a desktop-native rebuild as an optional recovery route, not as proof that the primary export works or as an automatic requirement for the user.
4. Check backend support for masks, groups, blend modes, live typography, curved text, profiles, bit depths, and document size. Choose a supported alternative or disclose scope reductions when needed.
5. Treat PSD and PSB as different formats. Check both pixel-dimension and file-size constraints and backend limits before export; do not fix an unsupported format by changing the extension.
6. Avoid claiming that a general-purpose PSD library supports every Photoshop feature. For example, consult the current ag-psd limitation list before choosing it for complex text, non-RGB modes, higher bit depth, or PSB.

## Keep assembly deterministic

1. Read canvas settings, asset paths, offsets/transforms, group membership, masks, text, fonts, opacity, blend modes, and output paths from the manifest.
2. Replace project-specific dimensions, font conditionals, and expected layer counts with parameters and manifest-derived checks.
3. Validate all asset paths and prevent path traversal outside the authorized working directory. Avoid executing downloaded scripts or treating manifest values as executable code.
4. Preserve actual source images separately from masks where supported. Link masks and layers for intended movement, and preserve hidden/reference visibility correctly.
5. Generate unique layer IDs and stable descriptive names. Validate balanced nested groups and the serializer's required record order.
6. Keep binary format details inside tested code, not in free-form generation at each invocation. Test alignment, declared lengths, signatures, channel bounds, compression payloads, and type descriptors when maintaining a custom writer.
7. Distinguish the PSD header version, `TySh` structure version, text-data version, and optional `lyvr` layer version. Consult Adobe's specification before changing any version value; do not globally set these different fields to the same number.
8. Populate an accurate merged preview and any necessary layer caches. Do not mistake cached raster text for editable type data.
9. Preserve explicit color profiles and record conversions. Avoid silent changes of canvas size, orientation, channel depth, or profile.

## Prevent recurring export failures

1. Test nested group ordering and empty group records against the selected writer's expected structure; derive counts from the current manifest.
2. Check additional-information block lengths, padding, alignment, and optional metadata against the applicable format specification before modifying a serializer.
3. Keep distinct version fields separate and verify each field's meaning; do not copy a numeric repair from another file without understanding the relevant record.
4. Decode compressed layer and mask channels and compare their contents with the current source assets, not only with an embedded composite.
5. Distinguish an editable mask with preserved underlying pixels from a transparent cutout with its mask already applied; disclose any change of representation in a fallback.
6. Record multiple repair changes without claiming that one isolated cause has been proven unless a controlled reproduction establishes it.
7. Parameterize any reused builder's paths, dimensions, fonts, placement, groups, and expected counts before applying it to another job.
8. Record new failures in separate, authorized maintenance fixtures; never make a previous user's image, filename, conversation, or artifact hash a dependency of ordinary execution.

## Validate in independent stages

1. **Check input/asset integrity:** verify dimensions, coordinate placement, meaningful alpha where expected, asset existence, mask bounds, and font availability.
2. **Check PSD structure:** parse the written file; verify headers, channel payloads, group balance, unique IDs, text contents, mask records, visibility, and expected layer types.
3. **Check rendering:** decode through an independent reader where possible; render the actual visible layer stack with the hidden reference disabled; compare it to the intended composite. Inspect edges on light and dark backgrounds and test the requested blend modes.
4. **Check native opening:** open the exact saved artifact in Photoshop when available; record its filename/hash, Photoshop build, OS, missing-font warnings, repair dialogs, and whether layers remain intact.
5. **Check native editing:** edit representative live text, edit a mask, toggle and move components, save to a new file, close, and reopen. Verify both resulting appearance and retained editability.
6. Mark unavailable checks as `not_run`; mark user-reported checks as such. Keep successful native opening separate from editing and save/reopen validation.
7. Derive expected counts from the manifest. Include reference, hidden, text, group, fill, and effect layers in clearly defined categories; avoid ambiguous totals.
8. Add each defect to a repeatable regression test before upgrading dependencies or refactoring the exporter.

## Handle typography faithfully

1. Resolve actual installed font/PostScript names or expose a clear substitution report. Avoid silently selecting a default font.
2. Verify native glyph rendering after text refresh. Keep cached text and preview comparisons distinct from Photoshop-rendered text validation.
3. Test Unicode, shaping, multiline text, transformations, missing fonts, and text-on-path as separate feature cases.
4. Disclose when character-by-character curved text is editable only per character, or when a raster effect must be rebuilt after copy changes.
5. Preserve the original layered file when testing text refresh or substitution; save experiments to new files.

## Deliver evidence, not a blanket guarantee

1. Record the artifact identity, source category, writer/version, manifest-derived layer counts, checks, evidence, exceptions, and native environment in a validation report. Use `assets/validation-report.template.json`, relative to the skill root, when available; otherwise create the report from these requirements.
2. Include the layer manifest, font report, and provenance labels with the PSD and preview.
3. State whether a failure concerns export structure, text rendering, source separation, compositing, or an unavailable feature; avoid treating all failures as Photoshop-version incompatibility.
4. Preserve the exact tested output as a regression fixture and avoid attributing success to an untested repair variant.

Consult sources S4, S5, S7, and S8 in `sources.md` for native Photoshop APIs, binary-format details, and writer limitations.
