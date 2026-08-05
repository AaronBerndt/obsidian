---
description: Generate campaign-grounded potential Scenes and add them to a Cyberpunk episode
allowed-tools: Bash(ls:*), Read, Edit
argument-hint: [episode number and/or theme, e.g. "3 the Watson gig" or blank]
---

Generate a batch of **potential Scenes** for the Cyberpunk RED campaign using the
Lazy DM method, then add the chosen ones to an episode's `## Scenes` section.

A "potential scene" is a short description of something that *might* happen this
session — a firefight, a meet, a stakeout, a netrun, a decision point. It is a loose
list, not a script: not every scene will fire, and they need not run in order.
Keep each to one sentence.

## Step 1 — Figure out the target episode

Parse `$ARGUMENTS`:
- If it contains a number `N`, target `Cyberpunk/episodes/episodeN.md`.
- Otherwise, `ls Cyberpunk/episodes/` and target the highest-numbered `episodeN.md`
  (fall back to `pilot.md` if there are no numbered episodes yet).
- Any non-number words in `$ARGUMENTS` are a **theme/focus** to lean into
  (e.g. "the Watson gig", "corpo extraction", "a PC's debt"). If none, cover the
  campaign broadly.

If the target episode file does not exist, stop and tell the user (suggest `/cp-new-episode`).

## Step 2 — Load campaign context

Read, in this order:
- The target episode (its existing Gig, Scenes, Locations, Characters, Secrets & Clues).
- The previous episode for what just happened, what the payout was, and what Heat is
  still live.
- `Cyberpunk/characters.md` (the PCs, their Life Goals, debts, and enemies).
- `Cyberpunk/npcs.md` (fixers, corps, gangs, law).
- `Cyberpunk/gigs.md` (the job board — available, in progress, and fallout).
- Everything in `Cyberpunk/locations/` and `Cyberpunk/lore/`.
- Skim 1–2 more recent episodes if you need to trace an ongoing thread.

Note the running threads: the current gig, unpaid debts, standing Heat from past jobs,
faction pressure, and each PC's Life Goal.

## Step 3 — Generate 6–8 potential Scenes

Write 6–8, grounded in the context above. Aim for this shape:
- **1 strong start** — a concrete opening beat mid-action or mid-tension (respect any
  opening already noted in the episode's Scenes).
- **2–3 job / action** — a firefight, a heist beat, a chase, a netrun, or an obstacle
  between the crew and the payout.
- **1–2 roleplay / social** — a meet with a fixer, a Facedown, a negotiation, or an
  NPC calling in a favor.
- **1–2 exploration / legwork** — casing a site, buying info, a ripperdoc visit, or a
  chance to uncover a Secret & Clue.
- **1 wildcard / complication** — Heat arriving, a double-cross, a rival crew, or
  Trauma Team showing up for the wrong person.

Rules:
- One sentence each, active and concrete ("`Maelstrom` boosters box the crew's van in
  on the `Watson` overpass"), not vague ("a fight happens").
- Match the file's style: wrap proper nouns / named things in backticks
  (e.g. `` `Night City` ``, `` `Arasaka` ``, `` `The Afterlife` ``).
- Build on the episode's existing Scenes and where the previous episode ended; do not
  contradict them or repeat scenes already listed.
- Prefer real NPCs, factions, and locations from the campaign files over inventing new
  ones; if you introduce something new, keep it small and consistent with the setting.
- Where a scene is a natural place to drop one, you may hint at an existing Secret & Clue.
- Cyberpunk RED is lethal — at least one scene should have real teeth.

## Step 4 — Confirm with the DM

Present the scenes as a numbered list. Then ask the user to:
- approve all, or pick a subset (by number), or
- ask for edits / a reroll / more focused on a theme.

Do not write to the file until the user approves. Iterate as needed.

## Step 5 — Write them in

Append the approved scenes as `- ` bullets under the target episode's `## Scenes`
heading, keeping any existing bullets intact. Use Edit — do not touch the other
sections.

Then report the episode path and how many scenes were added.
