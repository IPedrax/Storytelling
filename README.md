<div align="center">
  <img src="assets/icons/feather.svg" width="56" alt="" />
  <h1>Storytelling</h1>
  <p><strong>A creative writing and worldbuilding companion for Claude — invent characters, worlds, cultures, groups, religions and plots, pressure-test them until they feel inhabited, then write the prose. Kept in an Obsidian vault you own, in each world's own language.</strong></p>
</div>

Most writing assistants generate. Ask for a character and you get a résumé — brave, loyal, quick-witted — and a world that is a map with names on it. **Storytelling** is the craft behind the generation. It builds from causes rather than traits: a wound produces a lie, the lie produces a want, and the want walks into a world whose scarcities produced its gods. Then it argues with what it made, because nothing invented here is finished until it can be wrong.

Grounded in **named craft, researched and cited** — not improvised: the ghost/wound/lie/want/need spine, Sanderson's laws of magic and the hollow iceberg, seven-point structure and the story circle, Swain's scene-and-sequel, try-fail cycles, Gardner's psychic distance, free indirect discourse, and the anthropology of production/distribution/consumption.

Built for **Claude Code** (Windows / macOS / Linux).

---

## <img src="assets/icons/check.svg" width="20" align="absmiddle" alt="" /> The aliveness test

The spine of the whole skill. It applies to everything invented — a character, a faith, a guild, a city, an empire — and nothing is finished until all five hold:

1. **Someone inside it disagrees with it.** A thing with no internal dissent is a prop.
2. **It costs somebody something.** Power without price is set dressing.
3. **It predates the story and outlasts it.** It was busy before the plot arrived.
4. **One detail in it is inconvenient for the plot.** Convenience is the tell of invention.
5. **It can be wrong.** It holds a belief about itself that the world does not confirm.

Say a character feels flat and the skill doesn't reassure you — it runs the list and names which one fails.

---

## <img src="assets/icons/layers.svg" width="20" align="absmiddle" alt="" /> The craft

A small router loads exactly one reference for the work in front of it, never all four.

| Working on | Reference | What's in it |
|---|---|---|
| **A person** | [`character.md`](skills/Storytelling/references/character.md) | Ghost → wound → lie → want vs need · arc shapes · the professed-identity-vs-verified-action gap · four voice dials · interiority and subtext · relationships cast off the wound |
| **A world** | [`world.md`](skills/Storytelling/references/world.md) | The hollow iceberg · Sanderson's four laws past magic · culture derived from material conditions · factions by want/leverage/constraint/fracture · religion built function-first, with schism · naming · history as scars |
| **Structure** | [`plot.md`](skills/Storytelling/references/plot.md) | The *and-then / therefore / but* causality test · seven-point placement · story circle · try-fail as *yes-but* / *no-and* · scene and sequel · promise-progress-payoff · a ten-step "does this hold up" stress test |
| **Sentences** | [`prose.md`](skills/Storytelling/references/prose.md) | Gardner's five psychic distances · filter words · free indirect discourse · show/tell as a real rule · dialogue subtext · rhythm · revision checklist |

---

## <img src="assets/icons/sparkles.svg" width="20" align="absmiddle" alt="" /> What it does

- **Builds from causes, not adjectives.** A character starts at the event that broke them and ends at the lie they still believe; a culture starts at what the land makes scarce and ends at what that arrangement needs people to believe. Traits are outputs, never inputs.
- **Argues with your world.** It runs the aliveness test, the causality test, the antagonist-plan test and the coincidence audit, and tells you which beat is an *"and then"*. Agreement is not the product.
- **Refuses to overbuild.** Sanderson's Third Law is enforced: expand what exists before adding something new, and build nothing the story hasn't asked for. Open questions get parked in an **Open** section instead of answered with filler — worldbuilder's disease is a failure mode the skill is written against.
- **Writes in your world's language.** Each world declares `language: pt-BR` or `en` in its entry note and everything inside inherits it — prose, names, headings. The craft references stay English; the page never has to be.
- **Models the web, not a tree.** Twelve entity types linked through flat frontmatter, so people, houses, orders, faiths, places and events form an actual graph you can query and walk. Each connection is written once and read from both ends, which is why the vault can't quietly contradict itself about who is whose brother.
- **Keeps notes organic.** One note per entity, growing into a folder only when a section genuinely outgrows the page. No template folders full of blank `Relationships.md` files waiting to shame you.
- **Never overwrites canon.** It reads what exists before inventing, and when new material contradicts what's written it says so and lets you choose. The vault is the record; recollection is not.
- **Lean by design.** The router is short and the four references load only when the work calls for them, so the skill is deep without eating your context up front.

---

## <img src="assets/icons/globe.svg" width="20" align="absmiddle" alt="" /> The vault

Notes live in plain markdown in an Obsidian vault you own, and the design turns on one rule: **folders say where a thing lives, links say what it has to do with anything.** Nesting is one-parent and permanent; connection is many-to-many and changes. Only the first is a folder — which is why a character can belong to a family, two guilds, a faith and a city at once without any of them owning her.

Twelve prefixed entity types, flat inside their world:

| | | | |
|---|---|---|---|
| `W-` world | `C-` character | `N-` NPC | `G-` group |
| `F-` family | `A-` ancestry | `P-` place | `R-` religion |
| `E-` event | `T-` thing | `B-` bond | `S-` scene |

```
Storytelling/
├── .obsidian/                  root vault — sees everything
├── Home.md                     index of worlds
└── W-Kaldros/                  a world…
    ├── .obsidian/              …and its own vault
    ├── W-Kaldros.md            entry note, declares language: pt-BR
    ├── C-Elara/                main cast — a vault of her own
    │   ├── .obsidian/
    │   └── C-Elara.md
    ├── N-Doorkeeper.md         an NPC — just a note
    ├── G-Silent-Order.md       an order she serves
    ├── F-Vashti.md             the house she was born to
    ├── B-Elara-and-Marek.md    eleven years, one betrayal, still allies
    └── S-01-The-Letter.md      the manuscript itself
```

Everything starts as a **single note** and becomes a folder only when it outgrows the page — Obsidian resolves wikilinks by name rather than path, so growing a note into a folder breaks nothing. Renaming does the same work in reverse: promote `N-Doorkeeper` to `C-Doorkeeper` and every link in the vault repoints itself.

Structure lives in **flat frontmatter properties** (`family:`, `member_of:`, `faith:`, `located_in:`) so Obsidian Bases can query it, and the graph view draws the whole web. Each edge is written **once**, on the dependent side: a character lists her orders, an order never lists its members — backlinks give it a live roster that can't drift out of sync with the truth. The two connections that *are* symmetric get a note of their own instead: an `E-` event for the night it happened, a `B-` bond for a relationship still running.

On first run the skill asks where your vault is and records the answer, so it only asks once. Obsidian is optional — it's markdown in folders either way.

---

## <img src="assets/icons/download.svg" width="20" align="absmiddle" alt="" /> Install

### <img src="assets/icons/terminal.svg" width="17" align="absmiddle" alt="" /> Claude Code — any platform

```bash
claude plugin marketplace add IPedrax/Storytelling
```

```bash
claude plugin install storytelling@storytelling
```

### <img src="assets/icons/monitor.svg" width="17" align="absmiddle" alt="" /> From a local clone

```bash
claude plugin marketplace add ./Storytelling && claude plugin install storytelling@storytelling
```

> **Restart Claude Code after installing**, then `/Storytelling` is available and the skill auto-triggers on fiction requests.

> **Prefer to let Claude install it?** Paste this into a new chat:
> *"Install this Claude Code plugin for me from https://github.com/IPedrax/Storytelling and walk me through anything you need."*

---

## <img src="assets/icons/chat.svg" width="20" align="absmiddle" alt="" /> How to use it

Just describe the fiction, and let it route:

- *"build me a world where the only fresh water is underground"*
- *"why does Elara feel flat?"*
- *"give this order of knights a schism"*
- *"what would he actually say here — he can't admit he was there"*
- *"does this plot hold up?"*
- *"write the scene where she finds the letter"*

Or go straight in:

```
/Storytelling                          picks up whatever is open in the vault
/Storytelling new world                creates the folder, the vault, the entry note, the index link
/Storytelling C-Elara                  loads a character and works on them
```

---

## <img src="assets/icons/settings.svg" width="20" align="absmiddle" alt="" /> How it works

**Find the vault → read what exists → pick the craft reference → build from causes → run the aliveness test → write it into the vault.**

`SKILL.md` is a router, not a manual. It carries the vault rules, the per-world language rule, the organic-notes rule and the aliveness test, then loads a single reference for the job at hand. Reading precedes inventing every time: established canon in the vault outranks anything the model remembers, and a contradiction is surfaced rather than resolved silently.

```
skills/Storytelling/
├── SKILL.md              router: vault law, language, organic notes, the aliveness test
└── references/           loaded on demand, one per craft domain
    ├── character.md      spine, arcs, contradiction, voice, interiority, subtext, casts
    ├── world.md          hollow iceberg, systems, culture, factions, religion, naming, history
    ├── plot.md           causality, turning points, try-fail, scene/sequel, stress tests
    └── prose.md          psychic distance, filtering, FID, dialogue, rhythm, revision
```

---

## <img src="assets/icons/check.svg" width="20" align="absmiddle" alt="" /> Verify

```bash
claude plugin validate .
```

---

## <img src="assets/icons/file.svg" width="20" align="absmiddle" alt="" /> License

Storytelling is [MIT](LICENSE).

The craft frameworks it references — Sanderson's laws, Gardner's psychic distance, Dan Wells' seven points, Swain's scene and sequel, the story circle, and the ghost/lie/want/need model as popularized by K.M. Weiland — belong to their authors and are cited, not reproduced.
