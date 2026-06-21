---
description: Scaffold the next D&D campaign episode in Legacy/episodes
allowed-tools: Bash(ls:*), Write
argument-hint: [episode title]
---

Create a new, blank episode file for the campaign.

Steps:
1. Determine the next episode number by listing `Legacy/episodes/`, finding the
   highest existing `episodeN.md` (ignore `pilot.md`), and adding 1. Call this `N`.
2. Create `Legacy/episodes/episodeN.md` with exactly this content (substitute `N`,
   and use the title from `$ARGUMENTS` after the colon — leave it blank if none was given):

```
---
id: legacy_episodeN
aliases:
  - episodeN
tags: []
---

# Episode N: $ARGUMENTS

## Characters

## Scenes
-

## Locations
-

## Secrets and Clues
-
```

3. Do not overwrite an existing file — if `episodeN.md` already exists, stop and report it.
4. After writing, confirm the path created and the episode number.
