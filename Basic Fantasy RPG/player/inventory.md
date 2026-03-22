# inventory.md — Inventory
# SKILL: player/inventory.md
# FORMAT VERSION: 1.0
# System: Basic Fantasy RPG, 3rd Edition (revision 127)
# Character: Caerwyn (Elf Magic-User, Level 1)

---
## Equipped

equipped:
  - slot: Main hand
    item: Silver Dagger
    properties: "1d8 damage (melee or thrown). STR -1 applies to attack roll and damage
                (minimum 1 damage on a successful hit). Silver — effective against
                lycanthropes and monsters that require silver weapons to damage."
    notes: Her only weapon. Kept sheathed at her belt. The silver edge makes it
           worth the cost over a standard dagger — lycanthropes ignore normal steel.

  - slot: Carried (worn)
    item: Backpack
    properties: Holds up to 40 lbs of gear. Currently worn — contents accessible
                in most situations.
    notes: Everything else lives here.

---
## Carried

carried:
  - item: Spellbook
    quantity: 1
    type: key item
    properties: Contains Read Magic and Sleep. Must study for 1 hour after a full
                rest to re-memorize spells. Lost or destroyed spellbook = no spell
                recovery until replaced (cost 25 gp for blank book; spells must
                be re-acquired).
    notes: Her most irreplaceable possession. Stored inside the scroll case during
           travel to protect it from moisture and wear.

  - item: Map/Scroll Case
    quantity: 1
    type: container
    properties: Waterproof tube. Protects rolled paper, maps, and the spellbook
                from moisture and physical damage.

  - item: Paper
    quantity: 5 sheets
    type: tool
    properties: For dungeon mapping, notes, and spell research. Fragile — ruined
                if soaked. Store in the scroll case when not in use.

  - item: Ink, jar
    quantity: 1
    type: tool
    properties: Standard writing ink. Sufficient for extensive notes and mapping.
                Spills in the pack are a hazard — keep it sealed.

  - item: Quill
    quantity: 1
    type: tool
    properties: Writing implement. Pair with ink. Fragile tip — avoid rough handling.

  - item: Chalk
    quantity: 1 small bag (~20 pieces)
    type: tool
    properties: Mark dungeon walls to track explored areas, indicate traps or hazards,
                and leave signals for the party. Works on stone and plaster.

  - item: Rations, Dry
    quantity: 1 week supply
    type: consumable
    properties: Sustains one character for one week without foraging. No preparation
                required. Cross off days as they pass.

  - item: Waterskin
    quantity: 1
    type: consumable
    properties: Holds approximately one day's water supply. Refill at streams, wells,
                or other clean water sources. Mark as empty when depleted.

  - item: Rope, Hemp
    quantity: 1 (50ft coil)
    type: tool
    properties: Supports approximately 1,000 lbs. Used for climbing, descending,
                binding, or rigging. 50ft covers most dungeon vertical hazards.

  - item: Iron Spikes
    quantity: 12
    type: tool
    properties: Hammered into doorframes to hold doors open or shut, anchor a rope,
                or improvise a weapon (1d4 damage at GM discretion).
    notes: No hammer in inventory. Can be driven using a rock, the dagger pommel
           (risks dulling the blade), or another spike as a makeshift punch. Worth
           acquiring a hammer when possible.

  - item: Tinderbox (flint and steel)
    quantity: 1
    type: tool
    properties: Lights torches, lanterns, or campfires. Takes 1 full round to
                produce a flame under normal conditions. Longer in wind or wet.

  - item: Torches
    quantity: 6
    type: consumable
    properties: Burns for approximately 1 hour per torch. Illuminates a 30ft radius.
                Requires tinderbox to light. Mark off as consumed.
    notes: Caerwyn has Darkvision and does not personally need torches — but
           non-elf party members do. Useful for fire and signaling regardless.

  - item: Winter Blanket
    quantity: 1
    type: tool
    properties: Warmth for cold environments and rough outdoor rests. Reduces risk
                of cold-related attrition at GM discretion. Not a substitute for
                proper bedding on stone floors.

---
## Currency

currency:
  gold: 5
  silver: 0
  copper: 0

other_valuables: []

---
## Encumbrance

capacity:
  current_load: ~32 lbs (estimated)
  maximum: 50 lbs
  unit: lbs
  status: Unencumbered — full movement (40ft dungeon / 120ft open)
  # Note: BFRPG encumbrance thresholds — verify exact values in main rulebook.
  # Rule of thumb: STR 8 supports roughly 50 lbs before penalties apply.

---
## Notes

notes: >
  No hammer currently carried — iron spikes have limited utility without one.
  Spellbook is stored in the scroll case at all times during travel.
  Torches are for the party, not Caerwyn — her Darkvision covers her.
  At 5 gp remaining, the next priority purchase when in town should be
  a hammer (for the spikes) and possibly a backup weapon or healing supplies.
