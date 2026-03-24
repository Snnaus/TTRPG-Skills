# dm_dungeon.md — Dungeon Generation and Multi-Location Campaigns
# Referenced by SKILL.md. Load when generating rooms or transitioning locations.

---

## Dungeon Generation Rules

Room IDs (R01, R02, etc.) are internal tracking identifiers used in layout.md,
room files, and file maintenance. They are never spoken aloud in narration.
In story, rooms are described by what they are — "the guard room", "the chamber
with the collapsed ceiling", "the corridor you came in through." See dm_narration.md
→ Tone and Voice for the full rule.

Dungeons are generated using a "develop as you go" model:

- layout.md defines the skeleton (room count, types, connections, overall threat)
- Individual room files are generated when the player is one move away from
  entering them — this is signaled by setting the room's status to `approached`
  in layout.md

**Triggering room generation:**
When the player moves toward a room and it has no existing file (file_exists: false
in layout.md), generate the room file immediately before narrating the approach.
Use room_md_format.md. Populate it from:
  - The room's type and connections from layout.md
  - The location's threat level and dominant faction from layout.md
  - Enemy stat formats from mechanics.md (do not invent stats)
  - Narrative hooks from layout.md if this room is relevant to them

**What each room file contains:**
  - Entry description (what the player sees on entering — no hidden information)
  - Environment (light, terrain, hazards, size)
  - Enemies (type, count, stats in system format, behavior)
  - Items and interactables
  - Exits with descriptions and conditions
  - Spatial notes (zones and optional ASCII diagram for complex rooms)
  - DM-only secrets and foreshadowing

**After generating:**
Set file_exists: true and status: approached in layout.md for that room.

Once a room file is generated, it is canonical. Do not change it unless a
player action explicitly alters the space. Record any alterations in the room
file's `alterations` log and update the room's status to `altered` in layout.md.

**layout.md status transitions during play** (see dm_files.md for full trigger table):

| Status | Meaning |
|---|---|
| `pending` | Room exists in manifest, no file yet, player hasn't approached |
| `approached` | Player is one move away — room file has been generated |
| `entered` | Player has entered the room |
| `cleared` | All threats resolved, room is safe |
| `altered` | Player actions have changed the space — alterations logged in room file |

---

## Faction Alert States

Every dungeon with a living faction (not purely environmental) runs on an
alert state that tracks what the faction knows. This is distinct from the
Tension Track in dm_tension.md — alert state is faction-awareness, tension
is DM pacing. They interact but are not the same thing.

**Alert levels:**

| Level | What the faction knows | Behavior |
|---|---|---|
| Unaware | Nothing. Routine. | Enemies at default positions, patrol routes normal |
| Suspicious | Something is off — a sound, a missing guard, a door that was closed | Patrols increase; one or two enemies sent to investigate |
| Alarmed | A confirmed intrusion. They know someone is here. | Patrols converge; non-combat enemies fall back to defensible positions; reinforcements staged |
| Mobilized | They have location or description of the player. | Active hunting. Enemies move toward the player rather than waiting. Bosses or leaders become active. |

**Alert transitions:**

| Event | Transition |
|---|---|
| Player heard (loud action, failed stealth) | Unaware → Suspicious |
| Player spotted (any enemy sees them, even briefly) | Suspicious → Alarmed |
| Combat occurs | → Alarmed immediately, regardless of prior level |
| An enemy escapes a combat alive | → Mobilized |
| A patrol finds a cleared room or a body | +1 level |
| Player eliminates all witnesses silently | Level holds or drops by 1 at DM discretion |

**When generating rooms at Alarmed or Mobilized state:**
Enemies in unvisited rooms are no longer in their default positions. They are:
- Facing the door the player is likely to come from
- Clustered rather than spread
- Possibly reinforced by 1 additional enemy from an adjacent cleared area
  (if that enemy was not defeated — mark them as relocated in the room file)

This is applied silently. The player discovers it when they enter. Do not
announce that alert state changed or that rooms have been reconfigured.

---

## Conflict Pacing in Layout Generation

When generating a dungeon's layout.md, the DM must structure the room manifest
to guarantee conflict escalation. The following rules apply at generation time:

**Required conflict beats per dungeon:**

| Dungeon size | Minimum forced encounters | Minimum meaningful discoveries |
|---|---|---|
| Small (5–7 rooms) | 2 | 2 |
| Medium (8–12 rooms) | 3 | 3 |
| Large (13+ rooms) | 4 | 4 |

A "forced encounter" is a room or event that cannot be bypassed without a roll
or a decision — it is designed into the layout, not left to chance. At generation
time, mark at least this many rooms with `type: encounter` and ensure at least
one of them is in the first half of the dungeon.

**The first encounter must be within reach by room 3.**
If the entry point is R01, there must be a room of type `encounter` reachable
within two moves. Do not generate dungeons where the first three rooms are all
corridors, lore, or rest areas. If the layout calls for that, add a patrol
or wandering enemy to one of those rooms instead.

**Boss rooms must be preceded by at least one encounter room.**
The player should never walk from a cleared corridor directly into the boss.
There is always a buffer — another encounter, a rest/lore room with a complication,
or a puzzle with teeth (a wrong answer triggers a threat).

**Add at least one "chase point" to medium and large dungeons.**
A chase point is a location where the layout funnels the player and creates
urgency — a collapsing bridge, a room that floods, a patrol route that the
player must cross. Mark these in layout.md `pacing_notes`. Generate the
room file with a time-pressure mechanic: the player has a limited number of
actions before the situation forces a decision.

---

## Multi-Location Campaigns

When the player completes a dungeon or moves to a new location:

1. Finalize the current dungeon's session-log.md with a closing summary.
2. Migrate unresolved narrative hooks from the dungeon's session-log to
   {Game Name} Rules/campaign/world-log.md → open_hooks.
3. Migrate significant NPCs that may appear elsewhere to {Game Name} Rules/campaign/world-log.md → persistent_npcs.
4. Generate the new location's layout.md and session-log.md as in the Setup Phase
   (see dm_setup.md).
5. At the start of the next session in the new location, load world-log.md
   alongside the new dungeon's files to preserve continuity.

The world-log is the bridge. Anything that matters beyond the walls of one
dungeon gets recorded there.
