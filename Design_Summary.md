# Tabletop RPG Dungeon Master Skill — Design Summary

## Core Concept

A flexible, AI-powered Dungeon Master that ingests any tabletop RPG rulebook and runs a full game experience for solo or co-op players. The primary interface is conversational, with visual elements (maps, character sheets, diagrams) surfacing contextually when they add clarity.

---

## Architecture: Skill Factory Model

The parent skill is a **router**. On setup, it:
1. Ingests the rulebook
2. Parses the mechanics and identifies system-specific rules
3. Dynamically generates the sub-skills needed for that particular game system

Since all tabletop RPGs share a universal skeleton, the parser slots in system-specific details rather than building from scratch.

---

## File System Structure

```
/dungeon-master/
├── SKILL.md                  # Parent routing skill
├── campaign/
│   └── world-log.md          # Cross-dungeon state and narrative hooks
├── rulebook/
│   └── mechanics.md
├── dungeons/
│   └── [dungeon-name]/
│       ├── layout.md
│       ├── rooms/
│       └── session-log.md
├── player/
│   ├── character-sheet.md
│   └── inventory.md
└── companions/
    └── [companion-name]/
        ├── soul.md
        ├── character-sheet.md
        └── inventory.md
```

---

## Dungeon Generation

Uses a **"develop as you go"** model — broad structural template upfront, room details filled in as the player approaches. Spatial questions reference already-generated layouts and surface visual diagrams.

---

## Companion System

Persistent party members with defined personality, goals, beliefs, and internal state. Character development surfaces through atmosphere and description. Ignored story beats still affect the companion's internal state in the background.

Relationship is tracked on two dimensions: a base level (distant → neutral → warm → devoted) and an independent tension overlay (none / strained / conflicted). Companions can leave the party under extreme conditions — see dm_skill.md for departure rules.

---

## Persistence Layer

| Entity | What Persists |
|---|---|
| Player | Stats, inventory, XP, backstory |
| Companions | Soul state, goals, beliefs, relationship + tension, inventory |
| Dungeons | Layout, cleared rooms, unresolved encounters |
| World | Key NPCs, quests, lore, cross-dungeon state (world-log.md) |

---

## Setup Phase

1. User provides rulebook (pasted text or described from memory)
2. Skill parses core mechanics into mechanics.md
3. Generates system-specific sub-skills (minimum: combat_resolution, skill_checks)
4. Walks through character creation
5. Optionally creates companion party members with soul.md files
6. Establishes campaign setting and scenario
7. Generates initial dungeon layout

---

## Design Decisions (Resolved)

| Question | Decision | Reference |
|---|---|---|
| Can companions leave the party? | Yes — requires direct belief betrayal or 4+ sessions of ignored threads | dm_skill.md → Conflict and departure rules |
| Spatial diagrams format | ASCII art for reliability; zone-based by default, grid optional for complex rooms | SKILL.md → Visual Aids |
| Rulebook input format | Pasted text or player description (prototype); PDF parsing deferred to future version | SKILL.md → Setup Phase |
| Co-op multiplayer | Not supported in prototype; listed as future work | SKILL.md → What This Skill Does NOT Handle |

---

## Open Questions (Active)

- How should world-level state persist across multiple dungeons? (world-log.md is proposed but not yet templated)
- Should the DM produce complete updated character files at session end instead of deltas?
- Token budget targets per context type for context window management
- Automated state management sub-skill design (currently manual)
