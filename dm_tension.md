# dm_tension.md — Tension, Escalation, and Pressure Clocks
# Referenced by SKILL.md. Load alongside dm_session.md at all times during active play.
# This sub-skill owns dungeon escalation. The DM uses it to ensure conflict arrives
# rather than waiting for the player to stumble into it.

---

## Core Principle

A dungeon is not a museum. It does not wait patiently for the player to find trouble.
Enemies move. Factions react. Time costs something. The player's presence in a location
has consequences that accumulate whether or not they act quickly.

The DM's job is to make the world press back.

---

## Session Persistence

The Tension Track, Faction Alert State, and Passive Beat Counter all persist
between sessions. They are written to session-log.md at session end and read
back at session start. The dungeon does not reset because the player logged off.

**At session end**, write the following block to the Running Tracker section
of session-log.md under `dungeon_state`:

```yaml
dungeon_state:
  tension_track: [1–5 — current level at session end]
  faction_alert: [unaware / suspicious / alarmed / mobilized]
  passive_beat_count: [0–4 — current count at session end]
  notes: >
    [Optional. One sentence on what drove the current state —
     e.g. "Combat in the guard chamber alerted the faction. Two enemies fled."
     Omit if nothing notable.]
```

**At session start** (and session resume), read `dungeon_state` from the most
recent session-log entry before beginning play. Restore the Tension Track,
Alert State, and passive beat counter to those values. Do not reset them to
defaults just because a new session is starting.

If `dungeon_state` is absent from the session log (older sessions predating
this system), infer starting state from context:
- Any combat logged → start at Tension Track 3 minimum
- Any enemy escape noted → start at Alarmed minimum
- No conflicts logged → start at track level matching the dungeon's threat_level default

**Mid-session updates** are written to mid_session_notes deltas as changes occur —
not to the Running Tracker, which is session-end only:

```
deltas: "HP -8. Tension Track: 3 → 4 (combat triggered patrol convergence).
         Faction alert: Suspicious → Alarmed. Passive beat counter reset."
```

This allows full reconstruction of dungeon state on an interrupted session resume.

---

## The Tension Track

Every dungeon session runs on a hidden Tension Track with five levels:

```
[1: DORMANT] → [2: STIRRING] → [3: ACTIVE] → [4: HUNTING] → [5: BREAKING POINT]
```

**Starting level:** Read from `dungeon_state.tension_track` in session-log.md.
If no prior session exists, derive from layout.md → threat_level:
- Low threat → start at 1 (Dormant)
- Moderate threat → start at 2 (Stirring)
- High/Variable threat → start at 3 (Active)

**The track only moves forward.** It never resets mid-session. A short rest may
slow the rate of escalation but does not reduce the level.

---

## What Each Level Means

**1 — DORMANT**
The dungeon feels still. Enemies are in their default positions. No sign of the
player has reached them yet. Atmosphere is heavy but not yet threatening.

DM behavior: Describe environmental unease. Surface dormant threads (see dm_skill.md).
No active enemy presence in narration.

**2 — STIRRING**
Something in the dungeon has registered a disturbance — sound, a draft from an
opened door, a missing patrol. Enemies are alert but not yet converging.

DM behavior: Begin surfacing signs of life. Distant sounds. A torch that was lit
is now dark. Footsteps that stop when the player stops. No direct encounter yet,
but the player should feel watched.

**3 — ACTIVE**
The dungeon knows someone is here. Patrols have changed routes. Doors the player
left open may now be closed. Enemies in uncleared rooms are positioned for defense,
not routine.

DM behavior: One enemy or faction element must appear within the next 2 DM responses —
not necessarily combat, but a direct encounter (a patrol spotted, a guard heard,
a door that opens before the player reaches it). This is a hard deadline, not a
suggestion.

**4 — HUNTING**
The dungeon's inhabitants are actively searching. Patrols have converged. Stragglers
from cleared rooms have been missed and reported. The player is being looked for.

DM behavior: Combat or a forced encounter must occur within the next DM response.
If the player is moving, the encounter finds them in transit. If they are stationary,
it comes to them. Do not wait for the player to trigger it.

**5 — BREAKING POINT**
The dungeon has mobilized fully. Multiple factions or enemy groups are coordinated.
The player is in a race — their window to act before being overwhelmed is closing.

DM behavior: Encounters become unavoidable. Every room transition carries a chance
of running into opposition. At this level the player should feel urgency in every
decision. This level does not sustain indefinitely — it resolves through combat,
escape, or player defeat.

---

## What Advances the Track

Each of the following advances the Tension Track by one level:

| Trigger | Notes |
|---|---|
| Player enters a new room | Applies once per room, not per step |
| Player triggers any noise-generating action | Forced door, dropped item, loud combat |
| Combat occurs in any room | Enemies elsewhere react to the sounds |
| Player takes a short rest | The dungeon doesn't wait |
| 3 consecutive passive beats without a tension signal | See "Passive Beat Counter" below |
| A patrol route is disrupted (guard not at post, door left open) | |
| Player is spotted by any enemy, even if combat doesn't occur | |

**The track does NOT advance when:**
- The player is in a cleared and sealed room taking a long rest (they have earned safety)
- The player successfully completes a stealth action without detection
- The dungeon's layout.md explicitly marks a room as isolated from the faction

---

## Passive Beat Counter

This is the primary anti-drag mechanism.

The DM keeps a count of consecutive "passive beats" — DM responses that contain
no combat, no threat signal, no companion confrontation, and no meaningful
discovery (a locked door opened, a lore reveal, a faction encounter).

Pure corridor narration, atmospheric description, and exploration of already-cleared
spaces all count as passive beats.

**At 3 passive beats:** The DM must introduce a tension signal in the next response.
This can be subtle — a sound, a companion's sudden stillness, a door that wasn't
closed before. The counter resets.

**At 5 passive beats without a tension signal:** Advance the Tension Track by one
level immediately. The dungeon reacts visibly and concretely. The counter resets.

The passive beat counter resets on any of the following:
- A combat encounter begins
- A companion takes an independent action that creates story pressure
- A meaningful discovery is made (lore, puzzle progress, key item found)
- A threat signal is successfully delivered
- A faction encounter occurs (hostile, neutral, or otherwise)

**Persistence:** The count at session end is written to `dungeon_state.passive_beat_count`
in session-log.md. On session start or resume, restore this count and continue
from it — do not restart at zero.

---

## Forced Encounter Rules

When the Tension Track reaches level 4 or the passive beat counter forces escalation,
the DM introduces a Forced Encounter. This is not "the player walks into a room with
enemies." This is the dungeon coming to the player.

**How to run a Forced Encounter:**

1. Determine the encounter type based on the dungeon's faction_behavior (from layout.md):
   - Patrol faction → a patrol finds the player mid-corridor
   - Guard faction → a guard comes to check on an area the player disturbed
   - Reactive faction → reinforcements arrive at a room the player just cleared
   - Environmental dungeon (no faction) → a hazard activates, a trap triggers, a structural
     event occurs that forces immediate action

2. Do not pre-announce it. The encounter appears in narration as a natural continuation:
   > "You're halfway across the corridor when the door at the far end swings open."

3. Run it from that point. The player has a decision to make immediately — fight,
   flee, hide, talk. All options are live.

4. After the Forced Encounter resolves, the passive beat counter resets and the
   Tension Track level holds at its current value.

---

## Rest and Tension

**Short rest:** Does not reduce Tension Track level. Advances the track by one.
If the player is in an unsecured room, roll for an encounter during the rest.

**Long rest:** Only valid in a cleared and sealed room, or a designated rest room
per layout.md. Does not reduce the Tension Track below 2 — even safe rest means
the dungeon has reorganized. A long rest attempted in an unsecured location is
interrupted by a Forced Encounter after approximately one hour.

**Rest across a session boundary:** Record the rest type and elapsed time in
mid_session_notes. On resume, determine whether the rest completed based on the
dungeon_state restored from session-log.md.

---

## Dungeon-Level Escalation Cap

| Threat Level | Maximum Tension Track Level |
|---|---|
| Low | 3 (Active) — can reach 4 temporarily during a chase or escape |
| Moderate | 4 (Hunting) |
| High / Variable | 5 (Breaking Point) — no cap |

---

## Loading Note

This sub-skill is loaded at session start alongside dm_session.md and dm_narration.md.
It runs continuously in the background — the DM does not announce the Tension Track
level to the player. It is a DM-facing tool, not a player-facing mechanic.

The player experiences it only through narration: the dungeon feeling increasingly
hostile, enemies arriving uninvited, the walls closing in.

The player may ask OOC at any time: "(What's the current tension level?)" The DM
answers in parentheses with the track level and alert state, then resumes play.
