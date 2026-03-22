# turn_undead.md — Generated Sub-Skill
# SKILL: rulebook/sub-skills/turn_undead.md
# FORMAT VERSION: 1.0
# Parent system: Basic Fantasy RPG, 3rd Edition (r127)

---
## Purpose

handles: Cleric Turn Undead attempts — when it applies, the 2d6 roll, reading the
         result against the Turn Undead table, duration of effects, and evil Cleric variant.
invoked_when: >
  A Cleric (or Cleric combination class, if applicable) declares a Turn Undead attempt.
  The target must be an undead creature. Can be attempted each round if undead are present.
does_not_handle: >
  General combat with undead (see combat_resolution). Saving throws triggered by undead
  attacks like paralysis (see saving_throws). Spells the Cleric casts against undead
  (see spell_resolution).

---
## Rules Reference

# From mechanics.md — Unique Mechanics: Turn Undead

MECHANIC: Roll 2d6 and compare to the Turn Undead table, cross-referencing:
  — Cleric level (rows) vs. Undead type by Hit Dice (columns)

RESULTS:
  Turn:    Undead flee from the Cleric for 3d6 rounds. They cannot approach voluntarily.
  Destroy: Undead are annihilated — no roll, no save, they simply cease.
  Failure: No effect. Cleric may attempt again next round if they wish.

TURN UNDEAD TABLE:
  # Approximate values from BFRPG (verify against main rulebook p.57):
  # Column headers = Undead Hit Dice (Skeleton 1, Zombie 2, Ghoul 4, Wight 4, Wraith 5,
  #   Mummy 6, Spectre 6, Vampire 8+, Lich 11+, etc.)
  # Row headers = Cleric level

  Cleric Lvl | 1 HD | 2 HD | 3–4 HD | 5–6 HD | 7+ HD
      1      |  7   |  9   |   11   |   —    |   —
      2      |  T   |  7   |    9   |   11   |   —
      3      |  T   |  T   |    7   |    9   |   11
      4      |  D   |  T   |    T   |    7   |    9
      5      |  D   |  D   |    T   |    T   |    7
      6–7    |  D   |  D   |    D   |    T   |    T
      8+     |  D   |  D   |    D   |    D   |    T/D

  T = automatic Turn regardless of roll (no roll needed)
  D = automatic Destroy regardless of roll (no roll needed)
  Number = minimum 2d6 result required to Turn
  — = cannot affect this undead type at this level
  (Verify exact table values against main rulebook page 57)

HOW MANY AFFECTED: On a successful Turn, 2d6 HD worth of undead are affected,
  starting with the weakest. On Destroy, same determination.

EVIL CLERICS: An evil Cleric may Command undead instead of Turning. The undead
  obey the Cleric rather than fleeing. Use the same table and roll; success means
  Command, not Turn. Commanded undead serve until the next sunrise or the Cleric
  releases them.

---
## Resolution Procedure

steps:
  1. "CLERIC DECLARES TURN UNDEAD. The Cleric holds up their holy symbol and invokes
      divine power. This uses their action for the round — they cannot also attack."

  2. "IDENTIFY UNDEAD TYPE. What are the undead, and what is their approximate Hit
      Dice? Use the Turn Undead table column headers to find the right column:
      Skeleton ~1 HD / Zombie ~2 HD / Ghoul ~4 HD / Wight ~4 HD / Wraith ~5 HD /
      Mummy ~6 HD / Spectre ~6 HD / Vampire ~8+ HD / Lich ~11+ HD (approximate)."

  3. "LOOK UP THE TABLE. Find the intersection of Cleric level (row) and undead type
      (column).
      — If the cell shows T: automatic Turn. No roll needed. Go to step 5.
      — If the cell shows D: automatic Destroy. No roll needed. Go to step 6.
      — If the cell shows a number: roll 2d6. Equal to or higher than the number = Turn.
      — If the cell shows —: this undead type cannot be Turned at this level. Narrate
        failure. Return to combat_resolution."

  4. "ROLL 2d6 (if required). Compare to table value.
      — Equal or higher: Turn. Go to step 5.
      — Lower: Failure. Narrate: the undead are unmoved by the display of faith.
        Cleric may try again next round. Return to combat_resolution."

  5. "TURN EFFECT. Roll 2d6 to determine how many HD worth of undead are Turned.
      Affect the weakest undead first. Turned undead flee from the Cleric for 3d6 rounds.
      They cannot move toward the Cleric voluntarily during this time.
      Narrate: 'The undead recoil from the light — they scatter, stumbling away.'
      Note the duration. Return to combat_resolution for remaining combat."

  6. "DESTROY EFFECT. Roll 2d6 to determine how many HD worth of undead are Destroyed.
      Weakest first. They are annihilated — no HP loss, no saving throw, simply gone.
      Narrate: 'The holy light burns through them — they dissolve into ash and silence.'
      Return to combat_resolution if any undead remain."

---
## Edge Cases

edge_cases:
  - situation: "Mixed group of undead — some within the Cleric's Turn range, some not"
    ruling: "Resolve Turn for those that can be affected. Ignore those that cannot
             (e.g., a Lich when the Cleric is level 3). The Turned undead flee; the
             unaffected may still act freely."

  - situation: "Turned undead are cornered and cannot flee"
    ruling: "Turned undead cower and cannot attack voluntarily. They are functionally
             paralyzed in place. If struck, they still cannot retaliate during the Turn
             duration."

  - situation: "Evil Cleric wants to Command undead that another Cleric has Turned"
    ruling: "The competing divine power cancels — the stronger Cleric's effect holds.
             If same level, both effects cancel and the undead act freely. Use the
             Cleric's level as the tiebreaker; if tied, roll a contest (each rolls d20,
             highest wins)."

  - situation: "Can a Cleric Turn undead they created (e.g., via a spell)?"
    ruling: "Generally no — created undead obey their creator. GM discretion if the
             created undead have broken from control."

---
## Integration Notes

reads_from:
  - "mechanics.md → Unique Mechanics: Turn Undead"
  - "player/character-sheet.md → Cleric level"
  - "dungeons/[dungeon-name]/rooms/[current-room].md → undead enemy types and HD"

outputs_to:
  - "Narration: Turn/Destroy/Failure described through the visual drama of divine power."
  - "combat_resolution: Returns after resolving Turn/Destroy — remaining combat continues."
  - "Session summary: Turned or destroyed undead noted in room status update."

triggers_other_sub_skills:
  - "combat_resolution — returns here after Turn Undead resolves for remaining combat"
