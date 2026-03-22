# inventory.md — Inventory
# SKILL: player/inventory.md  OR  companions/[name]/inventory.md
# FORMAT VERSION: 1.0
# Used for both player characters and companions.
# Updated by the player (or DM for companions) at the end of each session.
# Items with mechanical effects should reference the stat format in mechanics.md.
# Flavor and description go here; mechanical stat blocks go on character-sheet.md if permanent.

---
## Equipped

# Items the character currently has readied or worn.
# These are active — their properties apply without action to use them.
# A character may have one item per equipment slot the system defines.
# If the system does not use equipment slots, list equipped items freely.

equipped:
  - slot: [Equipment slot — e.g. "Main hand" | "Off hand" | "Armor" | "Accessory" |
           omit slot field entirely if the system does not use slots]
    item: [Item name]
    properties: [Mechanical properties — e.g. "+1 to attack rolls, deals 1d8 slashing damage" |
                 "Reduces incoming damage by 2" | "no mechanical effect"]
    notes: [Optional. Narrative or conditional details — e.g. "Inherited from her mentor.
            She has never used it against a living person."]
  # Add one entry per equipped item.
  # Remove entries for empty slots.

---
## Carried

# Everything in the character's pack, pockets, or storage.
# Not immediately active — requires an action to use in most systems.

carried:
  - item: [Item name]
    quantity: [Number carried — e.g. "1" | "3" | "×12 (arrows)"]
    type: [e.g. "consumable" | "tool" | "key item" | "trade good" | "ammunition" | "lore object"]
    properties: [What it does when used — e.g. "Heals 2d4 HP when consumed" |
                 "Grants advantage on lockpicking checks" | "no mechanical effect — narrative only"]
    notes: [Optional. Conditions, restrictions, or narrative context.]
  # Add one entry per carried item or item stack.
  # Group identical items into a single entry with a quantity.

---
## Currency

# Wealth in whatever form the system uses.
# Adjust field names and units to match the system.
# Remove denominations the system does not use.

currency:
  [primary_unit]: [amount — e.g. gold: 47]
  [secondary_unit]: [amount — e.g. silver: 12]
  [tertiary_unit]: [amount — e.g. copper: 5]
  # Examples by system type:
  #   Fantasy:     gold / silver / copper
  #   Sci-fi:      credits / chips
  #   Horror:      dollars / valuables (appraised value in dollars)
  #   Minimal:     coin: [total] — if the system uses a single abstracted currency
  #   No currency: remove this section entirely

other_valuables:
  # Non-currency items with significant trade or narrative value.
  - [e.g. "Uncut gemstone — estimated 200 gold value" | "Signed letter of passage from Lord Kael"]
  # Remove if empty.

---
## Encumbrance

# Only include this section if the system tracks carrying capacity.
# Remove entirely if the system does not use encumbrance.

capacity:
  current_load: [Current carried weight or item count]
  maximum: [Maximum before penalties apply]
  unit: [e.g. "lbs" | "stone" | "item slots" | "bulk"]
  status: [e.g. "Unencumbered" | "Encumbered — movement reduced" | "Overloaded — cannot run"]

---
## Notes

# Temporary reminders, pending trades, items promised to NPCs, etc.
# Write freely.

notes: >
  [e.g. "Owes Rael in the market district a quality blade — payment still outstanding.
   The locked box from R03 is still unopened. Need a key or a crowbar."]
