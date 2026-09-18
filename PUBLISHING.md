# Prepare the library for public release

1. Choose the repository name and update the root title when a specific name has been selected.
2. Select the repository license, add its actual terms, and update the license notes and any skill `license` field. Use [GitHub's licensing guidance](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository); do not treat public visibility as a license choice.
3. Preserve required relative support paths under `skills/layered-photoshop/`. Keep optional templates and tests in the development repository, distinguish them from runtime requirements, and remove obsolete case-specific files when upgrading rather than merging them into the new package.
4. Review all files for private material, credentials, client imagery, font binaries, machine-specific paths, and generated outputs. Treat `.gitignore` as an aid rather than a substitute for review.
5. Keep the instruction-only status visible until an implementation is actually added and tested.
6. Confirm that no broad Photoshop-version support or completed benchmark is implied by a single artifact's successful-open report.
7. Run package checks again after editing names, files, or links; record what was checked.
8. Test discovery and a small task in every agent host you intend to claim as supported. Keep untested installation paths described as documentation-based instructions.
9. Publish the library tree as repository content. Offer a separate single-skill ZIP when useful; do not label the whole repository archive a universal skill importer or plugin.
10. Add host-specific plugin packaging only after choosing the target platform and testing its manifest and installation route.
11. Add authorized sample assets or regression fixtures only when their redistribution permissions are clear.
12. Tag the release with its real scope: documentation and workflow packaging, not a newly implemented PSD converter.

No public repository was created or modified when this starter was prepared. No license or ownership declaration has been chosen on the maintainer's behalf.
