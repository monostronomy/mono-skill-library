# Layered Photoshop

**Turn a finished image into useful editable components—or build new artwork from independent components before it is flattened.**

`layered-photoshop` is a reusable workflow skill for tool-enabled AI agents. It covers photographs, scans, illustrations, graphic compositions, and generated imagery. Its purpose is to produce a thoughtfully organized Photoshop document whose layers correspond to things a person actually needs to edit.

**Version:** 0.1.2 · **Status:** instruction-only draft · **Documentation checked:** September 18, 2026

> **Know what is included.** This package contains instructions, references, prompts, and planning/test templates. It does not bundle an image model, segmentation engine, general PSD writer, or Photoshop automation program. An agent needs suitable tools outside this package to produce the actual artwork and PSD. The general workflow has not yet been validated across source categories and exporter features; keep per-job test evidence separate from the skill's documentation status.

## Contents

[Quick start](#quick-start) · [Two workflows](#choose-a-workflow) · [Best use cases](#best-use-cases) · [Requirements](#requirements) · [Decomposition](#separate-an-existing-image) · [Layer-first generation](#create-new-artwork-layer-first) · [Text](#handle-text-and-fonts) · [Deliverables](#expected-deliverables) · [Validation](#validate-the-deliverable) · [Evidence](#evidence-and-current-status) · [Troubleshooting](#troubleshooting) · [FAQ](#frequently-asked-questions)

## Quick start

1. Install or load the `layered-photoshop` folder in a compatible agent. Preserve `SKILL.md` and the four files under `references/`. Use the complete folder for convenience, or follow the optional-file guidance below for a smaller installation.
2. Provide an actual source image for decomposition, or a creative brief for new artwork.
3. Explain what you need to change later: wording, background, object placement, character parts, color, or effects.
4. Choose source-preserving extraction or authorize specific reconstruction. Set canvas requirements and background behavior.
5. Ask the agent to verify its tools and propose the layer breakdown before substantial work.
6. Review the PSD, the preview rendered from its layers, and the validation notes together.

For local hosts, copy this folder under `.agents/skills/` for Codex or `.claude/skills/` for Claude Code. Refer to their current [Codex][codex] and [Claude Code][claude] installation instructions. In an ordinary tool-enabled chat, supply the files and a prompt explicitly rather than assuming the skill name installs them.

Start with this source-image brief:

```text
Use the layered-photoshop workflow on the attached image. Separate the main
subject, foreground objects, background, and readable typography according
to what can be edited independently. Preserve the source pixels wherever
possible. Ask before inventing hidden content or cleaning surfaces beneath
text. Keep the original in a hidden reference group. Deliver a layered PSD,
an actual-layer preview, and a report of what was reconstructed and tested.
```

Or start with this new-art brief:

```text
Use the layered-photoshop workflow to create a layer-first illustration of
[scene]. Plan and produce the background, [subject], [props], [effects], and
[title] separately. Use real transparency for foreground assets and native
editable text for the title. Assemble the components into a layered PSD;
do not substitute a single generated final image. Check the available tools
and the proposed layer plan before spending the generation budget.
```

Find longer task briefs and host-specific invocation examples in [PROMPTS.md](PROMPTS.md).

## Keep execution files separate from optional material

Use the following boundary when installing or maintaining the skill:

| Files | Role | Needed for ordinary execution? |
|---|---|---|
| `LICENSE` | MIT terms and copyright notice | Include in every distribution. |
| `SKILL.md` | Entry point, routing, source protection, layer planning, and delivery requirements | Yes. |
| `references/decompose.md` | Source-preserving separation and typography procedure | Yes for decomposition; keep it in the two-mode distribution. |
| `references/generate-layer-first.md` | Independent asset generation and assembly procedure | Yes for layer-first work; keep it in the two-mode distribution. |
| `references/export-and-validation.md` | Shared export checks, failure prevention, and evidence reporting | Yes. |
| `references/sources.md` | Technical sources referenced by the operating procedures | Keep it with the procedures; consult it when verification is needed. |
| `assets/*.json` | Generic planning/report templates, not artwork or an exporter | Optional helpers; the instructions provide a fallback when absent. |
| `tests/acceptance-cases.md` | Proposed maintenance and scope-expansion checks | Optional for execution; keep it in the development repository. |
| `README.md`, `PROMPTS.md`, `CHANGELOG.md` | Human guidance, task briefs, and release history | Optional at runtime; recommended in the public repository. |
| `agents/openai.yaml` | Optional host presentation metadata | Use only when the target host supports it. |

Keep this minimal execution layout when preparing a smaller two-mode distribution:

```text
layered-photoshop/
├── SKILL.md
├── LICENSE
└── references/
    ├── decompose.md
    ├── generate-layer-first.md
    ├── export-and-validation.md
    └── sources.md
```

Use ordinary neutral paths such as `input/source.png`, `output/artwork.psd`, and `assets/subject.png` as examples only. Replace them with the current source, destination, and component names. Take dimensions, fonts, component counts, and background settings from the current job, not from a previous example.

Store project logs, client-specific output names, artifact hashes, and image-specific test results with that job or in separate authorized development records. Do not require them for skill execution. Keep generic export lessons in the shared validation procedure instead of asking future users to reproduce one image's repair history.

### Update an older installation

1. Preserve any local customizations before changing the installed skill.
2. Replace the old skill directory with this revision rather than merging files blindly; merging can leave removed references behind.
3. Confirm that the `references/` directory contains only the four files shown above and that the header reports version `0.1.2`.
4. Keep optional templates and maintenance tests when useful, or omit them according to the table above.

## Choose a workflow

The skill has **two production modes and one shared assembly/validation process**.

| Mode | Start with | Aim for | Main tradeoff |
|---|---|---|---|
| `decompose` | An existing flat photograph, scan, illustration, or composite | Source-derived components, editable masks where supported, reconstructed type, and a layered PSD | Preserve visible information without pretending to recover hidden information. |
| `generate-layer-first` | A concept, layout, or creative brief | Separately created assets, native text/graphics, and an assembled PSD | Keep separately produced assets consistent in lighting, scale, perspective, and identity. |

A hybrid job can use both—for example, a supplied product photograph in a newly generated scene. Record which layers came from the source, which were generated, and which were drawn or created natively.

### Choose the amount of reconstruction

**Source-preserving separation** keeps the visible components as faithfully as practical. It is appropriate when the original appearance matters more than rearranging the scene. A cutout may contain only the portion of an object that was visible.

**Editable reconstruction** adds requested missing surfaces or removes baked-in text from underlying plates. It is appropriate when an object must move or wording must change. Those additions are newly constructed content, not recovered source evidence.

**Layer-first creation** produces the components deliberately for a new composition. It avoids trying to discover an original layer stack after flattening, but still requires careful assembly.

The agent should not silently switch from the first contract to the second simply because a complete object would be more convenient.

## Best use cases

The cases below are recommended starting points based on the editing goals and visible structure. They are **not measured performance claims** for this draft.

| Use case | Useful independent components | Why use this workflow? | Watch for |
|---|---|---|---|
| Logos, badges, emblems, and channel graphics | Main symbol, frame, lettering, decorative marks, light accents | Revise wording, isolate the symbol, or adapt the layout without rebuilding every part. | Custom lettering may be artwork rather than ordinary type. |
| Posters, thumbnails, and promotional composites | Subject, background, title, supporting copy, framing, effects | Reuse a design with different copy or proportions. | Removing original text may require repairing the surface underneath it. |
| Product photographs | Product, background, contact shadow, optional copy | Reuse the product in a new layout while preserving its appearance. | Packaging text, reflections, and edge colors should not drift through generative repainting. |
| Scanned illustrations and traditional artwork | Main figures, selected foreground detail, paper/background, readable lettering | Prepare selective edits or motion without treating the entire scan as one unit. | Fine linework and paper texture can cross component boundaries. |
| Character illustrations and scene assets | Character, props, selected body parts, foreground effects | Make targeted revisions or prepare assets for later motion work. | Separation alone does not create a rig, joint geometry, or complete hidden anatomy. |
| New layered key art or environment illustrations | Background, main subject, props, foreground, atmosphere, title | Plan a composition whose important assets can be reused or replaced. | Independently generated parts need a shared visual specification. |
| Interface-like graphics and holographic compositions | Panels, frames, readable labels, icons, effects | Edit panel content and text separately from surrounding artwork. | Transparency and reflected backgrounds may already be baked into the source. |

For a first test, use a clear opaque subject or a graphic with distinct major parts. Increase difficulty once both the separation method and the export path have been checked.

### Use a different approach when necessary

Choose manual retouching, specialized matting, vector reconstruction, 3D rendering, or another dedicated workflow when the requested output depends on those methods. Do not use a layer count to disguise a mismatch between the task and the available tools.

Dense crowds, fur, smoke, glass, reflections, motion blur, and heavily merged painting strokes require particular care. A flat image does not uniquely determine foreground colors, background colors, and opacity; image-matting research formalizes this ambiguity. [Source: Hou and Liu, *Context-Aware Image Matting*][matting].

For example, separating a person from a chair cannot reveal the chair's covered upholstery. A reconstruction can propose it, but cannot certify what the original chair looked like there.

## Requirements

### Check the toolchain, not just the skill name

| Capability | Needed for | Included here? |
|---|---|---|
| Agent that can read skill/support files and inspect images | Both modes | No; supplied by the host. |
| Selection, masking, matting, and image-file processing | Existing-image decomposition | No. |
| Generation of separate assets and alpha-capable output | New layer-first artwork | No. |
| Native type creation or a PSD writer with tested type support | Promised editable text | No. |
| PSD assembly, asset placement, group/mask handling, and decoding | PSD delivery | No general implementation is bundled. |
| Desktop Photoshop in the intended environment | Native opening and edit/save/reopen tests | No. |
| Workflow instructions, references, prompts, and templates | Planning and execution guidance | Yes. |

Tools may be local, connected services, or an approved combination. Their presence, permissions, licensing, network access, and supported features must be checked for each environment. The skill does not specify an installed backend that it does not supply.

Photoshop has native text-creation APIs, but an external exporter must implement the relevant records correctly; writing pixels that look like text is not the same capability. Consult Adobe's [native type options][adobe-type] and [PSD format specification][psd-spec] when implementing that part of the workflow.

### Provide a useful brief

Provide the source or scene description, desired dimensions, output color requirements, important editing targets, required text, and background preference. Identify a target Photoshop version when one matters. State whether the objects must remain in their original positions or be complete enough for movement.

Set an approval boundary for paid calls and retries. Include a maximum budget when the host uses metered services. More parts, difficult masks, and regeneration can increase work; this draft makes no fixed cost or turnaround promise.

Keep inputs unchanged and write outputs to a new destination. Authorize external processing of private material only after understanding which service will receive it.

## Separate an existing image

Use [the decomposition procedure](references/decompose.md) for the full operating instructions.

### 1. Inspect the source and choose meaningful components

Identify the visible objects, overlapping regions, readable text, effects, and fine boundaries. Decide what each layer will allow the user to do.

Keep a character on one layer when only the background must change. Separate its eyes or hand when those parts actually need independent editing. Avoid dividing an image into arbitrary rectangles or hundreds of fragments that make ordinary work harder.

### 2. Preserve pixels and create masks

Extract source-derived components through masks where the toolchain supports that approach. Preserve the original raster in a hidden reference group. Inspect edges against contrasting backgrounds, not only against the original scene.

Document whether a layer uses an editable mask or an already-applied alpha cutout. An applied cutout can be useful, but it does not retain the same editable boundary information and underlying pixels as a mask-backed layer.

### 3. Handle overlap and background cleanup explicitly

Mark objects that are visible-only. When a foreground object moves, its previous footprint can expose missing background or missing parts of another object. Obtain approval before filling those areas.

Removing old typography has a related consequence: new editable type does not erase the original baked-in letters beneath it. Either authorize surface cleanup, keep the original lettering as artwork, or accept the stated limitation. Keep reconstructed plates separately identifiable.

### 4. Rebuild text and assemble the layers

Apply the agreed typography policy. Position components using recorded bounds and transforms, organize groups by editing purpose, and set background visibility explicitly. Reconstruct the original visible arrangement as the initial state unless the brief requests a redesign.

### 5. Compare the actual result

Render the preview from the visible layer stack. Compare it with the source, accounting for explicitly requested changes such as replacement type or cleaned surfaces. Investigate unapproved missing details, duplicated edges, gaps, shifted colors, or effects that have been counted twice.

Do not keep a full-image layer visible simply to make an incomplete separation look correct.

## Create new artwork layer-first

Use [the layer-first procedure](references/generate-layer-first.md) for the full operating instructions.

### 1. Define the scene and layer plan together

Establish the final composition before spending the full production budget. Specify the common camera angle, perspective, light direction, color treatment, scale relationships, and style. Identify which elements need to move, change, or be reused.

A mockup can guide placement, but it is not the requested final deliverable. The actual final composition must be reproducible from the separate assets.

### 2. Produce independent assets

Generate or draw each important component independently. Use native text and simple native geometry when those provide better editability than generated lettering or shapes.

Use real alpha transparency for foreground assets. Where the selected generator supports it, enable its transparency option and preserve an alpha-capable format. OpenAI's image documentation describes transparent PNG/WebP output and also notes continuing consistency and precise-placement limitations. Those capabilities must be checked for the specific model and tool in use. [Source: image-generation documentation][image-generation].

Reject a painted checkerboard as a substitute for alpha. OpenAI's [transparent-asset prompting guidance][image-prompting] makes the same distinction. Inspect the actual file rather than trusting its appearance in a thumbnail.

### 3. Produce enough object extent for the intended edits

Create the whole prop or sufficient hidden extent when it must later move. Give the background a clean plate when subjects may be removed. Keep placement coordinates, crop bounds, and transforms so each asset can return to the right position.

Do not demand unnecessary hidden detail for elements that will never move. Balance the requested editability against generation effort.

### 4. Separate dependent effects deliberately

Keep cast shadows, contact shadows, reflections, and glows separate when they need independent control. Record which object each effect belongs to.

Moving a character does not automatically move its shadow correctly or update a reflection. Glass and refraction are particularly dependent on the scene behind them. Treat these interactions as compositing work, not properties magically restored by a transparent PNG.

### 5. Assemble and review the composition

Inspect scale, identity, lighting, perspective, edge quality, contacts, and depth order across the assets. Reuse accepted components and regenerate only the parts that need changes when practical.

Avoid a final whole-image generative repaint that no longer corresponds to the layers. Correct the relevant assets and render the assembled stack again.

## Handle text and fonts

Specify exact wording and any lettering that must stay artwork. Use native type for ordinary titles, labels, captions, and supporting copy when the chosen backend can preserve it.

Treat decorative, sculpted, distressed, or highly custom letterforms separately. They may remain raster or vector artwork by agreement. A font replacement can provide similar visual character without being the original font.

For each reconstructed text block, record the wording, chosen font family/style, PostScript name where required, size, tracking, color, transform, and any substitution. Record uncertainty rather than inventing unreadable interface glyphs.

Distinguish these outcomes:

| Text result | What the user can reasonably expect |
|---|---|
| Native editable type | Edit the wording through a supported type layer, subject to font availability and tested layout support. |
| Individually positioned character layers | Edit characters individually; do not expect a single flowing phrase or genuine text-on-path behavior. |
| Rasterized lettering | Edit pixels or replace the artwork; do not describe it as native editable text. |
| Vector outlines | Edit paths when supported; do not describe outlines as font-based editable copy. |

Preserve a visual reference before text refresh or font substitution. For curved copy, multiline layout, non-Latin scripts, right-to-left text, or complex typography, verify the specific export implementation rather than assuming complete support. The [ag-psd maintainers][ag-psd], for example, document limitations; it is a possible implementation reference, not a bundled or certified backend.

**Do not include font files in this package or in the generated asset bundle.** Provide font names and acquisition information instead. Confirm the applicable font permissions separately.

## Choose the background and layer organization

Foreground transparency and canvas background visibility are separate settings. A composition can look black because a solid black layer is visible at the bottom while every foreground asset still has transparent surroundings. Hide that layer when exporting a transparent composite.

Use a hierarchy appropriate to the job. This is an illustrative top-to-bottom stack, not a required inventory:

```text
Reference                         [hidden]
Typography                        [native type where promised]
Foreground effects
Foreground objects
Main subjects
Props and supporting elements
Background scene
Solid background                  [requested color and visibility]
```

Keep masks linked appropriately to their layers, distinguish generated completions from source cutouts, and give names that communicate purpose. Record coordinate conventions in the manifest instead of hard-coding one image's size, placement, fonts, or number of layers into the skill.

## Expected deliverables

When the available toolchain can complete the job, request a layered PSD, a preview rendered from the actual layers, and an honest validation report. Request separate transparent assets and masks when they are useful for reuse or recovery.

An example output folder could look like this:

```text
output/
├── artwork.psd
├── composite-preview.png
├── layer-manifest.json
├── validation-report.json
├── editing-notes.md
├── assets/                       # Optional separate components
└── masks/                        # Optional separate masks
```

These are example deliverable names, not files included in this skill. The optional JSON documents in `assets/` are planning/report templates, not an implemented writer API or JSON Schema. Create equivalent manifests and reports from the operating requirements when the templates are absent. Preserve unknown values and unrun tests explicitly.

Include source/construction provenance, font substitutions, incomplete hidden surfaces, baked optical effects, mask limitations, supported color conversions, and the checks actually performed. Deliver only files that exist. Report a blocked export honestly rather than renaming an image to `.psd` or supplying a preview as though it were the layered result.

## Validate the deliverable

Use [the export and validation procedure](references/export-and-validation.md). Keep the following evidence separate rather than collapsing it into one claim of compatibility.

| Check | What it establishes | What it does not establish |
|---|---|---|
| Verify file and archive integrity | The expected bytes and packaged files exist and can be read. | Image quality or Photoshop compatibility. |
| Parse PSD structure and decode channels | The selected parser accepts the structure and decodes the tested data. | Photoshop's behavior for every supported feature. |
| Render the actual layers | The layers produce the reviewed composite rather than only a cached preview. | Native text and mask editing. |
| Inspect visual quality | The image meets the agreed fidelity or design criteria. | Correct binary metadata by itself. |
| Open in the target Photoshop version | That exact artifact opens in that environment. | Editing, refreshing type, saving, or reopening. |
| Edit, save, close, and reopen | The particular tested editing operations survive that native workflow. | All Photoshop versions or all untested features. |

In a native check, change representative text, modify a mask, move a component, and verify group visibility. Save a copy, close it, reopen it, and inspect again. Record any font substitution or changed rendering.

Identify the exact file by its hash and record the writer/dependency version, Photoshop version, operating system, test actions, and evidence source. Mark anything unavailable as not run or unconfirmed.

Treat the original PSD rejection as an engineering lesson: readable previews and plausible layer counts are not sufficient acceptance criteria.

## Evidence and current status

Treat this release as an instruction-only workflow, not as a newly implemented converter or a validated general processing system. Evaluate each active toolchain and each saved artifact on its own evidence.

Record a reported Photoshop open as opening evidence for that exact artifact when identified. Do not infer text editing, mask editing, font refresh, component movement, save/reopen behavior, or support for other images from an opening report alone.

Use `tests/acceptance-cases.md` as an optional maintainer test plan when it is present. The proposed cases cover photographs, difficult boundaries, scans, overlapping objects, new generation, and exporter features; do not describe them as completed results. Apply the per-job validation procedure whether or not the maintenance plan is installed.

## Troubleshooting

| Symptom | Check and act |
|---|---|
| The agent does not discover the skill | Check the installation path, exact `SKILL.md` filename, header, matching folder/name, and host configuration. Keep the complete folder together. |
| The agent can discuss the workflow but produces no files | Ask it to identify the actual processing and export tools. Resolve missing capabilities before further production promises. |
| The PSD is rejected by Photoshop | Preserve the failed file, exact error, writer version, and target environment. Test serialization with small fixtures; consult the exporter procedure instead of repeatedly changing the preview. |
| The preview is correct but layers do not reproduce it | Hide the source/reference image and render the real stack. Investigate missing components, effects, blend modes, and cached text. |
| A foreground asset has a white box or checkerboard | Inspect its alpha channel and pipeline. Re-extract or regenerate real transparency rather than painting over the backdrop. |
| Moving an object reveals gaps | Check whether the job was visible-source-only. Authorize a complete-object/background reconstruction or retain the original placement. |
| Editing text leaves old letters underneath | Inspect the source plate. Approve cleanup or keep the old lettering as artwork; new live type alone cannot remove it. |
| Type shifts after opening | Check missing fonts, substitution, font metrics, transformations, and native text support. Compare with the preserved reference. |
| Separate generated parts do not match | Reconcile camera, lighting, palette, identity, scale, and object contacts using shared references. Revise the affected components. |
| The project needs CMYK, high bit depth, unusual size, or PSB | Verify those requirements against the selected backend before processing. Request approval for any conversion or alternative format. |

## Frequently asked questions

### Does the source have to be AI-generated?

No. The workflow is designed to assess ordinary photographs, scans, illustration, and generated imagery. Source category changes the likely separation method and difficulty, not the need for a layer plan and validation.

### Can it work on any image?

It can assess any image the host can read and propose an appropriate result. It cannot promise perfect recovery of an original layer stack, hidden geometry, fonts, or independent optical components from every flat image. Accepting an input category is different from guaranteeing the requested reconstruction.

### Is this a one-command PSD converter?

Not in this release. It is a reusable procedure for an agent with suitable tools. A self-contained converter needs an implemented and tested processing/export path in addition to these instructions.

### Does opening the PSD prove it is fully editable?

No. Test the specific edits required, then save and reopen. A cached picture of a text layer can look correct even when the underlying text implementation needs further work.

### Can a single image-generation prompt create the whole layered document?

Treat that as tool-dependent. A generator returning one image does not thereby return an editable PSD layer tree. This workflow requests independently addressable assets, then assembles them through a compatible writer. A future tool that returns genuine layers would still need output validation.

### Does a layer-first PSD automatically become animation-ready?

No. State the animation requirements in advance. Complete objects, pivots, joint overlap, naming, and rigging are additional requirements, not consequences of having many layers.

### Can the result be pixel-identical to the source?

Set the desired tolerance before work. Source-only extraction can target a very close recomposition, while font replacement and approved reconstruction intentionally change pixels. Complex transparency, overlapping effects, and imperfect boundaries may prevent an exact match. Report the actual comparison result.

### Does this recover vectors or 3D data?

Not automatically. Native shape construction and vector tracing are separate methods. A PSD assembled from raster components is not a recovered 3D scene, vector master, or render-pass archive.

### How much will a job cost or how long will it take?

No fixed figure has been validated. Set a budget and stop conditions based on the active tools, asset count, mask difficulty, text work, retries, and native testing. Start with a small representative proof of the actual workflow.

## Develop the skill further

1. Recover or implement a reusable PSD assembly backend and pin its dependencies.
2. Drive dimensions, placement, masks, fonts, and grouping from a manifest rather than project-specific constants.
3. Add small exporter fixtures before relying on complex art as the only test.
4. Run the proposed visual cases and native Photoshop editing checks.
5. Publish the tested scope and unresolved failures without treating a finite test set as proof of universal recovery.

Read [SKILL.md](SKILL.md) for agent instructions, [PROMPTS.md](PROMPTS.md) for task briefs, [CHANGELOG.md](CHANGELOG.md) for release changes, and [references/sources.md](references/sources.md) for primary technical sources.

## License and asset rights

Original material in this skill is available under the [MIT License](LICENSE), copyright (c) 2026 monostronomy, to the extent the contributors hold the applicable rights. Include this license and its notices in standalone distributions, including minimal packages. Identify third-party material separately and retain its applicable terms.

Independent artwork does not become MIT-licensed merely by using this workflow; repository material copied into an output remains subject to its applicable license. Keep image rights, third-party assets, font permissions, and service terms separate. Do not publish private client inputs or font binaries as test fixtures.

[codex]: https://developers.openai.com/codex/skills/
[claude]: https://code.claude.com/docs/en/skills
[matting]: https://arxiv.org/abs/1909.09725
[adobe-type]: https://developer.adobe.com/photoshop/uxp/ps_reference/objects/createoptions/textlayercreateoptions/
[psd-spec]: https://www.adobe.com/devnet-apps/photoshop/fileformatashtml/
[image-generation]: https://developers.openai.com/api/docs/guides/image-generation
[image-prompting]: https://developers.openai.com/api/docs/guides/image-prompting
[ag-psd]: https://github.com/Agamnentzar/ag-psd
