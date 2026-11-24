# AGENTS.md

This file is for AI agents installing the `spider-web` skill. This repository ships two language versions of the same skill. Both use the frontmatter name `spider-web` and the command `$spider-web`. Install exactly one; they cannot be installed at the same time.

- `skills/spider-web/` — English
- `skills/spider-web-zh/` — Traditional Chinese (the folder name in this repository may stay `spider-web-zh`)

Copy exactly one chosen folder into the agent's skills directory. If the loader uses the folder name, name the installed folder `spider-web`. The installed folder must have `SKILL.md` at its root.

## Install companions

Whichever language version you install, also install `grill-me` and `grilling` from [mattpocock/skills](https://github.com/mattpocock/skills). Stage 1 follows `grilling`'s questioning style without loading that skill; stage 6 starts `grill-me` (which starts `grilling`) and interrogates only the chosen route.

Install them from:

- [`skills/productivity/grill-me/`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)
- [`skills/productivity/grilling/`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)

Copy those folders byte-for-byte into the agent's skills directory, keeping the folder names `grill-me` and `grilling`. Do not rewrite, summarize, or edit their contents. Pinning or recording the upstream commit is optional.

If a skill with that name is already installed, leave it in place. Do not overwrite it.

## Verify

After installing, confirm that every skill you intended to install is discoverable by the agent's skill loader:

- `spider-web` (exactly one language version)
- `grill-me`
- `grilling`

Each should be a folder in the skills directory with a `SKILL.md` whose frontmatter has a valid matching `name`. Report which were newly installed and which were already present.
