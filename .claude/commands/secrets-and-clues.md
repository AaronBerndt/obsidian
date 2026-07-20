---
description: Generate campaign-grounded Secrets & Clues and add them to an episode
allowed-tools: Bash(ls:*), Read, Edit
argument-hint: [episode number and/or theme, e.g. "23 the harpies" or blank]
---

Generate a batch of **Secrets & Clues** for the campaign using the Lazy DM method,
then add the chosen ones to an episode's `## Secrets and Clues` section.

A "secret or clue" is a single, short piece of information the players *might*
discover this session. It is NOT tied to a location or NPC — you reveal it wherever
it fits. Keep each to one sentence.

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
- The target episode (see what Scenes/Locations/Characters and existing clues it has).
- The previous episode (`episode{N-1}.md`) for what just happened.
- `Legacy/characters.md` (the PCs and their backstory hooks).
- `Legacy/npcs.md` (factions and NPCs).
- `Legacy/rod_locations.md` and everything in `Legacy/locations/`.
- Skim 1–2 more recent episodes if you need to trace an ongoing thread.

Note the running plot threads (e.g. the Rod of Seven Parts, the Red Hand / Azarr Kull,
the Void Rifts, Rogueport's gang power vacuum, the Covenant of the Sword hunting Tefnare).

## Step 3 — Generate 10 Secrets & Clues

Write 10, grounded in the context above. Aim for this mix:
- **3–4 main-plot** — advance the Rod hunt, the Red Hand, or the Void.
- **2–3 PC-personal** — tied to a specific PC's backstory (Jeanne, Bodvar, Tefnare,
  Ygara, Egoluis, Rel) or an active NPC relationship.
- **2 world/lore/color** — foreshadowing, faction news, or flavor that deepens the setting.
- **1 immediate hook** — ties into this episode's opening scene or theme.
- **1 danger/red herring** — a warning, a lie, or a threat that raises tension.

Rules:
- One sentence each. Concrete and revealable, not vague mood.
- Match the file's style: wrap proper nouns / named things in backticks
  (e.g. `` `Void Rift` ``, `` `Red Hand` ``, `` `Tef` ``).
- Do NOT repeat clues already listed in the target or previous episode — unless you're
  deliberately carrying forward an unresolved one, in which case say so.
- Prefer using names and threads that actually exist in the campaign files over inventing
  new ones; if you introduce something new, keep it small and consistent with the setting.

## Step 4 — Confirm with the DM

Present the 10 as a numbered list. Then ask the user to:
- approve all, or pick a subset (by number), or
- ask for edits / a reroll / more focused on a theme.

Do not write to the file until the user approves. Iterate as needed.

## Step 5 — Write them in

Append the approved clues as `- ` bullets under the target episode's
`## Secrets and Clues` heading, keeping any existing bullets intact. Use Edit — do not
touch the `## Characters`, `## Scenes`, or `## Locations` sections.

Then report the episode path and how many clues were added.
