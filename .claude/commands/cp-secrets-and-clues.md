---
description: Generate campaign-grounded Secrets & Clues and add them to a Cyberpunk episode
allowed-tools: Bash(ls:*), Read, Edit
argument-hint: [episode number and/or theme, e.g. "3 the Watson gig" or blank]
---

Generate a batch of **Secrets & Clues** for the Cyberpunk RED campaign using the
Lazy DM method, then add the chosen ones to an episode's `## Secrets and Clues` section.

A "secret or clue" is a single, short piece of information the players *might*
discover this session. It is NOT tied to a location or NPC — you reveal it wherever
it fits. Keep each to one sentence.

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
- The target episode (its Gig, Scenes, Locations, Characters, and existing clues).
- The previous episode for what just happened and what Heat is still live.
- `Cyberpunk/characters.md` (the PCs, their Life Goals, debts, and enemies).
- `Cyberpunk/npcs.md` (fixers, corps, gangs, law).
- `Cyberpunk/gigs.md` (the job board — available, in progress, and fallout).
- Everything in `Cyberpunk/locations/` and `Cyberpunk/lore/`.
- Skim 1–2 more recent episodes if you need to trace an ongoing thread.

## Step 3 — Generate 10 Secrets & Clues

Write 10, grounded in the context above. Aim for this mix:
- **3–4 gig-critical** — what the client actually wants, who else is bidding, where
  the real security is, what the twist is.
- **2–3 PC-personal** — tied to a specific PC's Lifepath, Life Goal, debt, or enemy.
- **2 world / faction / street** — corp maneuvering, gang turf shifts, screamsheet
  news, or Net/Blackwall color.
- **1 immediate hook** — ties into this episode's opening scene or theme.
- **1 danger / red herring** — a warning, a plant, or a threat that raises tension.

Rules:
- One sentence each. Concrete and revealable, not vague mood.
- Match the file's style: wrap proper nouns / named things in backticks
  (e.g. `` `Arasaka` ``, `` `Maelstrom` ``, `` `Trauma Team` ``).
- Do NOT repeat clues already listed in the target or previous episode — unless you're
  deliberately carrying one forward, in which case say so.
- Prefer names and threads that actually exist in the campaign files over inventing new
  ones; if you introduce something new, keep it small and consistent with the setting.
- In Cyberpunk, most information is bought, leaked, or stolen — favor clues that have
  a plausible source on the street.

## Step 4 — Confirm with the DM

Present the 10 as a numbered list. Then ask the user to:
- approve all, or pick a subset (by number), or
- ask for edits / a reroll / more focused on a theme.

Do not write to the file until the user approves. Iterate as needed.

## Step 5 — Write them in

Append the approved clues as `- ` bullets under the target episode's
`## Secrets and Clues` heading, keeping any existing bullets intact. Use Edit — do not
touch the other sections.

Then report the episode path and how many clues were added.
