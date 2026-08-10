---
name: Storytelling
description: >-
  Creative writing and worldbuilding companion backed by an Obsidian vault.
  Use whenever the user is inventing, developing, or writing fiction: creating a world, a
  character or NPC, a group, guild, order or faction, a family or bloodline, a people or species,
  a place, a religion, a historical event, an artifact, a magic or tech system, a relationship
  between two characters, a plot, or prose itself;
  asking to "add a character", "add an NPC", "build a world", "who runs this city",
  "flesh out X", "what would X do", "how are these two connected", "write this scene",
  "does this plot hold up", "make this feel more alive"; or asking anything about entities
  already in the vault. Also handles the vault's mechanics: the prefixed entity notes, the
  frontmatter link graph, nested vaults, and index links. Invoked explicitly with /Storytelling.
  Do not use for non-fiction writing, documentation, or marketing copy.
---

# Storytelling

Fiction companion, backed by an Obsidian vault.

## Finding the vault

The vault root is `D:\Storytelling` when that folder exists. Otherwise, on first use, ask the
user where their storytelling vault is (or offer to create one), and record the answer in
`CLAUDE.md` as `Storytelling vault: <path>` so it's never asked twice. Everything below uses
`<vault>` for that root.

## Two jobs, two mechanisms

**Folders say where a thing lives. Links say what it has to do with anything.**

Keep these separate and the vault scales. Mix them, put a character inside a guild folder, and
the first character who joins two guilds, or leaves one, breaks the structure. Containment is
one-parent and permanent; connection is many-to-many and changes. Only the first is a folder.

## Entities

Every entity is a prefixed note. The prefix is part of the filename, so `[[C-Elara]]` is
unambiguous in a link and entities of a kind sort together.

| Prefix | Type | What it is |
| --- | --- | --- |
| `W-` | world | The container. Everything else sits inside one. |
| `C-` | character | Main cast. Carries a full spine and an arc. |
| `N-` | NPC | Everyone else: recurring minor, or a one-scene walk-on. |
| `G-` | group | An organization: guild, order, crew, company, faction, army, court. |
| `F-` | family | A bloodline: house, clan, dynasty. Kinship, not employment. |
| `A-` | ancestry | A people: species, culture, nation, caste: what someone *is*, not what they joined. |
| `P-` | place | City, region, building, road, room: anywhere something happens. |
| `R-` | religion | The *faith*: doctrine, practice, cosmology. Its church is a `G-`. |
| `E-` | event | Something that happened: war, schism, founding, murder, marriage. |
| `T-` | thing | Artifact, magic or tech system, language, law, disease, ship. |
| `B-` | bond | A relationship that carries its own story: a rivalry, a marriage, a debt. |
| `S-` | scene | The manuscript itself: a written scene or chapter. |

Nothing here is a hierarchy. A character holds a `family`, an `ancestry`, three `member_of`
groups, a `faith`, and a `located_in` place at once, and none of them owns them.

**Names**: prefix, then hyphens inside the name: `G-Silent-Order`, `E-The-Sundering`. Shell-safe
and readable in a link.

**`C-` vs `N-` is depth, and it is not a life sentence.** When a doorkeeper starts pulling scenes
toward them, rename `N-Doorkeeper` to `C-Doorkeeper`, and Obsidian rewrites every `[[N-Doorkeeper]]`
in the vault automatically. Promote when the story shows you where the energy is, never in
advance. Craft differences between the tiers: [references/character.md](references/character.md).

## Structure

Flat inside a world. One folder per world; every entity of that world sits directly in it.

```
<vault>/
├── Home.md                     index of worlds only
├── W-Kaldros/
│   ├── .obsidian/app.json      a world is its own vault
│   ├── W-Kaldros.md            entry note
│   ├── C-Elara/                main cast: folder + vault
│   │   ├── .obsidian/app.json
│   │   └── C-Elara.md
│   ├── N-Doorkeeper.md         an NPC: just a note
│   ├── G-Silent-Order.md
│   ├── F-Vashti.md
│   ├── A-Highlanders.md
│   ├── P-Highreach.md
│   ├── R-The-Ledger.md
│   ├── E-The-Sundering.md
│   ├── T-Thousand-Keys.md
│   ├── B-Elara-and-Marek.md
│   └── S-01-The-Letter.md
└── C-Wanderer.md               no world yet: sits at the root
```

**Everything starts as a single note.** It becomes a folder only when it outgrows the page:
`G-Silent-Order.md` → `G-Silent-Order/G-Silent-Order.md` plus the split-off files. Obsidian
resolves wikilinks **by name, not path**, so promoting a note to a folder does not break a single
`[[G-Silent-Order]]` anywhere in the vault. That is what makes growing organically safe.

**Nested vaults** (`.obsidian\app.json` containing `{}`) go on `W-` worlds and `C-` main cast,
the two things opened standalone. Not on every note; a hundred `.obsidian` folders is upkeep with
no payoff.

### Creating

A world is the only thing that needs a command. `$v` is the vault root.

```powershell
$v='D:\Storytelling'; $n='W-Kaldros'; mkdir "$v\$n\.obsidian" -Force; '{}' | Out-File "$v\$n\.obsidian\app.json" -Encoding utf8; "# $n" | Out-File "$v\$n\$n.md" -Encoding utf8
```

```bash
v=~/Storytelling; n=W-Kaldros; mkdir -p "$v/$n/.obsidian" && echo '{}' > "$v/$n/.obsidian/app.json" && echo "# $n" > "$v/$n/$n.md"
```

Then link it under **Index** in `Home.md`; a world is not created until that link exists.
Everything else is just a `.md` file written into the world's folder.

## The link graph

Obsidian resolves `[[links]]` in frontmatter as real edges, so the graph view and backlinks show
the whole web. Four rules keep it honest.

**1. Frontmatter carries structure. The body carries the story.**

Frontmatter says *that* Elara belongs to the Silent Order. The body says she joined at fourteen
to escape her mother and has never once said so out loud. Both are edges; only one has meaning.

**2. Properties stay flat.** No nesting, ever, because Obsidian Bases can only filter flat properties,
and a nested `relations:` map is invisible to every query you would want to run.

```yaml
---
type: character
world: "[[W-Kaldros]]"
ancestry: "[[A-Highlanders]]"
family: "[[F-Vashti]]"
member_of: ["[[G-Silent-Order]]", "[[G-Nightpost]]"]
faith: "[[R-The-Ledger]]"
located_in: "[[P-Highreach]]"
status: alive
language: pt-BR
---
```

Common keys by type, all optional and all flat:

| Type | Keys |
| --- | --- |
| character | `world` · `ancestry` · `family` · `member_of` · `faith` · `located_in` · `status` |
| NPC | same as character, plus `tier` (`minor` · `background`) and `function`, what they're for |
| group | `kind` · `world` · `seat` · `head` · `faith` · `rivals` · `founded` |
| family | `world` · `seat` · `head` · `status` |
| ancestry | `world` · `kind` · `homeland` |
| place | `kind` · `world` · `within` · `held_by` |
| religion | `world` · `centre` · `schism_of` |
| event | `world` · `when` · `where` · `involved` |
| thing | `kind` · `world` · `held_by` · `origin` |
| bond | `world` · `between` · `kind` · `temperature` (warming · cooling · frozen · breaking) |
| scene | `world` · `pov` · `where` · `involved` · `status` (draft · revised · final) |

**3. Write each edge once, on the dependent side, never both.**

A character lists their groups. A group does **not** list its members. Membership changes from the
person's end, and Obsidian's backlinks give the group a live roster for free. Write it twice and
the two copies drift until one of them is a lie.

The exception is *leadership*, which is about the group's own shape and belongs on the group
(`head`, `leads`). Everything else: dependent side only. Never hand-maintain a roster; if the
group note wants one visible, that is the backlinks pane or a Bases view, not typed text that rots.

**4. Grade the connection, then pick its home.** Most of the work is picking the right one:

| Grade | Example | Where it lives |
| --- | --- | --- |
| **Structural** | She is in the Order. | One frontmatter key. Nothing more. |
| **Meaningful** | She distrusts the Master of Keys. | One line in her body, with the why. |
| **It happened** | The night he sold her name to the Ledger. | An `E-` event both link to. |
| **It's ongoing and load-bearing** | Elara and Marek: eleven years, one betrayal, still allies. | A `B-` bond note. |

The last two exist because **a relationship written on both sides will disagree with itself.**
Symmetric connections are the one case where the edge does *not* go on a dependent side. It goes
on a third note that both point at. The `E-` holds a moment; the `B-` holds a history that is
still running. Both give every participant their story back through backlinks, told once.

Use a `B-` only when the relationship has a shape of its own: a rivalry with rounds, a marriage
with terms, a debt with a clock. Two people who simply know each other do not need a note; that's
a line in a body.

## The connection test

Structural sibling of the aliveness test, run on the graph rather than the content:

- **No inbound links**: nothing references it, so it isn't in the world yet. It's a draft.
- **Only outbound links**: it knows about the world; the world doesn't know about it. Scenery.
- **Linked only to its world**: floating. Every entity should touch at least one thing that
  isn't its container.
- **Before editing any note, read its backlinks.** That is where contradictions live: what other
  notes have already claimed about this one.

## Language is per world

Every world's entry note declares its language in frontmatter:

```yaml
language: pt-BR   # or: en
```

Prose, names, note bodies, and section headings go in that language. Everything inside the world
inherits it. For a rootless entity, ask once and record it the same way. If a world has no
declaration yet, read its existing notes and follow what's there; don't switch languages
mid-vault. The craft references stay English; the output never has to be.

## Notes grow organically

Start with only the entry note. A section moves into its own file when it outgrows the page, not
before. Never create a blank file to be filled in later; an empty `Relationships.md` is a chore,
not a story. When a split happens, leave a link behind.

The same rule governs entities themselves: a name mentioned in passing is a name, not a note.
Give it a note when something needs to point at it.

## Read before inventing

If the entity already exists, read its note *and its backlinks* first. New material must not
contradict what is written. If it does, say so and let the user choose; never silently overwrite
established canon. Vault text is the record; memory of it is not.

## Craft

Load the reference that matches the work. One is usually enough; don't read all four.

| Working on | Read |
| --- | --- |
| `C-` `N-` `B-`: a person, their depth, their voice, who they're bound to | [references/character.md](references/character.md) |
| `W-` `G-` `F-` `A-` `P-` `R-` `E-` `T-`: the world and everything standing in it | [references/world.md](references/world.md) |
| Structure, scene order, pacing, "does this plot hold up" | [references/plot.md](references/plot.md) |
| `S-`: actual sentences: POV, dialogue, style | [references/prose.md](references/prose.md) |
| Revising drafted prose so it doesn't read as machine-written | [references/humanize.md](references/humanize.md) |

**Prose is never delivered on the first pass.** After writing any `S-` scene or any stretch of
narrative, run [references/humanize.md](references/humanize.md) over it before showing it to the
user. A model's default output is the statistical average of everything ever written, and that
average has a recognizable smell. The pass is what removes it.

## The aliveness test

Applies to everything invented here: a character, a faith, a guild, a family, a city, an empire.
It isn't finished until all five hold:

1. **Someone inside it disagrees with it.** A thing with no internal dissent is a prop.
2. **It costs somebody something.** Power without price is set dressing.
3. **It predates the story and outlasts it.** It was busy before the plot arrived.
4. **One detail in it is inconvenient for the plot.** Convenience is the tell of invention.
5. **It can be wrong.** It holds a belief about itself that the world does not confirm.

When the user says something feels flat, run this list first and name which one fails.
