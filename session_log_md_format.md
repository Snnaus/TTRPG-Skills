# session-log.md — Campaign Session Log
# SKILL: dungeons/[location-name]/session-log.md
# FORMAT VERSION: 1.1
# Persistent record of all sessions in this campaign.
# Written by the DM: mid_session_notes are appended automatically during play at
# key milestones; the full session summary is written at session end.
# Player may annotate but should not alter DM-written entries.
# This file is loaded at session start to reconstruct context.
# Load only the most recent 2–3 entries in context unless the player references older history.

---
## Campaign Identity

campaign_name: [Name of this campaign or adventure]
location: [Primary dungeon or location name]
system: [TTRPG system being used — matches mechanics.md]
player_character: [Player character name and role]
companions: [List of active companion names — e.g. "Mira (Cleric), Torven (Scout)" | "none"]
campaign_start: [Date of first session — YYYY-MM-DD]

---
## Running Tracker

# Persistent values that change across sessions.
# Updated each session end. Single source of truth for campaign-wide state.

advancement:
  current_level: [Current character level, tier, or rank]
  advancement_track: [Current XP total, milestones, or equivalent]
  next_threshold: [What is needed to advance — e.g. "900 XP" | "3rd major milestone" |
                   "not tracked"]

dungeon_state:
  # Tension and alert state as of the END of the most recent session.
  # Read by the DM at session start to restore escalation state.
  # The dungeon does not reset between sessions — these values carry forward.
  tension_track: [1–5 — level at session end]
  # 1: Dormant | 2: Stirring | 3: Active | 4: Hunting | 5: Breaking Point
  faction_alert: [unaware / suspicious / alarmed / mobilized]
  passive_beat_count: [0–4 — counter value at session end; restored at next session start]
  notes: >
    [Optional. One sentence on what drove the current state —
     e.g. "Two guards fled combat and reached the upper level. Faction is now mobilized."
     Omit if nothing notable — leave as empty string or remove field.]

significant_npcs:
  # NPCs who have become narratively important across sessions.
  # Not full companions — these are tracked because they may return.
  - name: [NPC name]
    last_known_status: [e.g. "Alive, hostile" | "Deceased — Session 3" | "Unknown, fled"]
    significance: [Why this NPC matters — one sentence]
  # Add when an NPC becomes significant. Do not list every NPC encountered.
  # Remove if the NPC is fully resolved with no future relevance.

open_hooks:
  # Unresolved story threads, player leads, and dangling questions.
  # Add freely. Remove only when definitively resolved in play.
  - "[e.g. The locked door in R03 — player does not yet have the key]"
  - "[e.g. Mira recognized something in the vault but said nothing. Not yet addressed.]"
  # Keep this list current. It informs what the DM should surface going forward.

world_state_changes:
  # Major changes to the world caused by player action that persist beyond this dungeon.
  # Not room-level changes — those live in room files. These are world-level consequences.
  - "[e.g. The Ember Order's garrison in Dravenport has been alerted — Session 4]"
  # Add sparingly. Only truly consequential changes belong here.

---
## Session Entries

# One entry per session, appended in order.
# Each entry is written by the DM at session end.
# Do not edit previous entries. Annotate instead.

# ─────────────────────────────────────────────
# SESSION [number] — [YYYY-MM-DD]
# ─────────────────────────────────────────────

sessions:
  - session: 1
    date: [YYYY-MM-DD]

    dm_rolls:
      # Audit log of all DM rolls made this session.
      # Appended immediately when the roll is made — never edited after the fact.
      # Results are withheld from the player at the time if the information is
      # sensitive. The player may ask OOC to review any entry once the relevant
      # encounter or scene is resolved.
      - label: "[e.g. Guard perception check — R03]"
        dice: "[e.g. 1d20]"
        result: "[individual die result(s) — e.g. 6]"
        modifier: "[modifier value and source — e.g. +2 (WIS) | none]"
        total: "[final total — e.g. 8]"
        context: "[What this roll determined — e.g. 'Guard failed to notice player hiding behind crates']"
        revealed: false  # Set to true once the player has been told the result
      # Continue appending entries below as rolls occur.

    mid_session_notes:
      # Written by the DM automatically during play at key story milestones.
      # Each entry is appended as events occur — do not edit previous entries.
      # The player does not need to manage this; the DM maintains it silently.
      # At session end, the DM uses these notes to write the full summary below.
      # Tension/alert state changes are recorded here as they happen.
      - label: "[e.g. Combat — Guard Room R03]"
        outcome: "[One sentence — what happened and how it resolved]"
        deltas: "[HP change, items gained/lost, XP if awarded, tension/alert changes — or 'none']"
        # Tension delta example: "Tension Track: 2 → 3. Faction alert: unaware → suspicious."
        hooks: "[Any new open threads this created — or 'none']"
      # Continue appending entries below as milestones occur.

    summary: >
      [3–6 sentences. What happened this session at a narrative level.
       Enough detail to reconstruct context at next session start without
       re-reading everything else. Write in past tense, third person.]

    key_events:
      # Specific decisions, combat outcomes, or story beats worth flagging.
      - "[e.g. Player chose to free the prisoner rather than complete the retrieval objective]"
      - "[e.g. First combat encounter — cleared without player taking damage]"
      - "[e.g. Player learned the vault was built to contain something, not protect it]"

    character_deltas:
      # Changes to track before next session. Player applies these to their files.
      xp_gained: [Amount — e.g. "150 XP" | "1 milestone" | "none"]
      hp_change: [Net change — e.g. "-8 HP taken (currently at 22/30)" | "no change"]
      items_gained:
        - [Item name and brief note — e.g. "Iron key from the Warden's body"]
      items_lost:
        - [Item name and reason — e.g. "2× Healing Potion consumed"]
      currency_change: [Net gain/loss — e.g. "+34 gold" | "no change"]
      # Remove empty lists. Keep only what changed.

    companion_updates:
      # Soul state changes to apply at session end. One block per companion.
      - companion: [Companion name]
        internal_state_updated: [true / false]
        relationship_changed: [true / false — if true, note direction]
        milestone_added: [true / false — if true, log the milestone event]
        notes: [Brief summary of what shifted and why — e.g. "Mira went quiet after the
                village massacre reference. No direct engagement from player. Internal state
                updated to reflect she is processing this alone."]
      # Remove if no companions are active.

    rooms_generated:
      # New room files created this session.
      - [Room ID and name — e.g. "R03 — The Warden's Chamber"]
      # Empty list if no new rooms were generated this session.

    dm_notes: >
      [Optional. DM-facing observations not captured elsewhere.
       e.g. "Player is avoiding the companion arc. Will surface thread more directly
       next session through environmental detail rather than dialogue."]

  # ─────────────────────────────────────────────
  # Append subsequent sessions below in the same format.
  # ─────────────────────────────────────────────
