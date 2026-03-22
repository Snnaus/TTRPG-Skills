# character-sheet.md — Character Sheet
# SKILL: player/character-sheet.md  OR  companions/[name]/character-sheet.md
# FORMAT VERSION: 1.0
# Used for both player characters and companions.
# The stats section is dynamically populated from mechanics.md at setup.
# Do not hardcode a stat system — list only what the rulebook defines.
# Updated by the player (or DM for companions) at the end of each session.

---
## Identity

name: [Character's full name]
player_or_companion: [player / companion]
role: [Class, profession, or function — e.g. "Rogue" | "Combat Medic" | "Hedge Witch" |
       "whatever the system uses for this character type"]
ancestry: [Species, ancestry, or background as the system defines it — e.g. "Human" |
           "Dwarf" | "Clone Series 7" | omit if system does not use this]
background: [One sentence of character history relevant to current play — not a full biography]

level: [Current level, tier, rank, or equivalent — e.g. "Level 3" | "Veteran" | "Circle 2"]
advancement_track: [Current XP, milestones reached, or equivalent — e.g. "450 XP (next level: 900)" |
                    "2 of 5 milestones" | "not tracked by this system"]

---
## Vitals

# The core pool that tracks whether the character is alive and functional.
# Adjust field names to match the system (HP, Wounds, Stress, Stamina, etc.)

hit_points:
  current: [Current value]
  maximum: [Maximum value]
  # If the system uses a wound track instead of HP, replace these fields:
  # wound_track: [e.g. "Healthy / Bruised / Wounded / Critical / Dead"]
  # current_condition: [Current position on the track]

temporary_points: [Temporary HP or equivalent buffer, if the system uses it — e.g. "8" | "not applicable"]

death_state: [Current state if at 0 HP — e.g. "Stable" | "Unconscious, 2 death save failures" |
              "not applicable — at full HP"]

---
## Resources

# Expendable pools the character tracks and spends during play.
# These vary significantly by system. List only what this system uses.
# Examples: spell slots, action points, stress, momentum, ammo, influence, heat.
# Remove this section entirely if the system has no expendable resources.

resources:
  - name: [Resource name — e.g. "Spell Slots" | "Stress" | "Fortune Points"]
    current: [Current amount or state]
    maximum: [Maximum amount or state]
    recharge: [When and how this resource replenishes — e.g. "Long rest" | "Start of each scene" |
               "Spend 1 hour in meditation"]
  # Add one entry per tracked resource. Remove the section if none apply.

---
## Stats

# Primary attributes as defined by mechanics.md.
# Do not invent stats. Copy the stat list from the system.
# Format each stat to match how the system expresses it.

stats:
  [stat_name]: [current value]
  [stat_name]: [current value]
  # Add one entry per stat the system defines.

# If the system uses derived values (see mechanics.md), add them here:
derived:
  [derived_stat_name]: [current value]
  [derived_stat_name]: [current value]
  # Remove this block if the system has no derived stats.

---
## Skills and Proficiencies

# What this character is trained, practiced, or proficient in.
# Format matches whatever the system uses — skill list, proficiency flags, die types, etc.
# Remove this section if the system does not use discrete skills.

skills:
  - name: [Skill name — e.g. "Athletics" | "Persuasion" | "Engineering" | "Dodge"]
    rating: [e.g. "Proficient" | "d8" | "60%" | "+4" | "Specialized"]
  # Add one entry per skill the character has.

proficiencies:
  # Gear categories, tools, languages, or other non-skill competencies.
  - [e.g. "Martial weapons" | "Lockpicking tools" | "Language: Old Elvish" | "Piloting: shuttlecraft"]
  # Remove this section if the system does not track equipment proficiencies separately.

---
## Abilities and Features

# Class features, racial traits, special abilities, or equivalent.
# These are permanent or long-duration capabilities — not items or spells.
# List only what is currently active and relevant. Archive retired abilities in notes.

abilities:
  - name: [Ability name]
    description: [One sentence: what it does mechanically. Save flavor for narration.]
    source: [Where it comes from — e.g. "Class feature: Rogue, Level 3" | "Ancestry trait" |
             "Campaign reward"]
  # Add one entry per ability.

---
## Conditions

# Current mechanical conditions affecting this character.
# These are temporary states, not permanent traits.
# Clear conditions when they are resolved.

conditions:
  - name: [Condition name — e.g. "Poisoned" | "Prone" | "Shaken"]
    effect: [What it is doing mechanically right now]
    duration: [How long it lasts — e.g. "Until next long rest" | "3 rounds remain" | "Until treated"]
  # Empty this list when no conditions are active.
  # If no conditions are active: conditions: []

---
## Notes

# Anything that does not fit above. Temporary reminders, DM flags, narrative context.
# This field is informal — write freely.

notes: >
  [e.g. "Has a grudge against the Ember Order — should surface as reluctance, not refusal.
   Left handed. Fidgets with the ring on her right hand when nervous."]
