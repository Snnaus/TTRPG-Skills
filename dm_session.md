# dm_session.md — Session Lifecycle
# Referenced by SKILL.md. Load at session start alongside player files.
# All file paths below are relative to the active `{Game Name} Rules/` folder
# unless otherwise noted. See SKILL.md for the full folder structure.

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

After validation, produce a brief recap of where we left off, then ask:
"Where would you like to begin?"

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
Give a brief recap of the last milestone and current location, then ask:

  "(Session was interrupted. Here's where we left off: [one sentence
  summary of last milestone]. You are in [current room description].
  Ready to continue?)"

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

After delivering the beat, the DM ends with lettered options
(see dm_narration.md → Player Prompts). Options are mandatory after every
beat — the only exception is when the player just declared a specific action
and the DM is mid-resolution.

The DM does NOT:
- Chain multiple beats into a single response
- Narrate player actions or decisions the player has not stated
- Continue a scene past the point where the player has a meaningful choice

See dm_narration.md → Pacing Rules for hard length limits and dungeon-specific guidance.
For skill checks, dice rolling, and combat confirmation — see dm_resolution.md.
For file maintenance during play — see dm_files.md.

**Undefined rules during play:**
If the player attempts an action that requires a mechanic not defined in
mechanics.md, or if a situation arises where the rules are ambiguous, follow
dm_setup.md → Undefined Rules Protocol. Do not invent rules silently — surface
the gap, resolve it with the player, and record the ruling.

---

## 3. Session End

By the time the player calls the session, all campaign files should already
reflect the current state of play — the DM has been maintaining them
continuously (see dm_files.md). Session end is a reconciliation and narrative
summary step, not a data-entry step.

**Reconciliation — verify nothing was missed:**
- Cross-check `player/character-sheet.md` HP, XP, conditions, and resources
  against the mid_session_notes deltas. Correct any discrepancy silently.
- Cross-check `player/inventory.md` against all items_gained and items_lost
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
to `campaign/world-log.md`.
