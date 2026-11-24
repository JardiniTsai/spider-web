# AGENTS.md

This file is for AI agents installing the `spider-web` skill. This repository ships two skill versions with distinct names, and either or both may be installed:

- `skills/spider-web/` — English, frontmatter `name: spider-web`
- `skills/spider-web-zh/` — Traditional Chinese, frontmatter `name: spider-web-zh`

Copy the chosen folder(s) into the agent's skills directory, keeping those folder names, so each one has `SKILL.md` at its root.

## Install companions

Whichever language version you install, also install `grill-me` and `grilling` from [mattpocock/skills](https://github.com/mattpocock/skills):

- [`skills/productivity/grill-me/`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)
- [`skills/productivity/grilling/`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)

Copy those folders byte-for-byte into the agent's skills directory, keeping the folder names `grill-me` and `grilling`. Do not rewrite, summarize, or edit their contents. Pinning or recording the upstream commit is optional.

If a skill with that name is already installed, leave it in place. Do not overwrite it.

## Verify

After installing, confirm that every skill you intended to install is discoverable by the agent's skill loader:

- `spider-web` and/or `spider-web-zh` (as chosen)
- `grill-me`
- `grilling`

Each should be a folder in the skills directory with a `SKILL.md` whose frontmatter has a valid matching `name`. Report which were newly installed and which were already present.
