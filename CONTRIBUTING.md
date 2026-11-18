# Contributing

This repository holds open-source skills written by others, for Collabrium's skill catalog. Most contributions add,
update or remove one of those skills. Read the license policy and the quality bar in the [README](README.md) first.

## Adding a skill

1. **Check the license.** Find the license that covers the skill's folder: a license file in the folder, else the
   upstream repository's top-level license, and the SKILL.md's `license` field. All of them must agree and be one of
   MIT, Apache-2.0, BSD-2-Clause, BSD-3-Clause, ISC, CC0-1.0, Unlicense or CC-BY-4.0. If a skill says it was adapted
   from another one, the original's license must qualify too. When in doubt, leave it out.
2. **Read every file.** Treat what you downloaded as untrusted: do not run its scripts to "try it". Read them. Leave the
   skill out if a script downloads and runs code (`curl … | sh`), reads credentials or files outside the working
   directory, sends data anywhere the skill does not say, is obfuscated or minified, or turns off safety checks. Note
   any paid or proprietary service it needs.
3. **Copy the folder** to `skills/<name>/`, where `<name>` is the SKILL.md's `name` (`a-z`, `0-9`, single hyphens, at
   most 64 characters, no `claude` or `anthropic`; pick a clear name and record the rename if upstream's does not fit).
   Do not copy hidden files, symlinks, or files that belong to the upstream repository rather than the skill
   (README, CI, packaging).
4. **Keep the license.** Put the license text in the folder as `LICENSE` (or keep upstream's `LICENSE.txt`), keep every
   copyright header, and copy any Apache-2.0 `NOTICE` file. Set the frontmatter `license` to
   `<SPDX id> (full text in LICENSE)`.
5. **Change only what the format needs**, such as bundling a file the skill links to outside its folder and fixing that
   link. Do not edit the instructions.
6. **Write `SOURCE.md`** in the folder: upstream repository, path, full commit SHA, original authors, license, and the
   list of changes (see any existing skill for the layout).
7. **Update the indexes:** `skills.json`, the table in `README.md`, and `THIRD_PARTY_NOTICES.md`.
8. **Check it imports.** Push a branch and, in Collabrium, add the skill from GitHub with
   `Falcon-Tech-Systems/collabrium-skills/skills/<name>@<branch>`. The review must show no refusal, and no warning
   other than ones you have explained in the pull request. Keep the repository well under the catalog's caps
   (16 MiB tarball, 25 MiB unpacked).

## Updating a skill

Copy the new upstream version over the folder, redo steps 2 to 8, and update the commit in `SOURCE.md`, `skills.json`
and `THIRD_PARTY_NOTICES.md`. Re-check the license: projects do change them.

## Removing a skill

Delete the folder and its entries in the three indexes. Collabrium drops it from the catalog at the next daily sync;
copies people already added stay in their libraries.

## Pull requests

One skill (or one upstream repository's batch) per pull request, with the license, the commit, and anything notable
you found while reading the files in the description.
