# Contribute a skill or improvement

## Propose a useful change

1. Identify the workflow and the user's intended result before expanding the library.
2. Check whether the change belongs in an existing skill or warrants an independent skill.
3. Describe what is implemented, what depends on host tools, and what remains a proposal.
4. Provide a small representative example without publishing private source material.

## Add a skill

1. Create `skills/<skill-name>/` and copy [the template](templates/SKILL.template.md) to `SKILL.md` inside it.
2. Set a matching name and clear trigger description using [the header guide](docs/skill-format.md).
3. Write a human-facing README covering the problem, best use cases, installation, requirements, first run, deliverables, limits, and validation evidence.
4. Write every operating rule as an action to take; make the instructions understandable without prior conversations.
5. Keep the scope focused on one coherent job or closely related modes sharing an output contract.
6. Include only reusable support material; identify required runtime files separately from optional templates, human guidance, and maintenance tests. Keep required references relative to the skill folder, and do not require client-specific histories or prior conversations to run a skill.
7. Add the skill to the root README without describing planned behavior as an implemented feature.
8. Preserve source attribution and identify any third-party material and applicable terms.

## Add executable tools

1. Document every dependency, permission, network destination, expected input, and output location.
2. Pin and test the relevant implementation versions where repeatability depends on them.
3. Preserve originals, avoid silent overwrites, and make destructive behavior explicit.
4. Keep credentials out of examples, files, archives, and logs.
5. Add useful error messages, input validation, and tests for malformed or missing inputs.
6. Test code independently of agent instructions; do not use a convincing narrative as execution evidence.
7. Separate deterministic mechanics from model-dependent judgment so failures can be reproduced.

## Record evidence

1. Name the artifact or test case and record the exact actions performed.
2. Distinguish direct execution evidence, attributed user reports, and untested expectations.
3. Record file hashes, dependency versions, and target application details when relevant.
4. Mark tests as passed, failed, blocked, or not run, and include a short reason.
5. Preserve uncertainty when the exact successful file or environment is unknown.
6. Add regression cases for confirmed failures before expanding compatibility claims.
7. Keep a proposed test plan clearly separate from a report of completed tests.

## Review images and Photoshop changes

1. Inspect the real source and the actual layers, not only an embedded preview.
2. Disclose source cutouts, reconstructed surfaces, generated objects, raster text, and substituted fonts.
3. Check alpha edges and supported blend behavior on appropriate backgrounds.
4. Test native text, masks, movement, saving, and reopening separately from initial opening.
5. Avoid publishing a client's or contributor's artwork without permission to redistribute it.
6. Keep font binaries out of the repository and asset bundles; document names instead.
7. Apply the Layered Photoshop [acceptance plan](skills/layered-photoshop/tests/acceptance-cases.md) to relevant changes.

## Report a problem

1. State the skill and package version, host, operating system, and relevant application version.
2. Provide the task brief and exact error or unexpected behavior.
3. Identify which stage failed: discovery, tool access, processing, export, opening, editing, or save/reopen.
4. Include the smallest shareable reproduction and list tests already performed.
5. Remove private data and secrets before posting screenshots, manifests, files, or logs.
6. Describe what evidence would demonstrate that the proposed fix works.

## Prepare a change for review

1. Update the skill changelog and metadata when changing its distributed behavior or documentation.
2. Check YAML, JSON templates, links, examples, and archive contents.
3. Re-run affected implementation and host tests; state anything not run.
4. Keep sample outputs and compatibility claims aligned with the actual package contents.
5. Ask the maintainer to confirm license terms before accepting third-party code or assets into a public release.
