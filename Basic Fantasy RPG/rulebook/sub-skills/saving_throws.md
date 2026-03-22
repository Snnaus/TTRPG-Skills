# saving_throws.md — Generated Sub-Skill
# SKILL: rulebook/sub-skills/saving_throws.md
# FORMAT VERSION: 1.0
# Parent system: Basic Fantasy RPG, 3rd Edition (r127)

---
## Purpose

handles: All five saving throw categories — when to call for them, how to resolve them,
         racial and ability modifiers, and how to narrate success or failure.
invoked_when: >
  Any time a character faces a hazard covered by one of the five saving throw categories:
  poison, death effects, magic wand attacks, paralysis or petrification, breath weapons,
  or spells with a saving throw listed in their description.
  Also invoked when a monster ability calls for a save.
does_not_handle: >
  Thief ability rolls (see thief_skills). Non-combat improvised checks based on ability
  scores (no formal system — DM adjudicates). Attack rolls even if magically enhanced
  (see combat_resolution).

---
## Rules Reference

# From mechanics.md — Unique Mechanics: Saving Throws

FIVE CATEGORIES (each has its own target number per class and level):
  1. Death Ray or Poison — covers instant-death attacks and ingested/injected toxins
  2. Magic Wands — covers attacks from wands, staves, and rods
  3. Paralysis or Petrify — covers paralysis (ghouls, spells) and petrification (medusa, basilisk)
  4. Dragon Breath — covers breath weapon attacks from dragons and similar monsters
  5. Spells — covers offensive spells that allow a save for reduced or negated effect

RESOLUTION: Roll 1d20. If the result is equal to or greater than the character's target
number for that category, the save succeeds.

TARGET NUMBERS: Listed in class saving throw tables (main rulebook). Lower numbers mean
better saves — target numbers decrease as characters gain levels.

RACIAL MODIFIERS (applied to base class saving throw values):
  Dwarves:  +4 vs. Death Ray or Poison / +4 vs. Magic Wands /
            +4 vs. Paralysis or Petrify / +3 vs. Dragon Breath / +4 vs. Spells
  Halflings: Same bonuses as Dwarves.
  Elves:    +1 vs. Paralysis or Petrify / +2 vs. Magic Wands / +2 vs. Spells
  Humans:   No racial saving throw bonuses.

WISDOM MODIFIER: May apply to saving throws vs. magical attacks (GM discretion per
main rulebook). When applied, add WIS modifier to the saving throw roll.

---
## Resolution Procedure

steps:
  1. "IDENTIFY THE TRIGGER. An attack, spell, or hazard requires a save. Determine which
      of the five categories applies:
      — Poison, death ray → Death Ray or Poison
      — Wand/staff/rod attack → Magic Wands
      — Ghoul touch, hold spell, medusa gaze → Paralysis or Petrify
      — Dragon breath weapon → Dragon Breath
      — Offensive spell with save listed → Spells"

  2. "LOOK UP THE TARGET NUMBER. Find the character's saving throw target for the
      identified category. Use the class saving throw table (main rulebook).
      Apply racial bonus to reduce the target number (lower = easier to save):
      e.g., Dwarf base target 14 vs. Poison → adjusted to 10 (14 - 4 bonus)."

  3. "CALL FOR THE ROLL. Narrate the threat, then:
      'Roll a saving throw vs. [category]. You need a [target number] or higher.'
      Do not break the fiction with category names if possible — use the effect:
      'The ghoul's paralytic touch reaches for you — can you resist?'"

  4. "APPLY THE RESULT.
      SUCCESS (roll ≥ target): Character avoids or reduces the effect. Narrate the
      resistance — the character shakes off the poison, leaps away from the breath,
      breaks free of the hold.
      FAILURE (roll < target): Apply the full effect. Narrate it — the character
      succumbs to the poison, turns to stone, drops unconscious."

  5. "TRACK ONGOING EFFECTS. If the failed save produces a duration-based condition
      (paralysis, slow, etc.), note the duration. Check each round or as appropriate."

---
## Edge Cases

edge_cases:
  - situation: "Character does not know what type of save to make"
    ruling: "The GM determines the category from the source of the threat. The player
             does not need to know the category name — just the target number. Narrate
             the hazard, call the number."

  - situation: "Multiple hazards require saves in the same round (e.g., dragon breathes and bites)"
    ruling: "Resolve saves one at a time in order of occurrence. Each save is independent.
             Failing one does not carry over to the next."

  - situation: "A spell says 'save for half damage'"
    ruling: "On a failed save: full damage. On a successful save: roll damage as normal,
             then halve the result (round down). Apply this halved total to HP."

  - situation: "Paralysis from a ghoul — how long does it last?"
    ruling: "Per Basic Fantasy RPG: paralysis caused by ghouls lasts 2d4 turns (20–80 minutes)
             unless a Remove Paralysis spell or similar magic is used. Track turns elapsed.
             A paralyzed character cannot act — enemies attack them at advantage (GM may
             rule auto-hit or +4 to attack rolls)."

---
## Integration Notes

reads_from:
  - "mechanics.md → Unique Mechanics: Saving Throws (target numbers, racial modifiers)"
  - "player/character-sheet.md → saving throw values and racial modifiers"
  - "companions/[name]/character-sheet.md → companion saving throw values"

outputs_to:
  - "Narration: Success or failure described through the character's physical or mental response."
  - "Session summary: Conditions caused by failed saves noted in character_deltas."

triggers_other_sub_skills:
  - "combat_resolution — if the failed save results in damage that reduces HP"
