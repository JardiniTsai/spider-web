---
name: spider-web
description: >-
  Use only when the user explicitly names spider-web (e.g. "$spider-web", "use
  spider web", "spider-web this") to frame and then broadly explore a vague idea
  or task into many materially distinct possibilities before choosing or
  building. Never start it from generic wording like "help me think of a few
  directions" or "幫我想幾個方向".
---
# spider-web: frame first, expand, then hand off to grill-me

## 0. Explicit invocation only (the lock)

- Start only when the user explicitly writes spider-web (for example `$spider-web`, "use spider web", or "run spider-web").
- Wording such as "help me think of a few directions", "let's diverge", or "brainstorm" **must not** start it. You may ask "Want to run this with spider-web?", but you must not start on your own.
- For simple tasks (shortening a letter, fixing a typo), just do the work. Do not mention spider-web.
- **Sole exception: re-entry for a branch switch.** If the user has already explicitly started this run, and the interrogation stage hits the §8 branch-switch exit, the user or the agent may call spider-web again — but only in "branch-switch mode", carrying the existing `handoff.md` and `web.md`. Do not open a new topic.
- If the environment honors `agents/openai.yaml`, its `allow_implicit_invocation: false` is also part of this lock.

## 1. Flow overview

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

- At the end of each stage, tell the user in one sentence which stage you are in and what comes next.
- Put files for each run in `spider-web-runs/<YYYYMMDD>-<short-title>/` under the working directory. Create the folder and start writing `web.md` at the end of Stage 1, then update it at every later stage; write `handoff.md` in Stage 5.
- Cost caps are in §9. No stage may exceed them.

## 2. Stage 1: Framing interrogation

**Do not load** the grilling skill in this stage. spider-web itself follows grilling's questioning style:

- Ask only one question at a time, and wait for the user's reply before asking the next.
- Attach your recommended answer to every question.
- Look up facts you can find from the environment, files, or tools; do not ask the user for those. Only decisions go to the user.
- Do not start implementing any solution before a shared understanding is confirmed.

Framing-only rules:

- **Question count**: at most 5 questions (confirming "Frame OK" does not count). Stop once the four facets below all have answers; you need not use all five. Do not re-ask a facet the user's original wording already answered.
- **Ask about the problem, not the solution.** Do not propose, compare, or hint at any solution. If the user volunteers a solution, record it as "the user's initial idea" and treat it as an ordinary node in Stage 2, not as a premise.
- **Four required facets**:
  1. **The real desired outcome**: climb the "and then?" ladder (below) and find the highest layer that is still deliverable.
  2. **Hard constraints**: budget, time, regulation, technology, staffing, brand, or other immovable conditions.
  3. **Out of scope**: directions that are explicitly excluded.
  4. **How success is judged**: observable metrics or judgment criteria, and who judges.
- **The "and then?" ladder**:
  - Start from the user's original wording and keep asking "After this is done, and then?", writing a higher outcome at each step up.
  - After each step, judge whether it is deliverable: within the hard constraints, can AI plus existing resources produce a result in a reasonable time?
  - At the first layer that is "not doable, or too vague" (for example "help me make a million"), **step back one layer**. That layer is "the real desired outcome".
  - You draft the ladder and recommend where to stop; the user decides.
- **Produce a "frame card"**, at most 10 lines:
  ```
  Topic (original wording):
  Real desired outcome (layer N):
  The layer stepped back from, and why:
  Hard constraints:
  Out of scope:
  Success criteria:
  User's initial idea (if any, to be used as a node):
  ```
- **Gate**: enter Stage 2 only after the user replies "Frame OK" or after their corrections.

## 3. Stage 2: Skeleton web

- Expand breadth-first within the frame card. Axes include speed, altitude, depth, range, demand, channels, monetization, retention, and lifecycle, plus any other axes the topic needs.
- **Nouns into verbs (required)**: before expanding, rewrite product nouns in the topic as the job they must do (for example, "homepage" → "make a stranger stop and get curious within five seconds"). Ask "Which industries in the world are best at this?", find at least 3 different industries, borrow one technique from each, and make each a node. Show this verb rewrite at the start of the skeleton web.
- **Unreasonable goals (optional)**: you may do this once for a group, set the success metric to an extreme value, and ask "If this were definitely achievable, what would be completely different about the approach?", producing new nodes. Do not write extreme goals into the frame card's success criteria, and do not treat them as a promise.
- **Each node has only three fields**:

  | Field | Content |
  |---|---|
  | Name | Short name, 6–15 characters |
  | One-liner | What this node is and how it differs from the others, within 30 characters |
  | Demand-evidence strength | Strong / medium / weak / none, plus one sentence of basis (for example "has public search volume" or "only a guess") |

- Demand evidence may be checked only lightly: at most one quick lookup per node, or use known facts. Do not do deep research.
- **Stop when**: you reach 30 nodes, or new ideas are only slight variations of existing nodes, whichever comes first. If you stop because of the cap, also list at most 3 "remaining directions" — names only, no numbers, not counted as nodes.
- **Output order**:
  1. Full node list: numbered N1, N2…, list all, do not sort.
  2. Grouping: each group lists its node numbers; do not hide, delete, or merge nodes.
  3. Mark obviously duplicate nodes, but still keep them.
- In this stage, **do not recommend and do not rank**.

## 4. Stage 3: User circles nodes

- Ask the user to circle the nodes to expand, at most 5; a combination counts as 1. To circle more, they must first drop others.
- You may offer **one** recommendation with reasons (for example "I'd circle N3, N7, and N12"). The whole web is already visible, so this is not early convergence.
- The user may ask for one more skeleton round (only 1 round). After it, the total number of nodes still must not exceed 30.

## 5. Stage 4: Deep expansion

- Fill all 13 columns only for circled nodes: higher-level outcome, demand evidence, first users, repeatable acquisition channel, product-led growth loop, business model, retention path, expert methods, primary data, external validation, cross-domain techniques, risks, and required tools / permissions / environment.
- Look up facts, tools, and feasibility yourself, at most 3 queries per node; if you cannot find something, mark it "Unverified" and later put it in the unverified assumptions in handoff.md.
- **"Not applicable" rules**:
  - For non-product topics (internal process, personal task, one-off project, and the like) or when a node itself does not apply, you may write `Not applicable: <one-sentence reason>`.
  - **These 5 columns must not be marked not applicable**: higher-level outcome, expert methods, primary data, external validation, and risks. Every topic must have substantive content in them.
  - In a product topic, if more than half of the four columns acquisition, growth loop, business model, and retention are marked not applicable, note at the end of the node "this node may not be a product opportunity".
- **Fill expert methods with the four depth questions**: What would a leading expert in this field do that I have not thought of? What primary sources would they look at? What methods and tools would they use? How would they show that it works?
- **Unreasonable-goal stress test**: do this at least once for every circled node, as a short section "Approach under an extreme goal".
- **Real-world completeness**: if a node depends on a real-world mechanism, list the physical preconditions, the people or organizations that must be handed off to, and time lags. Sample data, simulations, fake integrations, or demos may test an interface or an assumption, but if they bypass the product's actual real-world mechanism, you must not say it is "already live".
- At the end you may recommend a node or a combination, with reasons.

## 6. Stage 5: Choose a branch and write the handoff

- After the user chooses a branch (one node or a combination) and confirms a shared understanding, write `handoff.md` in the same folder, in this format:

```markdown
# Handoff: <short topic name>
- Date:
- web.md: <path>
- Chosen branch: <node numbers and names; list each node if it is a combination>
- Why it was chosen (the user's wording or confirmation):

## Frame card
(Paste the Stage 1 frame card as-is)

## Hard constraints
- …

## 13 columns for the chosen branch
| Field | Content | Evidence strength (strong / medium / weak / unverified) | Source |
|---|---|---|---|
| Higher-level outcome | | | |
| … (13 rows; if not applicable, give a reason) | | | |

## Nearby alternatives (at most 3)
| Node | One-liner | When to choose it instead |
|---|---|---|

## Unverified assumptions
| # | Assumption | Impact if false | How to verify | Needs a user decision? |
|---|---|---|---|---|

## Real-world preconditions
| Precondition | Handoff needed (person / organization) | Estimated time lag | Can a demo stand in (usually no) |
|---|---|---|---|
(If none, write "no physical mechanism" and give a reason)

## Interrogation status
- Branch-switch used: no
- Settled decisions: (update during interrogation)
- Open decisions:
```

- Contents of `web.md`: the frame card, the verb rewrite, the full skeleton web, grouping, the circling record, and the deep-expansion content.

## 7. Stage 6: Hand off to grill-me

- After writing the handoff document, start the `grill-me` skill directly and interrogate only the chosen route, following its text as written, without rewriting or omitting any of its rules. Do not modify the grilling or grill-me files at all.
- The following are spider-web's **handoff add-on rules**. They apply at the same time as grill-me (they belong to spider-web, not to grill-me; they do not apply when grilling or grill-me is used on its own):
  1. Read `handoff.md` before starting. Do not re-ask facts the handoff already answered; start from "unverified assumptions" and trade-offs that need a user decision.
  2. Each time a decision is settled, update the "Interrogation status" in `handoff.md`.
  3. On every question, check whether the §8 branch-switch exit has been triggered.
- Execute only after the user confirms a shared understanding. When executing, follow the environment's existing assignment rules (for example, hand programming work to an existing engineering process or designated tool).

## 8. Interrogation exit: return to the web and switch branches

- **Triggers** (any one):
  - An unverified assumption is shown to be false, and it is a premise the chosen branch depends on;
  - A hard constraint appears during interrogation that is incompatible with the chosen branch;
  - The user says the frame card's "real desired outcome" has changed.
- **Re-entry**: stop grill-me, and have the user or the agent call spider-web again, carrying the existing `handoff.md` and `web.md` into branch-switch mode (the exception in §0).
- **Branch-switch actions**:
  1. Explain which premise was overturned and what the evidence is.
  2. Return to `web.md`, look first at nearby alternatives, then at other already expanded or skeleton nodes; suggest 1 or 2 replacement branches, with a recommendation, for the user to choose. Before proposing them, check each one against the frame card's hard constraints; do not propose nodes already known to be incompatible.
  3. If a newly chosen node has not been deep-expanded, fill the 13 columns, counting toward the cap of 5 deep-expanded nodes; if the cap is already full, ask the user to drop one already expanded node first.
  4. Update `handoff.md`: set "Branch-switch used" to "yes", keep a record of the original branch, and rewrite the sections about the chosen branch.
  5. Start grill-me again directly and interrogate only the newly chosen route; reuse settled decisions that still apply.
- **Cap**: only one switch per run. If a premise is overturned a second time, stop, report to the user, and suggest reframing from scratch or ending. Do not switch again on your own.
- If what was overturned is the frame card itself (the outcome or hard constraints changed), that is not a branch switch. Directly suggest that the user explicitly invoke spider-web again, starting from Stage 1.

## 9. Cost caps

| Item | Cap | Notes |
|---|---|---|
| Framing interrogation | 5 questions | Stop early once all four facets have answers |
| Skeleton-web nodes | 30 | Includes the extra round; stop at the cap, and list at most 3 "remaining directions" (names only) |
| Extra skeleton round | 1 | Only if the user asks |
| Deep-expanded nodes | 5 | A combination counts as 1; a branch-switch fill also counts |
| Skeleton demand checks | At most 1 quick lookup per node | Leave deep research for Stage 4 |
| Deep-expansion research | At most 3 queries per node | Mark "Unverified" if not found |
| Return-to-web branch switch | 1 | See §8 |

## 10. If you find a defect in the skill: propose only, do not edit it yourself

1. If you find a missing axis, early convergence, or any other defect in the skill, **do not modify any skill file** (including this one, grilling, and grill-me).
2. Attach a "proposed fix" at the end of that turn's reply: the problem, a minimal fix (as a diff), the scope of impact, and whether a rerun is needed.
3. Continue this run under the current skill unless the user says to stop.
4. Edit the skill only after the user explicitly approves the proposal, then say what changed. Whether to rerun from the original prompt is the user's decision; the default is not to rerun.
5. Do not write project-specific facts into this general-purpose skill; when needed, the user should provide project context before invoking it.

## 11. Bottom line

- Do not start implicitly (except for the §0 branch-switch re-entry).
- Do not exceed the §9 caps.
- In the skeleton-web stage, do not rank, merge, or recommend; grouping must not hide or delete nodes.
- Do not dump a large questionnaire on the user, and do not ask the user to imagine every possibility themselves.
- Do not ask the user for facts you can look up.
- Do not describe a demo or simulation as a real-world launch.
- Do not execute until the user has chosen a branch and confirmed a shared understanding.
