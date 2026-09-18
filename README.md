# Skill Library

Reusable workflows for tool-enabled AI agents: clear instructions, explicit dependencies, practical examples, and evidence of what has actually been tested.

Start with a skill that matches the job. Read its requirements, load the complete skill folder into a compatible agent, and give the agent the actual source material or creative brief. A skill organizes the work; it does not create tool access or guarantee the result.

**First available skill:** [Layered Photoshop](skills/layered-photoshop/README.md) — separate an existing image into editable components, or plan new artwork as independent transparent assets for a layered Photoshop document.

**Current release:** the first skill is an instruction-only draft, version **0.1.2**. It includes workflows, references, prompts, and planning/test templates. It does not yet include a general-purpose PSD exporter or image-processing implementation. Read the skill's [evidence and limitations](skills/layered-photoshop/README.md#evidence-and-current-status) before relying on it for production.

## Start here

| Your goal | Open this |
|---|---|
| Learn the Photoshop workflow, use cases, and limitations | [Layered Photoshop guide](skills/layered-photoshop/README.md) |
| Copy a task brief into an agent | [Prompt library](skills/layered-photoshop/PROMPTS.md) |
| Install a skill in a local agent | [Installation instructions](#install-a-skill) |
| Understand the required skill header | [Skill format and frontmatter](docs/skill-format.md) |
| Add another skill to this repository | [Contribution guide](CONTRIBUTING.md) and [skill template](templates/SKILL.template.md) |
| Prepare this starter for publication | [Publishing checklist](PUBLISHING.md) |

## Available skills

| Skill | Use it to | Package status |
|---|---|---|
| [`layered-photoshop`](skills/layered-photoshop/README.md) | Separate photographs, scans, illustrations, or flattened graphics into useful editable components; create new layer-first artwork; specify native editable typography and PSD validation. | Instruction-only draft; general processing and export workflows remain unvalidated. |

The use cases describe intended workflows, not a benchmarked success rate. More skills can be added as independent folders without changing how the first one is organized.

## What a skill contains

Each skill has an agent-facing `SKILL.md` and a human-facing `README.md`. The skill header identifies the task; the body supplies operating instructions. Supporting files hold longer procedures and reusable material. This follows the [Agent Skills format][skill-spec].

This repository separates three things:

- **Read the README to understand the workflow.** Find use cases, setup, examples, limitations, and evidence before starting.
- **Load SKILL.md to guide the agent.** Keep the operating instructions focused rather than loading the entire library into every task.
- **Provide the required tools to perform the work.** Check the selected skill's requirements; do not assume that a Markdown file installs software, grants permissions, or supplies an external service.

A skill may be instruction-only, may bundle scripts, or may depend on services outside the repository. Inspect each skill individually. Do not interpret a polished README as evidence that an implementation or integration test exists.

## Repository layout

```text
.
├── README.md                         # Library overview and installation
├── CONTRIBUTING.md                   # Rules for adding or improving skills
├── PUBLISHING.md                     # Maintainer's publication checklist
├── CHANGELOG.md                      # Changes to this starter
├── .gitignore
├── docs/
│   ├── skill-format.md               # Header format and authoring conventions
│   └── package-validation.md         # Packaging checks, not PSD tests
├── templates/
│   └── SKILL.template.md             # Starting point for the next skill
└── skills/
    └── layered-photoshop/
        ├── SKILL.md                  # Agent instructions and YAML frontmatter
        ├── README.md                 # Detailed workflow guide
        ├── PROMPTS.md                # Ready-to-adapt task briefs
        ├── CHANGELOG.md
        ├── agents/
        │   └── openai.yaml           # Optional OpenAI presentation metadata
        ├── assets/                  # Optional generic job/report templates
        ├── references/              # Generic runtime procedures and sources
        └── tests/                   # Optional maintainer acceptance plan
```

The `skills/` directory is the library's source layout. It is not automatically an installation directory for every agent. Copy the selected skill into the location required by the host, or use that host's supported installer.

## Install a skill

### Select and inspect the package

1. Download or clone this repository, or extract the supplied starter archive.
2. Read the selected skill's README and `SKILL.md`, including any scripts and external-service requirements.
3. Copy the **whole skill folder** for the simplest installation, keeping relative paths intact. For a smaller Layered Photoshop installation, keep `SKILL.md` and its four generic reference files; follow the skill's [required/optional file guide](skills/layered-photoshop/README.md#keep-execution-files-separate-from-optional-material) before omitting templates, tests, or human documentation.
4. Install only in an environment whose tool access and permissions you understand.
5. Confirm that the agent can find the skill, read a supporting file, and report its actual capabilities before expensive work.

### Use Codex locally

For a project installation, copy `skills/layered-photoshop/` to `.agents/skills/layered-photoshop/` inside the working project. For personal use across projects, use `~/.agents/skills/layered-photoshop/`. These are documented local discovery locations; confirm changes against the [current Codex instructions][codex-skills].

Run this PowerShell example **from the library repository root** to install into that same working directory without overwriting an existing skill:

```powershell
$source = Join-Path (Get-Location) "skills/layered-photoshop"
$target = Join-Path (Get-Location) ".agents/skills/layered-photoshop"

if (-not (Test-Path (Join-Path $source "SKILL.md"))) {
    throw "Run this from the library root; the source skill was not found."
}
if (Test-Path $target) {
    throw "The destination already exists. Review it before replacing it."
}

New-Item -ItemType Directory -Force -Path (Split-Path $target) | Out-Null
Copy-Item -LiteralPath $source -Destination $target -Recurse
```

Use this equivalent Bash example on macOS or Linux:

```bash
# Run from the library repository root.
source_dir="$PWD/skills/layered-photoshop"
target_dir="$PWD/.agents/skills/layered-photoshop"

if [ ! -f "$source_dir/SKILL.md" ]; then
  printf '%s\n' 'Source skill not found; use the library root.' >&2
elif [ -e "$target_dir" ] || [ -L "$target_dir" ]; then
  printf '%s\n' 'Destination exists; review it before replacing it.' >&2
else
  mkdir -p "$(dirname "$target_dir")" &&
  cp -R "$source_dir" "$target_dir"
fi
```

Point the destination at a different working project when appropriate. Keep that project's inputs and outputs outside the public library.

In Codex CLI or its IDE extension, mention the installed skill with `$layered-photoshop`; use the skill picker to confirm discovery. Restart Codex if a local update is not recognized. This invocation syntax is host-specific, not part of the portable file format. [Source: Codex skill documentation][codex-skills].

```text
$layered-photoshop Inspect input/source.png and propose a source-preserving
layer breakdown. Keep text editable where feasible. Report available image
and PSD tools before processing; do not reconstruct hidden surfaces yet.
```

### Use Claude Code locally

Copy the whole folder to `.claude/skills/layered-photoshop/` for a project, or `~/.claude/skills/layered-photoshop/` for personal use. Invoke it with `/layered-photoshop`. Refer to the [Claude Code skill documentation][claude-skills] for discovery and permission behavior.

```text
/layered-photoshop Plan a layer-first illustration from this brief. Keep the
subject, prop, background, shadows, and title independently editable. Check
that this session has the tools to produce the requested deliverables.
```

Installing these instructions does not give Claude Code an image generator or Photoshop. Verify those capabilities separately.

### Use another host or a chat session

Follow the host's documented import process. A name typed into an ordinary conversation is not proof that the host has loaded the skill. When skill import is unavailable, provide the skill and its support files as explicit task instructions and use the standalone prompts. File access, image tools, and a PSD-writing route are still prerequisites for an actual PSD.

Use the **single-skill archive** for importers that expect one skill. Use the **library starter archive** as repository content; do not assume it is also a one-click plugin or a single-skill upload. Provider-specific plugin packaging is a separate distribution step.

## Verify a first run

1. Ask the agent to state which skill it loaded and which supporting files it can read.
2. Ask it to distinguish bundled implementation from tools supplied by the host.
3. Start with a small, non-sensitive test input and a limited editing goal.
4. Compare the requested deliverables with the files actually produced.
5. Record tests as passed, failed, blocked, or not run; retain the evidence with the result.

For Photoshop work, check the finished file in the actual target application. Parsing a file and displaying its cached preview are different from editing its text and masks, saving, and reopening it. Use the skill's [validation workflow](skills/layered-photoshop/references/export-and-validation.md).

## Choose a useful first job

Start with a task where independent editing has a clear purpose: changing poster copy, separating a product from a background, rebuilding an emblem's main components, or making a new illustration whose character and props must remain reusable.

Avoid making the first test a demand for perfect recovery of every hidden object, physically independent glass, or a fully rigged animation puppet. Those are different and more demanding output contracts. The [Photoshop use-case guide](skills/layered-photoshop/README.md#best-use-cases) explains the distinctions.

## Improve the library

Follow [CONTRIBUTING.md](CONTRIBUTING.md). Keep each skill independently understandable. Document its inputs, outputs, dependencies, limits, and evidence. Keep client-specific histories and filenames out of runtime instructions; retain reusable lessons in generic procedures and keep authorized project records separate. Add deterministic code where repeatability matters, and test that code rather than asking the agent to reinvent it on every run.

Use the [frontmatter guide](docs/skill-format.md) and [template](templates/SKILL.template.md) when adding a skill. Keep host-specific configuration separate from portable instructions whenever practical.

## Privacy, licensing, and publication

Keep private source images, credentials, generated client work, font binaries, and application caches out of this repository. Review the actual files before committing; `.gitignore` is a convenience, not a privacy review.

**No repository license has been selected in this starter.** Select a license and add its terms before describing the project as open source or inviting reuse on those terms. GitHub's [licensing guide][github-license] explains the distinction between publishing a repository and licensing it. Do not assume that a repository license also covers third-party fonts, photos, logos, or other assets.

This library is an independent project, not an Adobe, OpenAI, or Anthropic product. Compatibility instructions describe intended integration paths, not vendor endorsement or completed certification.

[skill-spec]: https://agentskills.io/specification
[codex-skills]: https://developers.openai.com/codex/skills/
[claude-skills]: https://code.claude.com/docs/en/skills
[github-license]: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository
