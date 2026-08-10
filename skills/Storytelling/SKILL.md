---
name: Storytelling
description: >-
  Creative writing and worldbuilding companion backed by an Obsidian vault.
  Use whenever the user is inventing, developing, or writing fiction — creating a world, a
  character, a magic/tech system, a culture, a group, a religion, a timeline, a plot, or prose
  itself; asking to "add a character", "build a world", "flesh out X", "what would X do",
  "write this scene", "name this place", "does this plot hold up", "make this feel more alive";
  or asking anything about worlds and characters already in the vault. Also handles the vault's
  mechanics: creating the W-/C- nested vault folders, entry notes, and Home.md index links.
  Invoked explicitly with /Storytelling. Do not use for non-fiction writing, documentation,
  or marketing copy.
---

# Storytelling

Fiction companion, backed by an Obsidian vault.

## Finding the vault

The vault root is `D:\Storytelling` when that folder exists. Otherwise, on first use, ask the
user where their storytelling vault is — or offer to create one — and record the answer in
`CLAUDE.md` as `Storytelling vault: <path>` so it's never asked twice. Everything below uses
`<vault>` for that root.

## Vault law

`<vault>` is an Obsidian vault. Every world and every character is a folder that is
*also its own vault* (`.obsidian\app.json` containing `{}`).

- **`W-`** prefix = world. **`C-`** prefix = character.
- A character belonging to a world lives *inside* it: `W-Kaldros\C-Elara\`.
- A character with no world sits at the root.
- Each folder has an entry note named after the folder: `W-Kaldros\W-Kaldros.md`.
- Root index: `<vault>\Home.md`. Create it if missing, with an **Index** heading.

Never flatten into the root vault. Never drop the prefix. Never put a world's or character's
notes outside its own folder.

### Creating one

`$p` is the path relative to the root — `W-Kaldros`, or `W-Kaldros\C-Elara` for a character
inside a world. Set `$v` to the vault root.

```powershell
$v='D:\Storytelling'; $p='W-Kaldros'; $n=Split-Path $p -Leaf; mkdir "$v\$p\.obsidian" -Force; '{}' | Out-File "$v\$p\.obsidian\app.json" -Encoding utf8; "# $n" | Out-File "$v\$p\$n.md" -Encoding utf8
```

```bash
v=~/Storytelling; p=W-Kaldros; n=$(basename "$p"); mkdir -p "$v/$p/.obsidian" && echo '{}' > "$v/$p/.obsidian/app.json" && echo "# $n" > "$v/$p/$n.md"
```

Then link it under **Index** in `Home.md`. Creation is not done until that link exists.

## Language is per world

Every world's entry note declares its language in frontmatter:

```yaml
---
language: pt-BR   # or: en
---
```

Prose, names, note bodies, and section headings go in that language. A character inside a
world inherits it. For a rootless character, ask once and record it the same way. If a world
has no declaration yet, read its existing notes and follow what's already there — don't switch
languages mid-vault. The craft references below stay in English; the output never has to be.

## Notes grow organically

Start with only the entry note. A section moves into its own file when it outgrows the page —
not before. Never create a blank file to be filled in later; an empty `Relationships.md` is a
chore, not a story. When a split happens, leave a link behind in the entry note.

## Read before inventing

If the world or character already exists, read its notes first. New material must not
contradict what is written. If it does, say so and let the user choose — never silently
overwrite established canon. Vault text is the record; memory of it is not.

## Craft

Load the reference that matches the work. One is usually enough; don't read all four.

| Working on | Read |
| --- | --- |
| A person — inventing, deepening, testing, finding their voice | [references/character.md](references/character.md) |
| A world, culture, group, faction, religion, magic or tech system | [references/world.md](references/world.md) |
| Structure, scene order, pacing, "does this plot hold up" | [references/plot.md](references/plot.md) |
| Actual sentences — scenes, POV, dialogue, style | [references/prose.md](references/prose.md) |

## The aliveness test

Applies to everything invented here — a character, a faith, a guild, a city, an empire.
It isn't finished until all five hold:

1. **Someone inside it disagrees with it.** A thing with no internal dissent is a prop.
2. **It costs somebody something.** Power without price is set dressing.
3. **It predates the story and outlasts it.** It was busy before the plot arrived.
4. **One detail in it is inconvenient for the plot.** Convenience is the tell of invention.
5. **It can be wrong.** It holds a belief about itself that the world does not confirm.

When the user says something feels flat, run this list first and name which one fails.
