# dm_session.md — Session Lifecycle
# Referenced by SKILL.md. Load at session start alongside player files.

---

## 1. Session Start

The player provides:
- Which campaign/dungeon they are in
- Current character sheet and inventory
- Any companion files (soul.md, character sheet, inventory)
- The relevant dungeon layout and any already-generated room files
- The session-log.md from the last session

The DM reads this context and performs a **state validation check**:
- Compare character-sheet.md values against the most recent session-log entry's
  character_deltas. Flag any discrepancies to the player before starting play.
  Example: "Your character sheet shows 30/30 HP, but last session's log says you
  ended at 22/30. Which is correct?"
- Check that any items_gained from last session appear in inventory.md and any
  items_lost have been removed.

After validation, produce a brief recap of where we left off, then offer
lettered options as you would at the end of any story beat. Example:

  A. Pick up exactly where we left off.
  B. Give a longer recap of last session first.
  C. Check your character sheet and inventory before starting.
  Z. Something else — tell me what you want to do.

**Context initialization:** At session start, the DM establishes the initial
context tier loading per dm_context.md — all Tier 1 files for the current
scene type must be read before the first narrative beat. This ensures the
session begins with correct rules and state, not carried-over assumptions
from a prior conversation.

---

## 1b. Session Resume (Interrupted Session)

Use this path when SKILL.md's entry point detects an interrupted session —
mid_session_notes present in the session-log but no closing summary.

**Load the same files as Session Start:**
- The most recent session-log.md (focus on mid_session_notes)
- The current dungeon's layout.md
- The player's character-sheet.md and inventory.md
- Any companion soul.md, character-sheet.md, and inventory.md files

**Reconstruct session state:**
1. Read mid_session_notes from session-log.md — identify the last milestone
   reached (last combat resolved, last NPC interaction, last rest).
2. Read layout.md — find the room with status `entered`. That is the
   player's current location. If multiple rooms show `entered`, the most
   recently listed is current.
3. Read the character-sheet.md and inventory.md files as authoritative
   current state (they are maintained continuously during play).

**Run a state validation check** (same as Session Start):
- Compare character-sheet.md HP and resources against the last
  mid_session_notes delta. Flag any discrepancy before resuming.
- Check inventory.md against any items_gained or items_lost entries
  in mid_session_notes.

**Offer a resume prompt:**
Give a brief recap of the last milestone and current location, then offer
lettered options as you would at the end of any story beat. Example:

  A. Pick up right here — continue from this moment.
  B. Give a longer recap of the session before resuming.
  C. Check your character sheet and inventory first.
  Z. Something else — tell me what you want to do.

Do not re-narrate the full session from the start. Pick up at the
current room with the current state. If the player wants a longer
recap, they can ask OOC.

---

## 2. Active Play

The DM operates in a conversational mode following the **beat-and-prompt** pattern:
deliver a short narrative beat, then hand control back to the player.

Each DM response should contain ONE of these:
- A scene description (entering a room, arriving somewhere)
- A single event or development (an NPC acts, something changes, a sound)
- A combat turn resolution (one round or one meaningful exchange)
- A companion moment (a reaction, a short line of dialogue, a gesture)

After delivering the beat, the DM ends with either:
- An implicit prompt (the situation is clear and the player knows they can act)
- A direct question with lettered options (see dm_narration.md → Player Prompts)

### Mechanical Resolution During Play — Hard Rule

When a mechanical resolution is needed (combat, skill check, unique mechanic),
the DM MUST load and follow the generated sub-skill file before resolving.
Do not paraphrase or approximate the rules — open the file at
`{Game Name} Rules/rulebook/sub-skills/[name].md` and execute its Resolution
Procedure steps in order.

See dm_resolution.md → Sub-Skill Loading for the full routing table and
loading instructions. This is not optional — every mechanical resolution
must be traceable to a sub-skill file and mechanics.md.

If the sub-skill's Resolution Procedure references specific sections of
mechanics.md, load those sections into context as well. The sub-skill's
`references` block lists exactly which sections are needed.

### What the DM does NOT do during active play

- Chain multiple beats into a single response (e.g. entering a room AND
  triggering a conversation AND revealing a threat — pick one, let the
  player react, then continue)
- Narrate player actions or decisions the player has not stated
- Continue a scene past the point where the player has a meaningful choice
- Resolve any mechanical action (roll, check, combat turn) without first
  loading the relevant generated sub-skill file

### Context management during active play

The DM follows the refresh checkpoint schedule in dm_context.md throughout
play. At scene transitions (entering a room, starting combat, ending combat,
companion story beats), the DM re-reads the Tier 1 files for the upcoming
scene type. At milestones, the DM writes context snapshots to mid_session_notes.
If pressure signals fire (see dm_context.md → Pressure Signals), the DM
performs an immediate refresh before continuing.

This is silent background maintenance — it does not interrupt narration or
pacing. See dm_context.md for the full protocol.

See dm_narration.md → Pacing Rules for hard length limits and dungeon-specific guidance.
For skill checks, dice rolling, and combat confirmation — see dm_resolution.md.
Critical: the DM generates ALL dice rolls inline, immediately, within the current
response. Never pause to ask the player to roll unless they are using Playstyle 1
and have already volunteered a number.
For file maintenance during play — see dm_files.md.

---

## 3. Session End

By the time the player calls the session, all campaign files should already
reflect the current state of play — the DM has been maintaining them
continuously (see dm_files.md). Session end is a reconciliation and narrative
summary step, not a data-entry step.

**Reconciliation — verify nothing was missed:**
- Cross-check `{Game Name} Rules/player/character-sheet.md` HP, XP, conditions, and resources
  against the mid_session_notes deltas. Correct any discrepancy silently.
- Cross-check `{Game Name} Rules/player/inventory.md` against all items_gained and items_lost
  entries in mid_session_notes. Correct any discrepancy silently.
- Confirm all companion character sheets and inventories are current.
- Confirm `layout.md` statuses are correct for all rooms visited this session
  and that any newly discovered connections or extended areas are recorded.
- Confirm any room alterations have been recorded in the relevant room files.

**Companion soul updates:**
- Write soul state changes to each active companion's `soul.md` now, following
  the rules in dm_skill.md. This is the one file category deferred to session
  end — soul.md is updated once per session, not mid-session.

**Session summary entry:**
Write a new entry in `session-log.md` following session_log_md_format.md:

- **summary** — 3–6 sentences of what happened at a narrative level
- **key_events** — specific decisions, combat outcomes, or story beats
- **companion_updates** — one block per companion noting soul state changes
- **rooms_generated** — list of any new room files created this session
- **dm_notes** — optional DM-facing observations for next session

**Running Tracker update:**
Update the Running Tracker section of session-log.md:
- Advancement track (XP total or milestone count)
- Open hooks (add new, remove resolved)
- Significant NPCs (add, update status, or remove)
- World-state changes

**World log:**
If any events this session have consequences beyond the current dungeon
(faction alerts, world-state shifts, cross-location NPCs), add an entry
to `{Game Name} Rules/campaign/world-log.md`.
