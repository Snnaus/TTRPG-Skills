# dm_visuals.md — Visual Aids
# Referenced by SKILL.md. Load when the player asks a spatial question, combat begins, or a visual reference is needed.

---

## Visual Aids

Produce a visual aid when:
- The player asks a spatial question ("how far away is the enemy?")
- Combat begins (show rough positioning)
- The player asks to see their character sheet or inventory
- A room has a complex layout worth illustrating

### Format specifications

**Spatial combat diagram** — Use ASCII art. Zone-based by default (labeled
zones with cover and enemy positions). Use a grid only if the system explicitly
uses grid-based movement or the player requests it.

```
Example format:
  ┌─────────────────────────────────┐
  │ NORTH ALCOVE          [Door→R04]│
  │   [Warden]  [Pedestal]          │
  │─────────────────────────────────│
  │ CENTER FLOOR                    │
  │   (open, no cover)              │
  │─────────────────────────────────│
  │ SOUTH ENTRY           [Door→R02]│
  │   [Table/Cover]  [YOU]          │
  └─────────────────────────────────┘
```

Include: zone labels, enemy positions (by name), player position ([YOU]),
cover objects, exits with destination room IDs, and any active hazards.

**Character sheet summary** — Structured text, not a diagram. Show:
  - Name, role, level
  - HP: current/max
  - Key stats (abbreviated to fit a compact block)
  - Active conditions
  - Equipped items (weapon + armor only)
  - Resources with current/max (spell slots, stress, etc.)

**Dungeon map** — ASCII art using room IDs from layout.md. Mark current
location with [HERE], cleared rooms with [X], and unvisited rooms with
their ID. Use connection lines between rooms.

```
Example format:
  [X:R01] ── [HERE:R02] ── [R04:BOSS]
                  │
               [X:R03] ── [R05:TREASURE]
```
