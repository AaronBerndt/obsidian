---
description: Scaffold the next Cyberpunk RED episode in Cyberpunk/episodes
allowed-tools: Bash(ls:*), Write
argument-hint: [episode title]
---

Create a new, blank episode file for the Cyberpunk RED campaign.

Steps:
1. Determine the next episode number by listing `Cyberpunk/episodes/`, finding the
   highest existing `episodeN.md` (ignore `pilot.md`), and adding 1. Call this `N`.
   If no numbered episodes exist yet, `N` is 1.
2. Create `Cyberpunk/episodes/episodeN.md` with exactly this content (substitute `N`,
   and use the title from `$ARGUMENTS` after the colon — leave it blank if none was given):

```
---
id: cyberpunk_episodeN
aliases:
  - episodeN
tags: []
---

# Episode N: $ARGUMENTS

## Characters

## The Gig
- **Fixer / Client**:
- **Pay**:
- **The Job**:

## Scenes
-

## Locations
-

## Secrets and Clues
-

## Opposition
-

## Loot & Payout
-

## Heat
-
```

3. Do not overwrite an existing file — if `episodeN.md` already exists, stop and report it.
4. After writing, confirm the path created and the episode number.
