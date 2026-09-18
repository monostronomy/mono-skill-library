---
name: new-skill
license: MIT
description: >-
  Replace this text with the specific task and the user requests that should
  trigger it. State a meaningful boundary so unrelated requests do not match.
metadata:
  version: "0.1.0"
  maturity: "instruction-only draft"
---

# Perform the named workflow

## Establish the task

1. Replace this template with standalone instructions for one coherent workflow.
2. Read the actual user input and identify the intended result.
3. Verify the required tools, permissions, source access, and execution environment.
4. Resolve missing information only when it materially affects correctness or authorization.
5. Preserve originals and use a new output destination unless replacement is approved.

## Execute the workflow

1. Define concrete steps and connect them to the available tools.
2. Link longer procedures and sources from a local `references/` directory when supplied.
3. Use bundled scripts only when they exist, are documented, and have appropriate tests.
4. Record assumptions, transformations, and limitations alongside the work.
5. Stop or change the plan when a required capability is absent instead of claiming completion.

## Validate and deliver

1. Check the requested deliverables using tests appropriate to their intended use.
2. Distinguish performed checks from proposed tests or user-reported outcomes.
3. Deliver only outputs that exist and identify any incomplete requirement.
4. Update the human-facing README, evidence, and changelog when the workflow changes.
