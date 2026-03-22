# mechanics.md — Parsed Rulebook
# SKILL: rulebook/mechanics.md
# FORMAT VERSION: 1.0
# Generated at setup by the parent DM skill from player-provided rulebook text.
# This is the canonical rule reference for all sub-skills during play.
# Do not edit mid-campaign unless applying official errata.
# Sub-skills read from this file — they do not store their own rule copies.

---
## System

name: [Full name of the TTRPG system]
edition: [Edition, printing, or version — e.g. "5th Edition" | "Revised" | omit if not applicable]
setting: [Genre and tone — e.g. "dark fantasy", "cosmic horror", "pulp space opera", "domestic drama"]
source: [How rules were provided — e.g. "pasted core rulebook sections", "player described from memory", "summary provided"]

---
## Core Stats

# Every primary attribute or stat the system uses.
# For each: its name, what it governs mechanically, and how it is expressed.
# Do not invent stats. List only what the system actually uses.

stats:
  - name: [Stat name]
    governs: [What this stat affects during play]
    format: [How it is expressed — e.g. "numeric score 1–20 with derived modifier" |
             "die type d4 through d12" | "percentage 1–100" | "rated 1–5"]
  # Repeat for each stat the system uses.

derived_values:
  # Stats calculated from primary stats. HP, armor, initiative, speed, etc.
  # Remove this section entirely if the system has no derived values.
  - name: [Derived stat name]
    formula: [How it is calculated — plain language, not algebraic]
  # Repeat as needed.

---
## Resolution Mechanic

# How the system determines success or failure.
# This section is the core of all mechanical resolution — be precise.

roll_type: [One-line summary — e.g. "roll d20, add modifier, meet or beat a target number" |
            "roll a pool of d6s, count successes" | "draw a card from a standard deck" |
            "roll 2d6 and add a stat; 10+ is a hit, 7–9 is a partial, 6- is a miss"]

core_formula: >
  [Plain-language description of how a standard check works from start to finish.
   Include: what is rolled, what is added, what it is compared against, and what
   constitutes success versus failure. Write for someone who has never seen this system.]

difficulty_scale:
  # The system's named difficulty levels and their mechanical values.
  # Adjust the number of entries to match the system.
  - label: [e.g. "Trivial" | "Easy" | "Simple"]
    value: [e.g. "DC 8" | "Difficulty 1" | "target number 5"]
  - label: [e.g. "Moderate" | "Standard"]
    value: [e.g. "DC 13"]
  - label: [e.g. "Hard" | "Difficult"]
    value: [e.g. "DC 18"]
  - label: [e.g. "Extreme" | "Legendary"]
    value: [e.g. "DC 25+"]

critical_results:
  # Does the system have exceptional success or catastrophic failure conditions?
  critical_success:
    condition: [When it triggers — e.g. "natural maximum on the die" | "exceed target by 10+" | "not used"]
    effect: [What happens — e.g. "automatic success with added benefit" | "not used"]
  critical_failure:
    condition: [When it triggers — e.g. "natural minimum on the die" | "fail by 5 or more" | "not used"]
    effect: [What happens — e.g. "automatic failure; DM may introduce a complication" | "not used"]

contested_checks:
  # How opposing rolls work when two characters resist each other.
  method: [e.g. "Both parties roll; higher result wins. Ties favor the defender." |
           "Attacker rolls against a static defense value." | "not used"]

---
## Combat Structure

# Complete rules for structured conflict.
# If the system does not use traditional combat turns, describe its actual structure.

initiative:
  method: [How turn order is determined at the start of combat]
  order: [Which end of the result goes first — e.g. "highest acts first" | "lowest acts first"]
  ties: [How tied initiative is resolved — e.g. "player chooses" | "reroll" | "simultaneous"]

turn_structure:
  # What a character may do on their turn.
  # List action types with a brief description of each.
  # Do not invent action types the system does not have.
  actions:
    - [Action type and what it allows — e.g. "Main action: one significant act (attack, cast, interact, etc.)"]
    - [Add further action types as the system defines them]

damage:
  method: [How damage is calculated and applied]
  types: [Named damage types if the system tracks them — e.g. "fire, piercing, psychic" |
          "not differentiated — all damage reduces the same pool"]
  resistances: [How damage reduction or immunity works — e.g. "resistance halves; immunity negates" |
                "armor absorbs a flat amount" | "not used"]

conditions:
  # Status effects that mechanically alter a character's capabilities.
  # List only conditions with gameplay impact. Pure flavor conditions can be omitted.
  - name: [Condition name]
    effect: [What this condition changes mechanically]
  # Add one entry per condition the system defines.

defeat:
  player_at_zero: [What happens when player reaches 0 HP or equivalent defeat state]
  death_mechanics: [If there is a process between 0 HP and death — e.g. "death saving throws" |
                    "bleeding out for X rounds" | "immediate death" | "not used"]
  recovery: [How a player recovers — short rest, long rest, healing items, etc.]
  enemy_defeat: [Default outcome when enemies reach 0 HP or defeat threshold]

---
## Advancement

# How characters grow over the course of a campaign.

type: [e.g. "XP-based level progression" | "milestone leveling" | "narrative advancement" |
       "skill point allocation between sessions" | "permanent stat improvement on major events"]

tracking:
  method: [How advancement is measured and awarded]
  thresholds: [What triggers a level-up or advancement — e.g. specific XP totals, milestones, session count]

level_benefits:
  # What a player gains when they advance. Describe the pattern, not every exact value.
  - [e.g. "Maximum HP increases"]
  - [e.g. "New class features unlock at defined thresholds"]
  - [e.g. "One new skill or proficiency may be chosen"]
  # Add or remove to match what the system provides.

---
## Unique Mechanics

# System-specific rules that do not fit the universal skeleton above.
# This section captures what makes this system feel like itself.
# Examples: spell slots, sanity, stress, vows, clocks, heat, momentum, corruption.
# Remove this section entirely if the system has no unique mechanics beyond the above.

unique_mechanics:
  - name: [Mechanic name]
    description: >
      [Plain-language description of how this mechanic works, when it comes into play,
       and what consequences it produces. Write for someone who has never seen this system.]
    sub_skill: [Name of the sub-skill generated to handle this mechanic, if any —
                e.g. "spell_resolution" | "sanity_checks" | "handled inline, no sub-skill"]
  # Add one entry per unique mechanic.

---
## Generated Sub-Skills

# Sub-skills created from this rulebook at setup time.
# The parent DM skill delegates to these during active play.
# Each sub-skill file lives at rulebook/sub-skills/[name].md

sub_skills:
  - name: [Sub-skill filename without extension — e.g. "combat_resolution"]
    handles: [What mechanical domain this sub-skill owns during play]
  # Add one entry per generated sub-skill.
  # At minimum expect: combat_resolution, skill_checks
  # Add more for any unique_mechanics that warranted their own sub-skill.
