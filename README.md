# TTRPG Dungeon Master Skill

An AI-powered Dungeon Master that ingests any tabletop RPG rulebook and runs a full campaign for solo or co-op players. The primary interface is conversational, with visual elements (maps, character sheets, spatial diagrams) surfacing contextually when they add clarity.

---

## What It Does

This is a **skill factory** — a parent skill that reads your rulebook, parses the mechanics, and dynamically generates the sub-skills needed to run that specific game system. Since all tabletop RPGs share a common skeleton (stats, resolution, combat, advancement), the parser slots in system-specific details rather than building from scratch.

Supported out of the box with any system that has:
- A stat system
- A core resolution mechanic (roll vs. difficulty, opposed checks, etc.)
- A combat structure
- Some form of advancement

Systems tested: Basic Fantasy RPG. Should work with D&D, Pathfinder, Blades in the Dark, Mothership, and similar systems.

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

1. Open a new Claude conversation and attach or paste the contents of `SKILL.md`.
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

The DM operates in a **beat-and-prompt** pattern: one narrative beat per response, then the player acts. Rooms are generated on demand as you approach them — the layout skeleton exists upfront, but individual room files are created the moment you head toward them.

### Ending a Session

Tell Claude the session is over. It will produce:
- A session summary entry for `session-log.md`
- An `updated_character_sheet` with all deltas already applied (copy-paste ready)
- An `updated_inventory` with gains and losses applied
- Companion soul update blocks (one per companion)
- A list of any room files generated this session

You then copy the updated files back into the repo before the next session.

---

## Key Design Features

### Companion System

Persistent party members have a `soul.md` with personality, core belief, current goal, and relationship state. Relationship is tracked on two dimensions:

- **Base level:** distant → neutral → warm → devoted
- **Tension overlay:** none / strained / conflicted (independent of base level)

Companions develop through play — their internal state shifts whether or not the player engages with story beats. Ignored threads accumulate. Under extreme conditions (core belief betrayed, 4+ sessions of ignored threads), companions can withdraw, confront the player, or act independently.

### Dungeon Generation

Uses a **"develop as you go"** model. `layout.md` defines the skeleton upfront (room manifest, connections, threat level, narrative hooks). Individual room files are generated when the player is one move away from entering — keeping context lean and dungeons feeling alive.

### Multi-Location Campaigns

When a dungeon is complete, unresolved hooks and significant NPCs are migrated to `campaign/world-log.md`. This file is the bridge between locations — anything that matters beyond one dungeon lives there.

### Undefined Rules

When a situation isn't covered by `mechanics.md`, the DM first looks for an analogy in the defined system. If none exists, it asks the player how to handle it, then records the ruling in the session log. Improvised rulings are never silent.

---

## What This Does NOT Handle (Prototype Limitations)

- **Dice rolling** — resolve narratively or roll physical dice; results are player-reported
- **File writes** — player copies updated files manually at session end
- **Multiplayer coordination**
- **Rulebook PDF parsing** — paste or describe key rules instead
- **Automated state management** — the DM produces ready-to-copy output; automation is future work

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
| `Basic Fantasy RPG/` | Example campaign using Basic Fantasy RPG |
