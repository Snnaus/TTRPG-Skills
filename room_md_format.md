# [room-name].md — Room File
# SKILL: dungeons/[location-name]/rooms/[room-name].md
# FORMAT VERSION: 1.0
# Generated when the player is one move away from entering this room.
# Once generated, this file is canonical.
# Do not alter it unless a player action explicitly changes the space.
# Record any player-caused alterations under the Alterations section at the bottom.

---
## Identity

id: [Room ID matching layout.md manifest — e.g. "R03"]
name: [Room name — e.g. "The Warden's Chamber" | "Cargo Bay 7"]
type: [Room type — entry / corridor / encounter / puzzle / rest / lore / treasure / boss / exit]
location: [Parent location name — e.g. "The Ashen Vault"]

---
## Description

# What the player perceives on entering before taking any action.
# Write in second person. Vivid but concise — 3–5 sentences.
# Do not reveal hidden elements here. Describe only what is immediately apparent.

entry_description: >
  [e.g. "The door gives way with a low groan and the smell hits you first — iron and old
  smoke. The chamber is long and low-ceilinged, lined with iron sconces that have long
  since burned out. Your light catches the edge of an overturned table near the far wall
  and the silhouette of something that isn't furniture."]

---
## Environment

# Physical properties that affect movement, combat, or exploration.

light: [e.g. "Pitch dark — no natural light source" | "Dim — arrow slits admit grey daylight" |
        "Bright — active overhead lighting, no shadows"]
terrain: [Relevant surface and obstacle notes — e.g. "Stone floor, dry. Overturned table
          provides partial cover near the east wall. Rubble pile in the northwest corner." |
          "Even metal floor, sealed. No natural cover."]
hazards: [Environmental dangers — e.g. "Unstable ceiling near the north wall — loud impacts
          risk collapse" | "Exposed wiring on the east panel — touching it deals damage" |
          "none"]
size: [Rough dimensions or zone count — e.g. "Large — roughly 40ft × 30ft, 3 distinct zones" |
       "Small — single zone, 15ft across" | "abstract — treat as 2 zones"]

---
## Enemies

# Enemies present when the room is first entered.
# If the room type is not an encounter room, this section may be empty.
# Stat values should use the format defined in mechanics.md.
# Do not invent stats — reference the system's stat structure.

enemies:
  - name: [Enemy name — e.g. "Vault Warden" | "Security Drone MK-II"]
    count: [Number of this enemy type present]
    role: [Combat role — e.g. "melee bruiser" | "ranged harasser" | "support / healer" |
           "controller — restricts movement"]
    stats:
      # List only the stats relevant to running this enemy in combat.
      # Format matches the system's stat expression from mechanics.md.
      [stat_name]: [value]
      [stat_name]: [value]
      # Add as many stats as needed to run this enemy.
    abilities:
      - [Notable ability — e.g. "Necrotic Strike: deals extra damage on hit and heals the Warden for the same amount"]
      - [Add any special actions or passive traits worth flagging during combat]
    behavior: [How this enemy engages — e.g. "Rushes the nearest threat. Protects the lore
               pedestal at the north wall — will not move more than 10ft from it." |
               "Patrols. Will alert other rooms if not silenced quickly."]
    defeat_drops: [What the player can take after defeating this enemy — e.g. "Iron key (fits R05 lock)" |
                   "none" | "1d6 gold equivalent"]
  # Add one entry per distinct enemy type.
  # Remove this section entirely if the room has no enemies.

enemy_notes: >
  [Optional. DM-facing notes about this encounter — tactics, trigger conditions, hidden
   behaviors. e.g. "The Warden will not attack until the player moves within 20ft of the
   pedestal. Until then it watches and tracks movement silently."]

---
## Items and Treasure

# Everything the player can take, use, or interact with.

loot:
  - name: [Item name]
    type: [e.g. "weapon" | "armor" | "consumable" | "key item" | "currency" | "lore object"]
    description: [What it is and what it does — brief]
    location_in_room: [Where it is found — e.g. "Inside the chest against the east wall" |
                       "On the Warden's body after defeat"]
  # Add one entry per item. Remove section if room has no loot.

interactables:
  # Objects that can be examined or used but not taken.
  - name: [Object name — e.g. "Iron pedestal" | "Old map pinned to the wall"]
    description: [What the player learns or can do when they interact with it]
    hidden: [true / false — if true, player must search or pass a check to notice it]
  # Remove section if room has no interactables.

---
## Exits

# All ways out of this room and what the player sees from each.
# Connects back to layout.md — use the same room IDs.

exits:
  - direction: [e.g. "North door" | "East passage" | "Ladder down" | "Airlock hatch"]
    leads_to: [Room ID — e.g. "R04"]
    description: [What the player sees when they look toward this exit —
                  e.g. "A reinforced iron door, closed but unlocked. Faint light bleeds under it." |
                  "A collapsed passage — rubble blocks the way. Could be cleared with effort."]
    condition: [e.g. "open" | "locked — iron key required" | "blocked — requires a strength check" |
                "concealed — not visible without a search action"]
  # Add one entry per exit.

---
## Spatial Notes

# Used to generate combat diagrams or answer spatial questions.
# Write for the DM — not for player narration.

zones:
  - label: [Zone name — e.g. "Near entrance" | "Center floor" | "Pedestal area"]
    cover: [Cover available — e.g. "full cover behind overturned table" | "half cover, debris" | "none"]
    notes: [Relevant tactical details — e.g. "Enemies entering from the east must pass through
            here" | "Hazard zone — within range of ceiling collapse"]
  # Add one zone entry per distinct tactical area in the room.

diagram: |
  # Optional ASCII combat map. Generate if the room is spatially complex.
  # Mark exits, cover objects, enemy start positions, and hazards.
  # Example:
  #
  #   N
  #   │  [DOOR → R04]
  #   ▲
  #   │  [Warden]    [Pedestal]
  #   │
  #   │  [Table/Cover]
  #   ▼
  #   │  [DOOR → R02]
  #
  # Replace with actual room layout or leave blank for simple rooms.

---
## Status

# Tracks what has happened to this room. Updated at session end.

status: untouched
# untouched  — generated but player has not entered
# active     — player is currently here
# cleared    — all threats resolved, loot taken
# altered    — player action has changed the room's physical state

alterations: []
# Record player-caused changes after they happen.
# Format: "[Session date or number]: [What changed and why]"
# Example:
#   - "Session 3: The iron pedestal was destroyed by the player. The door to R04 is now
#      permanently unlocked — the pedestal was holding it sealed."

---
## DM Notes

# Hidden information the player does not have.
# Remove or strike through entries as they become known.

secrets:
  - [Something not apparent from the room description — e.g. "The Warden is not hostile by
     nature — it is bound by a glyph on the pedestal. Destroying the pedestal frees it and
     it becomes neutral, possibly an ally."]
  - [Add additional secrets as needed]

foreshadowing:
  - [Detail in this room that points toward a future story beat — e.g. "The insignia on the
     Warden's armor matches the one Mira went silent about in R01."]
  # These should be visible in the room description or through interaction.
  # Remove when the player has noticed them.
