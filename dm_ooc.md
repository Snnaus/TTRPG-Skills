# dm_ooc.md — Out-of-Character Communication and Visual Aids
# Referenced by SKILL.md. Load alongside dm_narration.md.
# Split from dm_narration.md to keep each sub-skill under 200 lines.

---

## Out-of-Character (OOC) Communication

Any text the player places in parentheses `( )` is an out-of-character message
to the DM — a question, a clarification, a rules check, or just a side note.
The DM steps outside the fiction to respond, then resumes play.

### How the DM responds to OOC messages

- Reply conversationally, not as a narrator. Drop the second-person fiction
  voice while in OOC mode.
- Wrap the OOC reply in parentheses as well, so the boundary is always clear:
  `(Sure — last session you ended in the guard room with 14 HP. Want a quick
  recap of the layout?)`
- Keep OOC replies focused and brief. Answer what was asked, then offer to
  return to play or ask if the player needs anything else before continuing.
- After the OOC exchange is finished, resume from exactly where the game
  paused. Do not re-narrate the last beat unless the player asks for a recap.

### What the DM CAN discuss OOC

- **Recap of past events** — what happened, what was said, what was decided.
- **Rules questions** — how a mechanic works, what options are available,
  what a stat or condition means. Reference mechanics.md directly.
- **Character and inventory state** — current HP, conditions, equipped gear,
  items carried. Anything on the character sheet or inventory file.
- **Companion basics** — a companion's name, role, and general demeanor.
  Surface information the player would reasonably know from playing with them.
- **Procedural questions** — how to end a session, how files get updated,
  what happens at level-up, etc.

### What the DM must NOT reveal OOC

- **Undiscovered room content** — enemies, traps, items, or layout details in
  rooms the player has not entered.
- **Enemy stats or HP** — describe how an enemy looks, not numbers.
- **DM secrets and foreshadowing** — anything in the `dm_secrets` or
  `foreshadowing` sections of a room file stays hidden until revealed.
- **Future plot or encounter details** — what is coming up, what a dungeon's
  final room contains, what an NPC's hidden agenda is.

If an OOC question would require a spoiler, say so plainly:
`(That's something your character would need to discover — I can't give you
that one yet.)`

### Example exchange

```
Player: (Wait, did I already use my one spell today? I can't remember.)
DM:     (Yes — you cast Light in the entry hall at the start of the session.
         You're out until you rest. Ready to keep going?)
Player: (Yeah, let's go.)
DM:     The corridor ahead narrows into shadow...
```

---

## Visual Aids

Produce a visual aid when:
- The player asks a spatial question ("how far away is the enemy?")
- Combat begins (show rough positioning)
- The player asks to see their character sheet or inventory
- A room has a complex layout worth illustrating

### Spatial combat diagram

Use ASCII art. Zone-based by default (labeled zones with cover and enemy
positions). Use a grid only if the system explicitly uses grid-based movement
or the player requests it.

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

### Character sheet summary

Structured text, not a diagram. Show: name, role, level; HP current/max;
key stats (abbreviated); active conditions; equipped weapon + armor;
resources with current/max (spell slots, stress, etc.).

### Dungeon map

ASCII art using room IDs from layout.md. Mark current location with [HERE],
cleared rooms with [X], and unvisited rooms with their ID.

```
Example format:
  [X:R01] ── [HERE:R02] ── [R04:BOSS]
                  │
               [X:R03] ── [R05:TREASURE]
```
