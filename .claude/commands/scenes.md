---
description: Generate campaign-grounded potential Scenes and add them to an episode
allowed-tools: Bash(ls:*), Read, Edit
argument-hint: [episode number and/or theme, e.g. "23 the harpies" or blank]
---

Generate a batch of **potential Scenes** for the campaign using the Lazy DM method,
then add the chosen ones to an episode's `## Scenes` section.

A "potential scene" is a short description of something that *might* happen this
session — an encounter, a location beat, a conversation, a decision point. It is a
loose list, not a script: not every scene will fire, and they need not run in order.
Keep each to one sentence.

## Step 1 — Figure out the target episode

Parse `$ARGUMENTS`:
- If it contains a number `N`, target `Legacy/episodes/episodeN.md`.
- Otherwise, `ls Legacy/episodes/` and target the highest-numbered `episodeN.md`
  (ignore `pilot.md`).
- Any non-number words in `$ARGUMENTS` are a **theme/focus** to lean into
  (e.g. "harpies", "Rogueport gangs", "Tefnare's past"). If none, cover the campaign broadly.

If the target episode file does not exist, stop and tell the user (suggest `/new-episode`).

## Step 2 — Load campaign context

Read, in this order:
- The target episode (its existing Scenes, Locations, Characters, and Secrets & Clues).
- The previous episode (`episode{N-1}.md`) for what just happened and where the party left off.
- `Legacy/characters.md` (the PCs and their goals/hooks).
- `Legacy/npcs.md` (factions and NPCs who could appear).
- `Legacy/rod_locations.md` and everything in `Legacy/locations/`.
- Skim 1–2 more recent episodes if you need to trace an ongoing thread.

Note the running plot threads (e.g. the Rod of Seven Parts, the Red Hand / Azarr Kull,
the Void Rifts, Rogueport's gang power vacuum, the Covenant of the Sword hunting Tefnare).

## Step 3 — Generate 6–8 potential Scenes

Write 6–8, grounded in the context above. Aim for this shape:
- **1 strong start** — a concrete opening beat that drops the party straight into
  action or tension (respect any opening already noted in the episode's Scenes).
- **2–3 plot / encounter** — combat, a chase, an obstacle, or a step toward the current
  goal (the Rod piece, the Void, a faction move).
- **1–2 roleplay / social** — a conversation, negotiation, or NPC reveal.
- **1–2 exploration / discovery** — a location beat or a chance to uncover a Secret & Clue.
- **1 wildcard / complication** — something that can escalate or twist if the table needs a jolt.

Rules:
- One sentence each, active and concrete ("The `harpies` dive as the ship rounds the
  cliffs"), not vague ("a fight happens").
- Match the file's style: wrap proper nouns / named things in backticks
  (e.g. `` `Rogueport` ``, `` `Red Hand` ``, `` `Void Rift` ``).
- Build on the episode's existing Scenes and where the previous episode ended; do not
  contradict them or repeat scenes already listed.
- Prefer real NPCs, factions, and locations from the campaign files over inventing new
  ones; if you introduce something new, keep it small and consistent with the setting.
- Where a scene is a natural place to drop one, you may hint at an existing Secret & Clue.

## Step 4 — Confirm with the DM

Present the scenes as a numbered list. Then ask the user to:
- approve all, or pick a subset (by number), or
- ask for edits / a reroll / more focused on a theme.

Do not write to the file until the user approves. Iterate as needed.

## Step 5 — Write them in

Append the approved scenes as `- ` bullets under the target episode's `## Scenes`
heading, keeping any existing bullets intact. Use Edit — do not touch the
`## Characters`, `## Locations`, or `## Secrets and Clues` sections.

Then report the episode path and how many scenes were added.
