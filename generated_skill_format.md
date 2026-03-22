# [mechanic-name].md — Generated Sub-Skill
# SKILL: rulebook/sub-skills/[mechanic-name].md
# FORMAT VERSION: 1.1
# Generated at setup by the parent DM skill.
# Parent system: [System name and edition]
# This sub-skill owns a specific mechanical domain during play.
# The parent SKILL.md routes to this file when that domain is invoked.

---
## Purpose

# What this sub-skill handles and when it is invoked.
# Be specific — the parent skill needs to know exactly when to delegate here.

handles: [Mechanical domain — e.g. "All combat turns: initiative, actions, damage, conditions, defeat"]
invoked_when: >
  [The conditions under which the parent skill calls this sub-skill.
   e.g. "Combat begins (any hostile action is declared or enemies are encountered),
   and during any combat turn until all enemies are defeated or flee."]
does_not_handle: >
  [Explicitly state what falls outside this sub-skill's scope, to avoid overlap
   with other sub-skills. e.g. "Spell effects (see spell_resolution). Social
   opposed checks outside combat (see skill_checks)."]

---
## Rules Reference

# Point to the relevant sections of mechanics.md by heading name.
# Do NOT copy the rules here — mechanics.md is the single source of truth.
# If mechanics.md is corrected, these references stay valid automatically.
# When this sub-skill is loaded into context, load the referenced sections
# of mechanics.md alongside it (see Context Management in SKILL.md).

references:
  - file: mechanics.md
    sections:
      - [Section heading — e.g. "Combat Structure"]
      - [Additional section if needed — e.g. "Core Stats"]
  # For combat_resolution: reference "Combat Structure" + "Core Stats"
  # For skill_checks: reference "Resolution Mechanic" + "Core Stats"
  # For spell_resolution: reference the relevant "Unique Mechanics" entry + "Core Stats"
  # Keep this lean — only what is needed to resolve this domain.

---
## Resolution Procedure

# Step-by-step instructions for how to run this mechanic during play.
# Written as a decision tree or ordered checklist.
# The goal: a consistent, repeatable process that does not require the DM to improvise rules.
# Reference specific mechanics.md fields by name (e.g. "Use the difficulty_scale
# from mechanics.md") rather than repeating their values.

steps:
  1. [First step — e.g. "Establish whether combat is triggered: hostile intent declared,
      ambush initiated, or player attacks."]
  2. [Second step — e.g. "Roll initiative for all participants using the method in
      mechanics.md → Combat Structure → initiative. Sort by the order rule. Announce
      turn order to player."]
  3. [Continue through the full resolution process for this mechanic.]
  # Add as many steps as needed. Each step should be a single clear instruction.

---
## Edge Cases

# Common complications and how to resolve them.
# Each entry is a situation the DM may encounter and the correct ruling.

edge_cases:
  - situation: [e.g. "Player wants to take an action not listed in the rules"]
    ruling: [e.g. "Apply the core resolution mechanic with a relevant stat. Set difficulty
             based on the difficulty scale in mechanics.md. Narrate the outcome."]
  - situation: [e.g. "Multiple conditions apply to the same character simultaneously"]
    ruling: [e.g. "Apply each condition's effect independently unless they directly
             contradict, in which case the more severe condition takes precedence."]
  # Add edge cases discovered during play. This section grows over time.

---
## Integration Notes

# How this sub-skill connects to other parts of the system.
# Prevents the DM from having to re-derive cross-mechanic interactions.

reads_from:
  - [File and section this sub-skill references — e.g. "mechanics.md → Combat Structure"]
  - [e.g. "player/character-sheet.md → stats and HP"]
  - [e.g. "rooms/[current-room].md → enemies and environmental features"]

outputs_to:
  - [Where results of this sub-skill are reported — e.g. "Narration: DM describes outcome"]
  - [e.g. "Session end: HP changes noted in session summary for player to apply to character-sheet.md"]
  - [e.g. "If enemy is defeated: update room status in layout.md at session end"]

triggers_other_sub_skills:
  - [Sub-skill that may be invoked as a result of this one —
     e.g. "spell_resolution — if player declares a spell attack"]
  - [e.g. "sanity_checks — if player witnesses an extreme horror event during combat"]
  # Remove this section if no other sub-skills are triggered.
