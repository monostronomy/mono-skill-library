# Verify external references

Consult these primary sources before implementation. Treat the access date, 2026-09-18, as the documentation check date, not as a guarantee against later changes.

1. **S1 — Verify the agent-skill format and installation behavior.** Consult OpenAI's skill documentation: `https://developers.openai.com/codex/skills/`. Follow and verify any redirect rather than relying on a previously observed destination. Check `SKILL.md` metadata, optional references/scripts, and current host locations.
2. **S2 — Verify supported image output and model limitations.** Consult OpenAI's *Image generation*: `https://developers.openai.com/api/docs/guides/image-generation`. Check transparency, output formats, exact sizing support, visual consistency, and placement limitations.
3. **S3 — Verify transparent-asset prompting and alpha preservation.** Consult OpenAI's *Image prompting*: `https://developers.openai.com/api/docs/guides/image-prompting`. Distinguish real alpha from a drawn checkerboard.
4. **S4 — Verify native type creation.** Consult Adobe's *TextLayerCreateOptions*: `https://developer.adobe.com/photoshop/uxp/ps_reference/objects/createoptions/textlayercreateoptions/`. Check supported fields, version constraints, and baseline positioning.
5. **S5 — Verify PSD binary structures.** Consult Adobe's *Photoshop File Formats Specification*: `https://www.adobe.com/devnet-apps/photoshop/fileformatashtml/`. Check layer/mask sections, descriptors, group-related records, padding, PSD/PSB distinctions, and the different version fields.
6. **S6 — Ground the limits of single-image matting.** Consult Hou and Liu, *Context-Aware Image Matting for Simultaneous Foreground and Alpha Estimation* (2019): `https://arxiv.org/abs/1909.09725`. Distinguish plausible estimates from unique recovery of foreground, alpha, and background.
7. **S7 — Check a candidate writer's limits instead of assuming full Photoshop parity.** Consult the ag-psd maintainers' README: `https://github.com/Agamnentzar/ag-psd`. Review current text, color-mode, bit-depth, PSB, and cache-rendering limitations.
8. **S8 — Verify native layer properties.** Consult Adobe's *Layer*: `https://developer.adobe.com/photoshop/uxp/ps_reference/classes/layer/`. Check masks/layer handling through supported APIs, blending, locks, and version-specific behavior before implementation.

Keep project-specific evidence in the current job's report or in separate, authorized maintainer records. Do not require another project's files or a prior conversation to execute this skill. Do not use external references as evidence that this instruction-only package has executed any image or export operation.

## Check skill-library packaging references

9. **S9 — Verify the portable header.** Consult the Agent Skills specification: `https://agentskills.io/specification`. Check required and optional fields, name constraints, and string-valued metadata.
10. **S10 — Verify Claude Code discovery and invocation.** Consult the official skill guide: `https://code.claude.com/docs/en/skills`. Check local installation paths and host-specific behavior.
11. **S11 — Choose publication terms explicitly.** Consult GitHub's licensing guide: `https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository`. Select actual terms before adding license metadata; do not assume that a public repository is automatically open source.

Keep the library's human-facing documentation separate from the instructions in `SKILL.md`. Treat installation examples as documentation-based guidance until tested in the target host.
