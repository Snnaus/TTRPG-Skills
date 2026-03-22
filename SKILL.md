---
name: ttrpg-dungeon-master
description: >
  AI-powered Dungeon Master for tabletop RPGs. Use this skill whenever the user
  wants to play a TTRPG, run a campaign session, create a character for an RPG,
  generate a dungeon or encounter, manage companion NPCs, or anything involving
  tabletop roleplaying games such as D&D, Pathfinder, Blades in the Dark, Mothership,
  or similar systems. Also trigger when the user references dungeon-master files
  (mechanics.md, soul.md, layout.md, session-log.md, character-sheet.md) or asks
  to resume a campaign.
---

# SKILL.md — Tabletop RPG Dungeon Master (Parent Skill)

## Purpose

This is the parent routing skill for an AI-powered Dungeon Master. It ingests a
tabletop RPG rulebook and a scenario, then orchestrates all sub-skills needed to
run a full campaign for one or two players. The primary interface is
conversational. Visual elements (maps, character sheets, spatial diagrams) are
surfaced contextually when they add clarity.

---

## Skill Architecture

This skill acts as a router. It does not handle game mechanics directly — it
delegates to sub-skills. Multiple games and campaigns can run concurrently —
each gets its own `{Game Name} Rules/` folder at the root level.

```
/
├── SKILL.md                        ← you are here (system-agnostic)
├── dm_*.md                         ← system-agnostic DM sub-skills
│
├── {Game Name} Rules/              ← one folder per game system/campaign
│   ├── rulebook/
│   │   ├── mechanics.md            ← parsed rules (generated at setup)
│   │   └── sub-skills/
│   │       └── [mechanic-name].md  ← generated sub-skills, one per mechanical domain
│   ├── campaign/
│   │   └── world-log.md            ← cross-dungeon persistent state
│   ├── dungeons/
│   │   └── [dungeon-name]/
│   │       ├── layout.md           ← broad structure, room list
│   │       ├── rooms/
│   │       │   └── [room-name].md  ← generated as player approaches
│   │       └── session-log.md      ← persistent record for this location
│   ├── player/
│   │   ├── character-sheet.md
│   │   └── inventory.md
│   └── companions/
│       └── [companion-name]/
│           ├── soul.md             ← personality, goals, beliefs, current state
│           ├── character-sheet.md
│           └── inventory.md
│
└── {Another Game} Rules/           ← second concurrent game, fully independent
    └── ...
```

All paths below are relative to the active `{Game Name} Rules/` folder.

**Format templates** (reference these when generating any file):

| File to generate | Template to follow |
|---|---|
| {Game Name} Rules/campaign/world-log.md | world_log_md_format.md |
| {Game Name} Rules/rulebook/mechanics.md | mechanics_md_format.md |
| {Game Name} Rules/rulebook/sub-skills/[name].md | generated_skill_format.md |
| {Game Name} Rules/dungeons/[name]/layout.md | layout_md_format.md |
| {Game Name} Rules/dungeons/[name]/rooms/[name].md | room_md_format.md |
| {Game Name} Rules/dungeons/[name]/session-log.md | session_log_md_format.md |
| {Game Name} Rules/player/character-sheet.md | character_sheet_md_format.md |
| {Game Name} Rules/player/inventory.md | inventory_md_format.md |
| {Game Name} Rules/companions/[name]/soul.md | soul_md_format.md |
| {Game Name} Rules/companions/[name]/character-sheet.md | character_sheet_md_format.md |
| {Game Name} Rules/companions/[name]/inventory.md | inventory_md_format.md |

---

## Entry Point — Do This First

Before doing anything else, run this check:

```
Step 1 — Scan for {Game Name} Rules/ folders containing rulebook/mechanics.md.

  NONE FOUND
    → No campaigns exist yet. Run dm_setup.md in full.
      Do not start a session or generate anything until setup is complete.

  ONE FOUND
    → That game is active. Skip to Step 2.

  MULTIPLE FOUND
    → Present the list to the player before proceeding:

      "I found [N] active campaigns:
        1. [Game A Name] — last session: [date from session-log, if available]
        2. [Game B Name] — last session: [date from session-log, if available]
        ...
        N+1. Start a new campaign

      Which would you like to continue, or start something new?"

      Wait for selection. Then proceed to Step 2 with the chosen game.

Step 2 — Check campaign state for the selected game.

  Does {Game Name} Rules/dungeons/[any dungeon]/session-log.md exist?

    NO
      → Rulebook exists but no campaign yet.
        Run dm_setup.md steps 6–9 (scenario, dungeon, session-log, world-log).

    YES
      → Does the most recent session-log entry have mid_session_notes
        but no closing session summary? (Indicates an interrupted session.)

        YES (session was interrupted)
          → Proceed to dm_session.md → Session Resume.

        NO (last session ended cleanly)
          → Proceed to dm_session.md → Session Start.
```

Do not skip or abbreviate setup. A campaign without mechanics.md cannot
be run correctly — there are no rules to reference for checks, combat,
or advancement.

---

## Sub-Skill Index

All DM behavior is defined in these files. Load the relevant sub-skill when
the situation requires it.

| Sub-skill | When to load | What it covers |
|---|---|---|
| `dm_session.md` | Every session | Session start, active play, session end |
| `dm_resolution.md` | Any skill check or combat | Skill checks, dice rolling, combat confirmation |
| `dm_files.md` | Always (background) | File maintenance, mid-session logging, context management |
| `dm_setup.md` | No mechanics.md exists, or rules questions | Campaign setup, character creation, undefined rules |
| `dm_dungeon.md` | Room generation or location transitions | Dungeon generation, multi-location campaigns |
| `dm_companions.md` | Any session with companions | Companion types, agency, character development |
| `dm_skill.md` | Session end or companion story beats | soul.md updates, surfacing rules, departure rules |
| `dm_narration.md` | Always (background) | Tone, voice, pacing, OOC communication, player prompts |

---

## What This Skill Does NOT Handle

These are delegated to sub-skills or future work:
- Multiplayer session coordination
- Rulebook PDF parsing — player pastes or describes key rules instead
