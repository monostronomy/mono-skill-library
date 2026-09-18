---
name: layered-photoshop
license: MIT
description: >-
  Create layered Photoshop documents from existing images or new layer-first
  artwork. Use when asked to separate, explode, or decompose an image into PSD
  layers; generate separate transparent components; or rebuild typography as
  editable text. Preserve source fidelity, disclose reconstruction, and validate
  the actual layers. Do not use for a simple flattened-image export.
compatibility: >-
  Requires a tool-enabled agent with image inspection and file access. Producing
  PSDs additionally requires suitable extraction or generation tools and a
  compatible PSD writer; none are bundled. Use desktop Photoshop for native
  validation.
metadata:
  version: "0.1.2"
  maturity: "instruction-only draft"
  validation: "general workflow not yet validated"
---

# Create layered Photoshop documents

## Establish the operating contract

1. Treat this package as reusable workflow instructions and reference material, not as an image generator, PSD export executable, or installation of an external service. Use `README.md` and `PROMPTS.md` as optional human-facing material when present; do not require them for execution.
2. Verify that the current environment supplies the image-generation, selection/matting, file-processing, typography, PSD-writing, and inspection tools needed for the requested mode. Follow the host's tool-routing, permissions, privacy, and content requirements.
3. Preserve original inputs. Write new outputs to a distinct destination; obtain permission before overwriting originals or uploading sensitive images to a new external service.
4. Inspect the actual supplied image before editing it. Request a usable attachment when an editing target is absent; do not invent a source from its name or from conversational memory.
5. Route an existing flattened image to `decompose`; route a request for new artwork to `generate-layer-first`. Combine these routes only when the user requests a hybrid, and label the origin of each resulting layer.
6. Identify the intended edits: moving whole objects, changing backgrounds, animating body parts, recoloring materials, editing typography, or modifying individual effects. Choose layer granularity for those edits rather than maximizing the layer count.
7. Record canvas dimensions, orientation, color profile, bit depth, intended Photoshop compatibility, text requirements, background behavior, reconstruction permission, and generation/retry budget in a job manifest. Use `assets/job-manifest.example.json` as an optional starting structure when present; otherwise create a manifest containing these fields. Replace every example value with the current job's values, and do not treat a template as a finished job.
8. Default a source-image job to source-preserving visible-surface extraction, with the source dimensions and profile retained where the export backend supports them. Disclose required conversions instead of silently reducing resolution, changing color mode, or reducing bit depth.
9. Default a new general-purpose screen-art job to RGB, 8 bits per channel, and an explicit sRGB profile unless the brief specifies otherwise. Confirm requirements for print, HDR, large-document, or other unsupported export cases.
10. Add a separate background layer with the requested color and visibility. Keep foreground layers transparent independently of whether the background is visible. Choose dimensions, background, fonts, and component counts from the current input and brief, never from another project. Use the requested output name or a neutral default such as `artwork.psd`; derive asset names from the current components.

## Plan the layer structure

1. Create a named layer inventory before expensive work. Record each component's purpose, stacking position, bounds or transform, extraction/generation method, mask, opacity, blend mode, and occlusion dependencies.
2. Group components by editing purpose: environment, subjects, props, graphic elements, typography, effects, and reference material. Use only groups appropriate to the image.
3. Identify text that must remain native editable text and text-like artwork that must remain raster or vector artwork. Preserve an original raster reference when reconstructing lettering.
4. Mark difficult boundaries such as hair, fur, glass, smoke, motion blur, reflective surfaces, shadows, and interpenetrating objects before committing to a separation method.
5. Explain any consequential tradeoff between matching the original, making components movable, and inventing missing surfaces. Proceed on the conservative route unless the user authorizes reconstruction.
6. Reserve the original flattened image for a hidden reference group. Never use a visible full-image layer to conceal failed component separation.

## Execute the selected workflow

1. Read `references/decompose.md` and apply its source-fidelity rules for existing artwork, photographs, scans, screenshots, or flattened composites.
2. Read `references/generate-layer-first.md` and apply its asset-production rules for new artwork. Use the available image-generation tool for image-generation tasks rather than substituting a text-only description of the desired outputs.
3. Read `references/export-and-validation.md` before selecting a PSD writer or assembling the document. Reuse a pinned, tested implementation instead of improvising binary serialization on each job.
4. Read `references/sources.md` when verifying tool support or file-format behavior; refresh time-sensitive capability claims before relying on them.
5. Report only the input categories, exporter features, and application behavior established by actual evidence. Treat untested capabilities as unvalidated; do not require a historical project, prior conversation, or maintenance test plan to run a new job.

## Deliver and report evidence

1. Deliver a layered PSD when a compatible export path exists. Otherwise report the unavailable dependency and provide only the deliverables actually created; never rename an ordinary image to `.psd` or imply that instructions alone completed an export.
2. Include a composite preview rendered from the actual visible layers, a layer manifest, font names and substitutions, reconstruction notes, and a validation report. Use `assets/validation-report.template.json` when present, or record the same per-job checks and evidence in a new report.
3. Include separate transparent assets and masks when requested or needed for recovery. Keep masks separately editable in the PSD when supported; disclose when alpha cutouts have masks permanently applied.
4. Preserve native editable text where promised. Disclose individually positioned character layers, raster effect overlays, font substitutions, and unavailable text-on-path support.
5. Check file existence and report only verified output paths. Distinguish archive integrity, structural PSD checks, independent decoding, visual compositing checks, native Photoshop opening, and native editing/save/reopen checks.
6. State which checks passed, failed, or were not run. Never infer Photoshop compatibility from a readable embedded preview, correct extension, plausible file size, or correct layer count alone.
7. Record the exact successful artifact hash, writer/dependency version, Photoshop version and operating system when known, plus the actions actually tested. Keep unknown fields explicitly unknown.
8. Add confirmed defects and regression cases to the skill without embedding image-specific coordinates or text into the general workflow.
