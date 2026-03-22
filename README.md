# TTRPG Dungeon Master Skill

An AI-powered Dungeon Master that ingests any tabletop RPG rulebook and runs a full campaign for solo or co-op players. The primary interface is conversational, with visual elements (maps, character sheets, spatial diagrams) surfacing contextually when they add clarity.

This project contains the system-agnostic skill files only. Campaign files generated from specific rule books (character sheets, dungeon layouts, session logs, etc.) are intentionally excluded from this repo.

---

## What It Does

This is a **skill factory** — a parent skill that reads your rulebook, parses the mechanics, and dynamically generates the sub-skills needed to run that specific game system. Since all tabletop RPGs share a common skeleton (stats, resolution, combat, advancement), the parser slots in system-specific details rather than building from scratch.

Supported with any system that has:
- A stat system
- A core resolution mechanic (roll vs. difficulty, opposed checks, etc.)
- A combat structure
- Some form of advancement

Systems tested: Basic Fantasy RPG. Designed to work with D&D, Pathfinder, Blades in the Dark, Mothership, and similar systems.

---

## File Structure

```
/dungeon-master/
├── SKILL.md                        ← Parent routing skill (start here)
├── dm_skill.md                     ← Companion soul update rules
├── campaign/
│   └── world-log.md                ← Cross-dungeon persistent state
├── rulebook/
│   ├── mechanics.md                ← Parsed rules (generated at setup)
│   └── sub-skills/
│       └── [mechanic-name].md      ← Generated sub-skills, one per domain
├── dungeons/
│   └── [dungeon-name]/
│       ├── layout.md               ← Broad structure and room manifest
│       ├── rooms/
│       │   └── [room-name].md      ← Generated as the player approaches
│       └── session-log.md          ← Persistent session record
├── player/
│   ├── character-sheet.md
│   └── inventory.md
└── companions/
    └── [companion-name]/
        ├── soul.md                 ← Personality, goals, beliefs, current state
        ├── character-sheet.md
        └── inventory.md
```

**Format templates** (in the repo root — used when generating any file):

| File to generate | Template |
|---|---|
| campaign/world-log.md | world_log_md_format.md |
| rulebook/mechanics.md | mechanics_md_format.md |
| rulebook/sub-skills/[name].md | generated_skill_format.md |
| dungeons/[name]/layout.md | layout_md_format.md |
| dungeons/[name]/rooms/[name].md | room_md_format.md |
| dungeons/[name]/session-log.md | session_log_md_format.md |
| player/character-sheet.md | character_sheet_md_format.md |
| player/inventory.md | inventory_md_format.md |
| companions/[name]/soul.md | soul_md_format.md |

---

## How to Use It

### First Time Setup

1. Open a new Claude conversation and attach or paste the contents of `SKILL.md` and `dm_skill.md`.
2. Tell Claude you want to start a new campaign and provide your rulebook — either paste the key mechanics or describe them from memory. (PDF parsing is a future feature; for now, text or description works.)
3. Claude will:
   - Parse the rulebook into `rulebook/mechanics.md`
   - Generate system-specific sub-skills (at minimum: `combat_resolution` and `skill_checks`)
   - Walk you through character creation → `player/character-sheet.md` and `player/inventory.md`
   - Ask if you want AI companion party members (each gets a `soul.md`, character sheet, and inventory)
   - Ask for a scenario or offer to generate one
   - Generate the first dungeon's `layout.md` and initialize `session-log.md`

### Starting a Session

Load the following files into context at session start:
- `SKILL.md` and `dm_skill.md`
- The last 2–3 entries from `session-log.md`
- The current dungeon's `layout.md`
- Your `character-sheet.md` and `inventory.md`
- Any companion `soul.md` files

Claude will validate your character state against the last session log (flagging any discrepancies), then give you a brief recap and ask where you want to begin.

### During Play

The DM operates in a **beat-and-prompt** pattern: one narrative beat per response, then the player acts. Most of the time responses are tight — 2–4 sentences of narration plus a prompt. For genuinely dramatic moments (boss defeats, near-death, irreversible choices, long-awaited revelations) the DM expands into a fuller cinematic beat before handing control back.

**Player prompts** — at decision points, the DM offers lettered shorthand options:

```
A. Draw your sword and step into the room.
B. Call out to see if anyone is inside.
C. Back away and find another route.
Z. Something else — tell me what you do.
```

Z is always the open-ended option. Type a letter to choose, or type freely for anything not listed.

**Narration** — the DM always refers to your character as "you" in story mode. Technical information (room IDs, stat values, file names, roll numbers) never appears in narration — rooms are described by what they are, not their tracking ID. That information is only surfaced OOC when you ask for it.

**Player dialogue** — any spoken dialogue you include will be echoed back with a "you say" attribution before the scene continues.

**Out-of-character (OOC) communication** — wrap anything in parentheses `( )` to speak to the DM outside the fiction. The DM replies in parentheses and resumes play after.

```
(Wait, did I already use my spell today?)
(Yes — you cast Light in R02 at the start of the session. You're out until you rest.)
```

The DM can remind you of past events, clarify rules, and confirm your current character state OOC. It will not reveal undiscovered room content, enemy stats, DM secrets, or future plot details.

**Skill checks (out of combat)** — before any out-of-combat roll, the DM tells you what stat or skill applies, the difficulty, any situational modifiers, and what's at stake — before asking for the roll.

**Combat** — uses a declare-confirm-resolve loop. You can play mechanically ("I attack with my sword, I rolled a 14") or narratively ("I want to shove him into the brazier") — the DM translates narrative intent into mechanics and confirms what it means before resolving. Nothing in combat resolves without your confirmation first.

**Dice rolls** — the DM handles all rolls inline. Player rolls are shown fully:

```
🎲 1d20 → 14 + 3 (STR) = 17 vs. Difficulty 14 — Success
```

DM rolls (enemy attacks, secret perception checks, trap triggers, NPC deception) are generated but not shown — only the narrative outcome is narrated. All DM rolls are logged to `session-log.md` and you can ask OOC to see any of them once the relevant scene is resolved.

**File maintenance** — the DM keeps all campaign files current throughout play. You do not track state or apply deltas manually. As events happen the DM silently updates:
- `character-sheet.md` — HP, XP, conditions, resources
- `inventory.md` — items gained, consumed, lost, currency
- `companions/[name]/character-sheet.md` and `inventory.md`
- `layout.md` — room statuses as you approach, enter, clear, or alter rooms; new connections and discovered areas added as they are found
- `rooms/[name].md` — generated when you move toward an unvisited room; alteration logs updated when you change a space
- `session-log.md` — compact milestone entries after combat, significant NPC interactions, companion moments, and major decisions; DM roll audit log

You can ask OOC at any time to see the current state of any file.

### Ending a Session

Tell Claude the session is over whenever you want to stop. The DM will:
1. Reconcile all files against the session's milestone notes — correcting any discrepancies silently
2. Update each active companion's `soul.md` with any state changes from this session
3. Write the full narrative session summary to `session-log.md`
4. Update the Running Tracker (advancement, open hooks, significant NPCs, world-state changes)
5. Update `campaign/world-log.md` if anything this session has consequences beyond the current dungeon

---

## Key Design Features

### Active File Management

The DM owns all campaign files during play. Character sheets, inventories, dungeon layouts, and room files are updated at the moment changes occur — not batched to session end. Session end is a reconciliation and summary step, not a data-entry step.

### Dungeon Generation

Uses a **"develop as you go"** model. `layout.md` defines the skeleton upfront (room manifest, connections, threat level, narrative hooks). Individual room files are generated the moment you move toward an unvisited room. Newly discovered connections and unexpected dungeon depth are added to `layout.md` as they are found.

### Dice Rolling and Auditing

All dice are rolled by the DM inline. Player rolls are fully visible. DM rolls for sensitive information (enemy attacks, secret checks) are withheld at the time but logged to an append-only audit trail in `session-log.md`. You can request to see any DM roll OOC once the scene is resolved.

### Companion System

Companions are fully built player characters controlled by the DM — not followers or assistants. They have complete character sheets (proper stats, class abilities, equipment) and act as co-protagonists with their own goals, opinions, and story arcs.

**Creation** — two paths:
- **Full character creation:** the player makes all the choices for the companion (class, stats, abilities, gear) using the same process as their own character. soul.md is then built to match.
- **Imported sheet:** the player provides a pre-built character sheet; the DM generates soul.md to match.

No companion enters play with placeholder stats.

**In combat** — the DM runs companion turns automatically each round using their actual class abilities and tactical tendencies defined in `soul.md`. A cleric heals when it matters and turns undead when it's called for. A thief flanks. A fighter holds the line.

**Outside combat** — companions are not passengers. They notice things relevant to their class, pursue their own goals, form opinions on player decisions before the player acts, and initiate story beats.

**Character development** — tracked on two dimensions in `soul.md`:

- **Base level:** distant → neutral → warm → devoted
- **Tension overlay:** none / strained / conflicted (independent of base level)

Companions develop whether or not you engage with story beats. Ignored threads accumulate. Under extreme conditions (core belief betrayed, 4+ sessions of ignored threads), companions can withdraw, confront you, or act independently.

### Cinematic Moments

Most play uses tight 2–4 sentence pacing. For genuinely significant moments — boss defeats, near-death, irreversible high-stakes choices, long-awaited revelations — the DM expands into a fuller cinematic beat with sensory detail, world reaction, and deliberate rhythm. These moments are reserved, not routine.

### Multi-Location Campaigns

When a dungeon is complete, unresolved hooks and significant NPCs are migrated to `campaign/world-log.md` — the bridge between locations that preserves continuity across the full campaign.

### Undefined Rules

When a situation isn't covered by `mechanics.md`, the DM looks for an analogy in the defined system first. If none exists, it asks the player how to handle it, then records the ruling in the session log. Improvised rulings are never silent.

---

## What This Does NOT Handle

- **Multiplayer coordination**
- **Rulebook PDF parsing** — paste or describe key rules instead

---

## Repository Contents

| File | Purpose |
|---|---|
| `SKILL.md` | Parent DM skill — the main entry point |
| `dm_skill.md` | Rules for updating companion soul.md files |
| `generated_skill_format.md` | Template for generated sub-skills |
| `mechanics_md_format.md` | Template for parsed rulebook mechanics |
| `character_sheet_md_format.md` | Template for character sheets |
| `inventory_md_format.md` | Template for inventory files |
| `layout_md_format.md` | Template for dungeon layouts |
| `room_md_format.md` | Template for individual room files |
| `session_log_md_format.md` | Template for session logs |
| `soul_md_format.md` | Template for companion soul files |
| `world_log_md_format.md` | Template for the cross-dungeon world log |
| `Design_Summary.md` | Architecture decisions and open questions |
