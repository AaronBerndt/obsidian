---
description: Scaffold the next Ravenloft (Dementlieu) episode in Ravenloft/episodes
allowed-tools: Bash(ls:*), Write
argument-hint: [episode title]
---

Create a new, blank episode file for the Ravenloft (Dementlieu) campaign.

Steps:
1. Determine the next episode number by listing `Ravenloft/episodes/`, finding the
   highest existing `episodeN.md` (ignore `pilot.md`), and adding 1. Call this `N`.
   If the folder doesn't exist or no numbered episodes exist yet, `N` is 1.
2. Create `Ravenloft/episodes/episodeN.md` with exactly this content (substitute `N`,
   and use the title from `$ARGUMENTS` after the colon — leave it blank if none was given):

```
---
id: ravenloft_episodeN
aliases:
  - episodeN
tags: [ravenloft, dementlieu]
---

# Episode N: $ARGUMENTS

## Strong Start
-

## Masks
-

## The Season
- **Invitation progress**:
- **This session's event**:
- **The MacGuffin**:

## Scenes
-

## Locations
-

## NPCs
-

## Secrets and Clues
-

## Encounters
-

## Midnight
-

## Appearances
- **Who's suspicious**:
- **Red Death's attention**:

## Rewards & Favors
-
```

3. Do not overwrite an existing file — if `episodeN.md` already exists, stop and report it.
4. After writing, confirm the path created and the episode number.
