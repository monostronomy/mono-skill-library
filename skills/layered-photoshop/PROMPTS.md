# Request a layered Photoshop project

## Separate an existing image

> Convert the attached image into a layered Photoshop document. Separate components according to what can be meaningfully edited independently, rather than producing rectangular crops or maximizing the layer count.
>
> Preserve the source appearance, dimensions, and color profile wherever supported. Keep source-derived pixels under editable masks. Keep the original flattened image in a hidden reference group. Preserve the visible composition; do not regenerate the source or invent obscured portions without approval.
>
> Rebuild readable typography as native editable text using suitable fonts, except for these lettering elements that must remain artwork: [exceptions, or none]. Report substitutions and limitations for curved, stylized, or illegible text. Flag any cleanup needed to remove the original baked-in lettering before performing it.
>
> Add a separate [black / other color] background layer with [visible / hidden] visibility. Name and group the components clearly. Deliver the PSD, a preview rendered from the actual layers, and a brief layer/font/validation report. Distinguish source cutouts from reconstructed content and distinguish a parsed PSD from one tested in desktop Photoshop.

## Generate a new design layer-first

> Create [describe the artwork] as a layer-first Photoshop project, not as a single finished image that is later presented as layered.
>
> Plan the independently editable components before generating final artwork. Use a shared composition, camera angle, scale, lighting direction, palette, and style. Generate each required foreground component as its own asset with real alpha transparency; preserve enough of the object for the intended movement and overlaps. Keep the background separate. Use shared references and inspect the assembled result for consistency.
>
> Keep these components independent: [list the important editing targets]. Create ordinary design text as native editable type, and create simple geometry as editable shapes where supported. Separate shadows, reflections, and glows when required for editing; flag interactions that will need adjustment after an object moves.
>
> Use [width × height] for the final canvas and preserve exact placement through full-canvas assets or documented offsets. Add a separate [black / other color] background layer with [visible / hidden] visibility. Deliver a real layered PSD, the transparent component assets, a layer-stack preview, and a validation report. Do not substitute a contact sheet, a painted checkerboard, duplicated full-image layers, or a final generative repaint for the requested component layers.

## Invoke an installed skill

Use the syntax supported by the host. For a local Codex installation, adapt either example:

```text
$layered-photoshop Decompose the attached photograph into source-preserving
editable components. Keep the whole subject, foreground props, background,
and readable text separate. Leave the black background hidden. Ask before
reconstructing hidden surfaces.
```

```text
$layered-photoshop Generate a layer-first illustration of [scene]. Keep
[components] independently editable, use native typography, and deliver the
layered PSD with a composite preview and validation notes.
```

Provide the actual source or creative brief along with the instruction. Load or install the skill before relying on its name as an invocation; a name in an ordinary chat is not proof that the skill or its tools are available.
