# AGENTS.md

This file is for AI agents installing the `spider-web` skill.

## Install companions

When you install `spider-web`, also install `grill-me` and `grilling` from [mattpocock/skills](https://github.com/mattpocock/skills):

- [`skills/productivity/grill-me/`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)
- [`skills/productivity/grilling/`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)

Copy those folders byte-for-byte into the agent's skills directory, keeping the folder names `grill-me` and `grilling`. Do not rewrite, summarize, or edit their contents. Pinning or recording the upstream commit is optional.

If a skill with that name is already installed, leave it in place. Do not overwrite it.

## Verify

After installing, confirm that `spider-web`, `grill-me`, and `grilling` are all discoverable by the agent's skill loader. Each should be a folder in the skills directory with a `SKILL.md` whose frontmatter has a valid `name` (`spider-web`, `grill-me`, or `grilling`). Report which of the three were newly installed and which were already present.
