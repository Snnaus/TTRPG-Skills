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

## Multi-Location Campaigns

When the player completes a dungeon or moves to a new location:

1. Finalize the current dungeon's session-log.md with a closing summary.
2. Migrate unresolved narrative hooks from the dungeon's session-log to
   campaign/world-log.md → open_hooks.
3. Migrate significant NPCs that may appear elsewhere to world-log.md → persistent_npcs.
4. Generate the new location's layout.md and session-log.md as in the Setup Phase
   (see dm_setup.md).
5. At the start of the next session in the new location, load world-log.md
   alongside the new dungeon's files to preserve continuity.

The world-log is the bridge. Anything that matters beyond the walls of one
dungeon gets recorded there.
