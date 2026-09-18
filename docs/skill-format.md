# Write a portable skill header

The machine-readable header is **YAML frontmatter** at the beginning of `SKILL.md`, between two lines containing `---`. A Markdown title is separate and belongs after that block. The library README is for readers; it does not replace the skill file.

The original Layered Photoshop 0.1.0 package already included `name`, `description`, and version/maturity metadata. Version 0.1.1 clarifies discovery wording and environment requirements; it does not repair a previously absent header.

## Use the portable core

Follow the [Agent Skills specification][spec]. Apply these constraints when authoring or validating a skill:

| Field | Action |
|---|---|
| `name` | Set a 1–64-character lowercase letter/digit/hyphen name matching the enclosing folder; avoid leading, trailing, or consecutive hyphens. |
| `description` | State the task and when to use it in 1–1,024 characters. |
| `compatibility` | Add environment requirements when needed; keep this optional string within 500 characters. |
| `metadata` | Store optional custom fields as string-to-string entries; quote version values. |
| `license` | Add an optional license name or reference only after selecting the actual terms. |
| `allowed-tools` | Treat this optional field as experimental and host-dependent; omit it unless its behavior is understood. |

Use the exact filename `SKILL.md` for this library. Keep the header as YAML rather than JSON or a fenced example inside the actual skill file. Put the body's first heading after the closing delimiter.

## Start a new skill

Copy [the template](../templates/SKILL.template.md) into `skills/<your-skill-name>/SKILL.md`, then replace its example values and instructions. Set the folder name and header `name` together. This minimal example shows the placement:

```markdown
---
name: example-workflow
description: Review a supplied project brief and produce an evidence-linked action plan. Use when a user asks to turn a project brief into next steps.
---

# Review a project brief

1. Read the supplied brief and identify the requested decision.
2. Separate documented facts from assumptions and missing information.
3. Produce an action plan with evidence and unresolved questions.
```

## Inspect the Layered Photoshop header

Read the complete, authoritative header in [SKILL.md](../skills/layered-photoshop/SKILL.md). Its values describe the workflow without claiming to supply the toolchain. In particular, `compatibility` declares the need for external image and PSD tools, and `metadata.maturity` remains `instruction-only draft`.

Keep version and evidence notes synchronized with the skill README and changelog. Treat `metadata.version` as a package convention, not a capability guarantee or a required top-level field.

## Keep instructions separate from documentation

1. Put execution rules in `SKILL.md` and write each rule as an action to take.
2. Put detailed human explanations and use cases in the skill's `README.md`.
3. Put longer operating procedures and primary sources in `references/`.
4. Put reusable data and report templates in `assets/`.
5. Add `scripts/` only when runnable code is actually supplied; document its dependencies and tests.
6. Link the support files from the instructions so the agent knows when to read them.
7. Keep the skill independently usable after its folder is copied out of the library.

## Handle host-specific metadata

The optional `agents/openai.yaml` file supplies OpenAI presentation metadata. It is not the required YAML header and does not install a tool dependency. This package includes a display name, short description, and default prompt; it makes no connector declaration. See [OpenAI's metadata documentation][codex].

Keep host-specific controls out of the portable header unless required for a tested integration. For example, Claude Code supports additional invocation controls; follow its [documented behavior][claude] rather than assuming the same keys work everywhere. Configuration that pre-approves a tool is not a portable sandbox.

## Check before publishing

1. Parse the actual frontmatter as YAML and verify field types, length constraints, and matching folder/name.
2. Reject duplicate keys, missing required values, broken relative references, and accidental copy-paste fences around the header.
3. Keep portable fields at the top level and put project-specific bookkeeping under string-valued `metadata`.
4. Check the description against positive and negative trigger examples.
5. Load the package in each host for which installation is claimed, then distinguish discovery testing from successful task execution.
6. Confirm that a standalone skill archive contains its own supporting files rather than depending on paths outside the skill folder.

The local package checks in [package-validation.md](package-validation.md) are packaging evidence only; they are not host installation tests or Photoshop execution results.

[spec]: https://agentskills.io/specification
[codex]: https://developers.openai.com/codex/skills/
[claude]: https://code.claude.com/docs/en/skills
