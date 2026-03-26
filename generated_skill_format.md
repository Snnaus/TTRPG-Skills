# [mechanic-name].md — Generated Sub-Skill
# SKILL: rulebook/sub-skills/[mechanic-name].md
# FORMAT VERSION: 1.2
# Generated at setup by the parent DM skill.
# Parent system: [System name and edition]
# This sub-skill owns a specific mechanical domain during play.
# The parent SKILL.md routes to this file when that domain is invoked.

---
## Skill Constraints

# Generated sub-skills must follow these structural rules:

# SIZE: This file must stay under 200 lines. If the mechanic is too complex
# for a single sub-skill, split it into two sub-skills with clear boundaries
# (e.g. spell_resolution_casting and spell_resolution_effects). Register
# both in mechanics.md → sub_skills and define their routing relationship
# in the integration_notes section of each.
#
# ROUTING: Every sub-skill must define exactly when it is invoked and what
# it does NOT handle. Ambiguous boundaries between sub-skills cause the DM
# to load the wrong file or skip resolution entirely. When in doubt, make
# the boundary narrower and more explicit.
#
# SINGLE SOURCE OF TRUTH: Never copy rules from mechanics.md into this file.
# Reference by section heading. If mechanics.md is corrected, references
# stay valid automatically.

---
## Purpose

handles: [Mechanical domain — e.g. "All combat turns: initiative, actions, damage, conditions, defeat"]
invoked_when: >
  [The exact conditions under which the parent skill calls this sub-skill.
   Be specific — "combat" is too vague; "Combat begins (any hostile action is
   declared or enemies are encountered), and during any combat turn until all
   enemies are defeated or flee" is correct.]
does_not_handle: >
  [Explicitly state what falls outside this sub-skill's scope, to avoid overlap
   with other sub-skills. Name the sub-skill that does handle it.
   e.g. "Spell effects (see spell_resolution). Social opposed checks outside
   combat (see skill_checks)."]

---
## Rules Reference

# Point to the relevant sections of mechanics.md by heading name.
# Do NOT copy the rules here — mechanics.md is the single source of truth.

references:
  - file: mechanics.md
    sections:
      - [Section heading — e.g. "Combat Structure"]
      - [Additional section if needed — e.g. "Core Stats"]
  # Keep this lean — only what is needed to resolve this domain.

---
## Resolution Procedure

# Step-by-step instructions for how to run this mechanic during play.
# Written as a decision tree or ordered checklist.
# Reference specific mechanics.md fields by name rather than repeating values.
# If this section alone exceeds ~80 lines, the mechanic should be split
# into two sub-skills.

steps:
  1. [First step — e.g. "Establish whether combat is triggered: hostile intent
      declared, ambush initiated, or player attacks."]
  2. [Second step — e.g. "Roll initiative for all participants using the method
      in mechanics.md → Combat Structure → initiative."]
  3. [Continue through the full resolution process.]
  # Each step should be a single clear instruction.

---
## Edge Cases

# Common complications and how to resolve them.
# This section grows over time as rulings are made during play.
# If it grows past ~30 entries, split related edge cases into a
# separate reference file and link to it.

edge_cases:
  - situation: [e.g. "Player wants to take an action not listed in the rules"]
    ruling: [e.g. "Apply the core resolution mechanic with a relevant stat.
             Set difficulty based on mechanics.md → difficulty_scale."]
  - situation: [e.g. "Multiple conditions apply simultaneously"]
    ruling: [e.g. "Apply each independently unless they contradict; more
             severe takes precedence."]

---
## Integration Notes

# How this sub-skill connects to the rest of the system.
# This section is critical for routing — it tells the DM what to load
# alongside this sub-skill and where results go afterward.

reads_from:
  - [e.g. "mechanics.md → Combat Structure"]
  - [e.g. "player/character-sheet.md → stats and HP"]
  - [e.g. "rooms/[current-room].md → enemies and environmental features"]

outputs_to:
  - [e.g. "Narration: DM describes outcome"]
  - [e.g. "dm_files.md triggers: HP changes → update character-sheet.md"]
  - [e.g. "If enemy defeated: update room status in layout.md"]

triggers_other_sub_skills:
  - [Sub-skill invoked as a result of this one — e.g. "spell_resolution —
     if player declares a spell attack"]
  # Remove this section if no other sub-skills are triggered.

hands_back_to:
  - [Where control returns after this sub-skill completes —
     e.g. "dm_session.md → Active Play (beat-and-prompt resumes)"]
  # This field ensures the DM knows how to exit this sub-skill cleanly.
