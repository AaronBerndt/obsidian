---
description: Import a Demiplane Cyberpunk RED character sheet into Cyberpunk/characters
allowed-tools: Bash(curl:*), Bash(python3:*), Bash(ls:*), Read, Write
argument-hint: [demiplane character sheet URL or UUID]
---

Parse a Demiplane Cyberpunk RED character sheet and write it as a markdown character
file in `Cyberpunk/characters/`.

The character URL or bare UUID is in `$ARGUMENTS`. If `$ARGUMENTS` is empty, stop and
ask for one.

## How the data is fetched

Demiplane's sheet is a Next.js app — the rendered HTML is an empty shell, so WebFetch
returns nothing but the page title. **Do not use WebFetch.** The character data ships in
the server-rendered RSC payload embedded in the page source, so a plain `curl` of the
sheet URL gets everything without authentication (as long as the owner has the sheet set
to link-viewable).

Steps:

1. Normalize `$ARGUMENTS` to a full URL. A bare UUID becomes
   `https://app.demiplane.com/nexus/cyberpunkred/character-sheet/<uuid>`.

2. Download the page into the scratchpad directory:

   ```
   curl -s -m 30 "<URL>" > <scratchpad>/demiplane-char.html
   ```

3. Extract the engine key/value pairs with this script (run it via `python3 - <<'EOF'`,
   substituting the real scratchpad path):

   ```python
   import re
   h = open('<scratchpad>/demiplane-char.html').read().replace('\\"', '"')
   pairs = {}
   pat = r'"id":"(custom_[^"]+)"(.{0,400}?)"value":("(?:[^"\\]|\\.)*"|-?[\d.]+|true|false|null)(?=[,}])'
   for m in re.finditer(pat, h, re.S):
       key, middle, val = m.group(1), m.group(2), m.group(3)
       if '"id":"' in middle:   # value belongs to a different engine
           continue
       pairs.setdefault(key, val)
   for k, v in sorted(pairs.items()):
       print(k, '=', v)
   ```

4. If no `custom_character_name` key comes back, the sheet is private. Stop and tell the
   user the owner needs to make it viewable by link.

## Key map

Everything under `custom_character_lifepath_table_*` is lifepath. The general keys are
the same for every character; the last block varies by Role (Medtech shown here — a Solo
sheet has `*_solo_*` keys, a Fixer `*_fixer_*`, and so on, so read whatever lifepath keys
actually came back rather than assuming this list is complete).

| Key fragment | Section |
| --- | --- |
| `cultural-region_input-region` / `_input-languages` | Cultural Origins |
| `your-personality_input-what-are-you-like` | Personality |
| `dress-and-personal-style_input-clothing-style` / `_input-hairstyle` | Dress & Personal Style |
| `affectation-you-are-never-without_*` | Dress & Personal Style |
| `your-motivations-and-relationships_*` | Motivations & Relationships |
| `most-valued-person-in-your-life_*` / `most-valued-possession-you-own_*` | Motivations & Relationships |
| `your-original-family-background_input-original-background` / `_input-description` | Family Background |
| `your-environment_input-childhood-environment` | Family Background |
| `your-family-crisis_input-background` | Family Background |
| `your-friends_set-N_*` | Friends (table) |
| `your-enemies_set-N_*` and `sweet-revenge_set-N_*` | Enemies |
| `your-tragic-love-affairs_set-N_*` | Tragic Love Affairs (table) |
| `your-life-goals_input-life-goals` | Life Goals |
| any other `lifepath_table_*` key | Role-specific lifepath section |

`*_num-sets` gives the number of entries in a repeating group; iterate `set-0` … `set-(n-1)`.

Non-lifepath keys worth including:

- `custom_character_name` — the character name.
- `custom_character_stat_<stat>_value--starting` — STATs. Demiplane names map to
  INT `intelligence`, REF `reflexes`, DEX `dexterity`, TECH `technique`, COOL `cool`,
  WILL `willpower`, LUCK `luck`, MOVE `movement`, BODY `body`, EMP `empathy`.
- `custom_character_skill_<slug>_level--starting` — skills. A skill whose slug is a UUID
  has its display name in a sibling `custom_character_skill_<uuid>_name` key.
- `custom_character_role-ability_<ability>_specialty_<x>_points` — Role ability
  breakdown. The ability name (e.g. `medicine` for Medtech) identifies the Role; the
  points sum to the Role rank.
- `custom_character_avatar` — portrait URL, reference it only if useful.

## Writing the file

Write `Cyberpunk/characters/<FirstName>.md` using the vault's frontmatter convention:

```
---
id: <FirstName>
aliases:
  - <nickname>
tags: []
---
```

Then: an `# <Name>` heading, a Role / source-link line linking back to the Demiplane URL,
a two-or-three sentence prose summary drawn from the lifepath answers, then a
`## Lifepath` section with the subsections in the key-map order above, followed by
`## Stats`, the Role ability section, `## Skills`, and `## Notes`.

Use tables for the repeating groups (Friends, Tragic Love Affairs) and for Stats and
Skills. Sort skills by level descending. Match `Cyberpunk/characters/Salvadore.md` for
formatting.

## Reporting

Demiplane sheets are frequently half-finished, so check for and surface these in the
`## Notes` section of the file and in your reply to the user:

- **Unfilled fields.** A value that repeats its own prompt text (e.g.
  `" What Caused it? Who's been Wronged?"`) was never filled in. Write
  `*(not filled in on the sheet)*` rather than treating it as content.
- **Missing STATs.** Note any STAT with no value instead of silently omitting the row.
- **Stray characters.** Table-derived answers sometimes keep the roll's letter or number
  prefix (e.g. `"e High Fashion (Exclusive, Designer, Couture)"`). Strip it and say so.
- **Contradictions with campaign notes.** Compare friends, enemies, and goals against
  `Cyberpunk/characters.md`; if the sheet disagrees with what's recorded there, flag the
  conflict rather than picking a side.
- **Internal contradictions**, such as a person listed as both a living friend and a dead
  lover.

Do not overwrite an existing character file without confirming with the user first.
