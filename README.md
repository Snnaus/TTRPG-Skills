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

Designed to work with any system that fits the supported structure.

---

## File Structure

The DM skill files (this repo) are system-agnostic and sit at the root. Each
game system and its campaign data live in a dedicated `{Game Name} Rules/`
folder. Multiple games can run concurrently — they never share files.

```
/
├── SKILL.md                        ← Parent routing skill (start here)
├── dm_*.md                         ← System-agnostic DM sub-skills
│
├── {Game Name} Rules/              ← Example: one game's full campaign data
│   ├── rulebook/
│   │   ├── mechanics.md            ← Parsed rules (generated at setup)
│   │   └── sub-skills/
│   │       └── [mechanic-name].md  ← Generated sub-skills, one per domain
│   ├── campaign/
│   │   └── world-log.md            ← Cross-dungeon persistent state
│   ├── dungeons/
│   │   └── [dungeon-name]/
│   │       ├── layout.md           ← Broad structure and room manifest
│   │       ├── rooms/
│   │       │   └── [room-name].md  ← Generated as the player approaches
│   │       └── session-log.md      ← Persistent session record
│   ├── player/
│   │   ├── character-sheet.md
│   │   └── inventory.md
│   └── companions/
│       └── [companion-name]/
│           ├── soul.md             ← Personality, goals, beliefs, current state
│           ├── character-sheet.md
│           └── inventory.md
│
└── {Another Game} Rules/           ← Second concurrent game, fully independent
    └── ...
```

**Format templates** (in the repo root — used when generating any file):

| File to generate | Template |
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

---

## How to Use It

### First Time Setup

1. Open a new Claude conversation and attach or paste the contents of `SKILL.md` and the relevant `dm_*.md` sub-skills.
2. Tell Claude you want to start a new campaign and provide your rulebook using one of three methods:
   - **PDF upload (recommended):** Upload your rulebook PDF. Claude will extract the rules content, identify core mechanics, and present a summary for you to confirm before proceeding. This produces the most complete and accurate rules parsing. *(Include `dm_pdf_ingest.md` in your context load for this method.)*
   - **Pasted text:** Copy and paste the key mechanics sections from your rulebook directly into the chat.
   - **Described from memory:** Describe the core rules and Claude will ask clarifying questions to fill in gaps.
3. Claude will confirm the game name, create a `{Game Name} Rules/` folder, then:
   - Parse the rulebook into `{Game Name} Rules/rulebook/mechanics.md`
   - Generate system-specific sub-skills (at minimum: `combat_resolution` and `skill_checks`)
   - Walk you through character creation → `player/character-sheet.md` and `player/inventory.md`
   - Ask if you want AI companion party members (each gets a `soul.md`, character sheet, and inventory)
   - Ask for a scenario or offer to generate one
   - Generate the first dungeon's `layout.md` and initialize `session-log.md`

### Starting or Resuming a Session

Load the following files into context:
- `SKILL.md` and the relevant `dm_*.md` sub-skills
- The most recent `session-log.md` entry (or last 2–3 entries)
- The current dungeon's `layout.md`
- Your `character-sheet.md` and `inventory.md`
- Any companion `soul.md`, `character-sheet.md`, and `inventory.md` files

**Multiple campaigns** — if you have more than one `{Game Name} Rules/` folder, the DM will list all active campaigns (with last session date where available) and ask which you want to continue, or offer to start a new one.

**Starting fresh** — Claude validates your character state against the last session log, flags any discrepancies, gives a brief recap, then offers lettered options — jump straight in, get a longer recap, or check your sheet first.

**Resuming an interrupted session** — if the last session was cut off mid-play (context lost, conversation ended unexpectedly), the DM detects this from the session log and automatically switches to resume mode: it reconstructs your current location from `layout.md`, checks your character state from the campaign files, and offers a short recap followed by the same lettered options before picking up exactly where you left off.

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

**Dice rolls** — the DM generates all rolls itself, immediately, inline in the response. You never need to provide a roll number unless you want to use Playstyle 1 (mechanical declaration — see Combat below). Player rolls are shown fully:

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

### PDF Rulebook Ingestion

The DM can read PDF rulebooks directly. Upload your rulebook PDF during setup and the DM will extract the rules content using a multi-strategy approach: text extraction for text-based PDFs, page rasterization for scanned documents, and targeted table extraction for stat blocks and reference charts. The DM presents a summary of what it found for your confirmation before parsing into mechanics.md. See `dm_pdf_ingest.md` for the full extraction procedure.

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

### Context Window Management

Long sessions consume context. As the conversation grows, the earliest loaded content — rules, companion personalities, game state — can drift out of effective attention. The DM uses a three-part system to prevent this:

- **Tiered file loading** — files are classified into three tiers (always-active, scene-active, reference-only) based on how critical they are. The DM loads and releases files according to their tier.
- **Refresh checkpoints** — at scene transitions (entering a room, starting combat, ending combat, companion story beats), the DM re-reads the core rules files needed for the upcoming scene type. If 8+ player turns pass without a refresh, one is triggered automatically.
- **Context snapshots** — at every milestone (combat resolved, NPC interaction, rest), the DM writes a compact state summary to the session log. This serves as a recovery point if the session is interrupted or if context pressure forces earlier content out.

If context pressure becomes severe, the DM may suggest a natural save point — but only once, and only as a suggestion. See `dm_context.md` for the full protocol.

---

## What This Does NOT Handle

- **Multiplayer coordination**

---

## Repository Contents

**DM sub-skills** — load the relevant file when the situation requires it:

| File | When to load | What it covers |
|---|---|---|
| `SKILL.md` | Every session | Parent router — file structure, template index, sub-skill index |
| `dm_session.md` | Every session | Session start, active play, session end |
| `dm_resolution.md` | Any skill check or combat | Skill checks, dice rolling, combat confirmation |
| `dm_files.md` | Always (background) | File maintenance, mid-session logging, context management |
| `dm_setup.md` | First time setup or rules questions | Campaign setup, character creation, undefined rules |
| `dm_pdf_ingest.md` | Player uploads a PDF rulebook during setup | PDF extraction, content diagnosis, targeted page reading |
| `dm_dungeon.md` | Room generation or location transitions | Dungeon generation, multi-location campaigns |
| `dm_companions.md` | Any session with companions | Companion types, agency, character development |
| `dm_skill.md` | Session end or companion story beats | soul.md updates, surfacing rules, departure rules |
| `dm_narration.md` | Always (background) | Tone, voice, pacing, OOC communication, player prompts |
| `dm_context.md` | Always (background) | Context window management, refresh checkpoints, snapshot format, pressure protocol |

**Format templates** — used when generating campaign files:

| File | Purpose |
|---|---|
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
