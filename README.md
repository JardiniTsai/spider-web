# spider-web

[English](README.md) | [正體中文](README.zh-TW.md)

## Source / Credits

The core ideas in spider-web are drawn from Felix Rieseberg's article [How to be more ambitious: a tutorial for humans with models](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/) (published 13 October 2026): the four types of ambition (Speed, Altitude, Depth, and Range); the goal beyond the goal; unreasonable goals; external validation; and four questions for going one level deeper. The "nouns into verbs" technique, as cited in the article, comes from Tom Kelley and Jonathan Littman's *The Art of Innovation*. The six stages, node limits, and handoff flow are this skill's own design; they are not the author's method, and nothing here implies that Felix Rieseberg endorses this skill.

## What it is

spider-web is an agent skill that starts only when the user explicitly names it. It first frames a vague idea or task, then expands it into a web of materially distinct possibilities, and only afterwards starts `grill-me` to interrogate only the chosen path. No work is done until the user confirms a shared understanding. It is not a short-list generator.

This repository ships two versions with distinct skill names, so both can be installed at once:

- `skills/spider-web/` — English (`name: spider-web`)
- `skills/spider-web-zh/` — Traditional Chinese (`name: spider-web-zh`)

Install and use it together with both `grill-me` and `grilling`: `grill-me` is a thin wrapper that starts the `grilling` skill. See [Matt Pocock's skills repo](https://github.com/mattpocock/skills) ([grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me), [grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)). Agents installing this skill should follow [AGENTS.md](AGENTS.md).

## Six stages

The following flow is taken from the skill's `SKILL.md` and is not rewritten here. The English version:

```
Explicitly invoke spider-web
  → Stage 1: Framing interrogation (spider-web itself uses grilling's questioning style, at most 5 questions, about the problem only)
  → Stage 2: Skeleton web (list everything → group, do not delete; cap 30 nodes)
  → Stage 3: User circles nodes to expand (cap 5)
  → Stage 4: Deep expansion (fill 13 columns only for circled nodes)
  → Stage 5: User chooses a branch → write handoff.md
  → Stage 6: After writing the handoff document, start grill-me directly and interrogate only the chosen route (spider-web's handoff add-on rules apply at the same time, including one branch-switch exit)
  → Execute only after the user confirms a shared understanding
```

At the end of each stage, the agent should say in one sentence which stage it is in and what comes next. Files for each run go in `spider-web-runs/<YYYYMMDD>-<short-title>/` under the working directory: create the folder and start `web.md` at the end of Stage 1, update it at every later stage, and write `handoff.md` in Stage 5.

## Install

1. In the same agent environment, install both `grill-me` and `grilling` (folder or skill names must be `grill-me` and `grilling`). See [AGENTS.md](AGENTS.md).
2. Copy `skills/spider-web` and/or `skills/spider-web-zh` into that agent's skills directory, keeping those folder names. Each folder must have `SKILL.md` at its root.
3. If the environment reads `agents/openai.yaml`, `allow_implicit_invocation: false` there turns off implicit invocation. Even if it does not read that file, each skill's frontmatter and body still require an explicit name (`spider-web` or `spider-web-zh`).

Skills directories differ by agent. Follow the docs for the agent you use; do not assume a particular machine or account path.

Example:

```text
$spider-web I want to… first expand the possibilities, don't execute.
```

or, for the Traditional Chinese skill:

```text
$spider-web-zh 我想做……先展開可能性，不要執行。
```

Phrases like "help me think of a few directions" will not start this skill.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE).
