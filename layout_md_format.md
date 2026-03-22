# layout.md — Dungeon / Location Layout
# SKILL: dungeons/[location-name]/layout.md
# FORMAT VERSION: 1.0
# Generated at setup or when a new location is introduced.
# This file is the skeleton of the location. It does not contain room detail.
# Room detail lives in rooms/[room-name].md, generated as the player approaches.
# Once written, this layout is canonical. Changes require an in-game reason.

---
## Location Identity

name: [Full name of this location — e.g. "The Ashen Vault" | "The Merchant Quarter, Dravenport"]
type: [Location type — e.g. "underground dungeon" | "ruined city district" | "space station" |
       "haunted manor" | "forest labyrinth"]
biome: [Physical environment — e.g. "carved stone, ancient" | "urban, partially collapsed" |
        "cold vacuum with pressurized corridors" | "organic, living structure"]
atmosphere: >
  [2–3 sentences. What this location feels like before anything happens.
   What does the player sense — light level, sound, smell, temperature, dread, awe?
   This sets the tone DM should maintain when narrating rooms here.]

---
## Threat Profile

threat_level: [e.g. "Low — appropriate for new characters" | "High — lethal without preparation" |
               "Variable — escalates as player descends"]
dominant_faction: [Primary enemy group or hazard type — e.g. "Undead remnants of the Ember Order" |
                   "Corporate security drones, older model" | "none — environmental hazard only"]
secondary_threats: [Other dangers present — e.g. "ancient traps, unstable architecture" |
                    "rival scavenger group" | "none"]
faction_behavior: >
  [How enemies in this location behave collectively. Do they patrol? Guard fixed points?
   React to noise? Have a command structure? This shapes how combat and stealth play out
   across the whole location — not just in individual rooms.]

---
## Narrative Hooks

# Reasons this location matters beyond the immediate goal.
# These are seeds — not all will be picked up by the player.

primary_hook: [The main reason the player is here — quest objective, character motivation, etc.]
secondary_hooks:
  - [A secondary story thread this location could unlock — e.g. "Evidence that the faction
     here was betrayed by the same guild that wronged the player's companion"]
  - [Another thread — e.g. "A survivor is hiding here and knows more than they should"]
  # Add or remove. These inform DM narration and room generation.

---
## Room Manifest

# Complete list of rooms in this location.
# This is the skeleton — detail is in individual room files.
# Status tracks what the player has done here.

# Room types:
#   entry       — where the player enters; usually low threat
#   corridor    — transitional space; connects other rooms
#   encounter   — primary combat or conflict space
#   puzzle      — obstacle requiring non-combat resolution
#   rest        — safe or semi-safe recovery space
#   lore        — environmental storytelling, records, history
#   treasure    — primary reward room
#   boss        — climactic encounter space
#   exit        — leads out of this location or to a new zone

rooms:
  - id: R01
    name: [Room name — e.g. "Entry Hall" | "Airlock Beta-7"]
    type: [Room type from list above]
    connections: [Room IDs this room connects to — e.g. "R02, R03"]
    status: untouched
    # Status values: untouched / approached / active / cleared / altered
    # untouched  — player has not been near this room; file may not exist yet
    # approached — player is one move away; room file must now be generated
    # active     — player is currently in this room
    # cleared    — player has resolved this room's contents
    # altered    — player action has changed the room's state from its generated form
    file_exists: false
    # Set to true once the room file is generated.

  - id: R02
    name: [Room name]
    type: [Room type]
    connections: [e.g. "R01, R04"]
    status: untouched
    file_exists: false

  # Continue for every room in this location.
  # Minimum viable dungeon: 5–8 rooms.
  # Include at least one of each type relevant to the scenario.
  # Boss room should not be directly adjacent to the entry room.

---
## Location Map

# Abstract zone diagram. Not pixel-perfect — spatial clarity only.
# Use ASCII or plain text. Update as rooms are cleared or altered.
# Mark the player's current location with [HERE] when updating mid-session.
# Mark cleared rooms with an X. Mark unvisited rooms with their ID.

# Example format (replace with actual layout):
#
#   [ENTRY: R01] ── [R02] ── [R04: BOSS]
#                      │
#                   [R03] ── [R05: TREASURE]
#
# Adjust shape to match actual connections. Vertical and diagonal connections are valid.

map: |
  [Draw the location map here using room IDs and connection lines.]

---
## DM Notes

# Information the player does not have. Used to maintain consistency.
# Remove entries as they become known to the player (or move to session-log.md).

location_secret: >
  [The thing about this location that changes its meaning when revealed.
   e.g. "The vault was not built to keep people out — it was built to keep something in."]

hidden_elements:
  - [Something not immediately visible — e.g. "A second faction is watching from the shadows"]
  - [Another hidden element — e.g. "The boss can be bypassed entirely if the player finds the terminal in R03"]
  # Add or remove as needed.

pacing_notes: >
  [Optional. Guidance on the intended emotional arc of this location.
   e.g. "Start with isolation and unease. Let threat escalate in R03–R04. Boss room should
   feel like the pressure has been building for the whole run."]
