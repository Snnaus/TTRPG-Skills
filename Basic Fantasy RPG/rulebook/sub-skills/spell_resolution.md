# spell_resolution.md — Generated Sub-Skill
# SKILL: rulebook/sub-skills/spell_resolution.md
# FORMAT VERSION: 1.0
# Parent system: Basic Fantasy RPG, 3rd Edition (r127)

---
## Purpose

handles: Spell slot tracking by class and level, spell declaration and timing,
         interrupted casting, arcane vs. divine differences, spell effects resolution.
invoked_when: >
  A Magic-User or Cleric (or Elf combination class) declares a spell on their turn,
  or when a monster casts a spell. Also invoked when a player asks what spells remain.
does_not_handle: >
  Attack rolls made as part of a spell (e.g., if a spell creates a bolt that requires
  an attack roll, resolve the roll in combat_resolution). Saving throws called for by
  spells (see saving_throws). Scrolls and magic items work differently — adjudicate
  from the item description.

---
## Rules Reference

# From mechanics.md — Unique Mechanics: Spells

ARCANE SPELLS (Magic-Users and Elves)
  Magic-Users begin knowing Read Magic + one other 1st-level spell.
  New spells must be found as written scrolls or in spellbooks and copied.
  Magic-Users may NOT wear armor or use shields.
  Elves (Fighter/Magic-User) may cast spells while wearing armor.
  Elves (Magic-User/Thief) may cast spells while wearing leather armor.

DIVINE SPELLS (Clerics)
  Clerics pray for spells — no spellbook required. Access is granted by deity.
  Clerics gain spells starting at 2nd level (no spells at level 1).
  Clerics may wear any armor but only use blunt weapons.

SPELLS PER DAY (from class tables in character PDF — representative values):
  Cleric:      Level 1: —/— | Level 2: 1 | Level 3: 2 | Level 4: 2/1 | Level 5: 2/2
               (columns = spell levels 1–6; dashes = no slots that spell level)
  Magic-User:  Level 1: 1 | Level 2: 2 | Level 3: 2/1 | Level 4: 2/2 | Level 5: 2/2/1
  See full tables in character PDF (pages 7–8) for levels 1–20.

SPELL LEVELS: 1 through 6 for both Clerics and Magic-Users. Higher-level spells are
more powerful and require higher character level to access.

CASTING: Spell is cast on the caster's turn. Takes the full turn action.
  If the caster is struck before their turn arrives (initiative loss) or struck while
  casting, the spell fails and the slot is expended.

PREPARATION: At the start of each day (after 8 hours of rest), the caster chooses
  which spells to memorize (Magic-User) or pray for (Cleric). Chosen spells fill the
  available slots. A slot is expended when the spell is cast, whether or not it
  has its intended effect (disrupted spells still cost the slot).

---
## Resolution Procedure

steps:
  1. "SPELL DECLARATION. The player (or monster) declares: casting a spell. Note which
      spell and its target(s). Note the current slot count before the cast."

  2. "CHECK IF CASTING IS SAFE. Did the caster act before being struck this round?
      If initiative went to the enemy and the caster was hit before their turn:
      the spell is disrupted. Narrate the disruption. Expend the slot. Skip to step 6."

  3. "EXPEND THE SLOT. Mark the appropriate spell level slot as used. If no slot
      remains for that spell level, the caster cannot cast it — tell the player:
      'You reach for that spell and find it gone from your mind.'"

  4. "RESOLVE THE EFFECT. Apply the spell's stated effect.
      — If the spell allows a saving throw: call saving_throws sub-skill. Apply
        success/failure result to the spell's outcome.
      — If the spell requires an attack roll: call combat_resolution for that roll.
      — If the spell deals damage with no save: apply damage directly.
      — If the spell has a duration: note the duration and track it."

  5. "NARRATE THE CAST. Describe the spell in second person for the player's character
      or third person for companions/monsters. Keep descriptions vivid and brief.
      Avoid naming the spell mechanically — describe what happens:
      'A bolt of searing force leaps from your hands...' not 'You cast Magic Missile.'"

  6. "UPDATE SPELL SLOTS. At session end, include current spell slots in character_deltas
      so the player can update their character sheet. Slots refresh after a full rest
      (8 hours). Track rest in narration — if the party has not rested, slots stay spent."

---
## Edge Cases

edge_cases:
  - situation: "Player wants to cast a spell not yet in their spellbook (Magic-User)"
    ruling: "Cannot be cast. The spell must be written in the spellbook and prepared that
             day. Narrate: 'That formula hasn't been committed to memory.' Offer the
             spells they do have prepared as options."

  - situation: "Cleric wants to cast a spell they haven't prayed for that day"
    ruling: "Cannot be cast. Clerics receive spells through prayer at day's start.
             Narrate: 'The words of prayer won't come — you didn't prepare for this.'
             Only exception: GM may allow a one-time plea for divine intervention at
             story-critical moments (rare, GM discretion)."

  - situation: "Spell targets an area and hits both enemies and allies"
    ruling: "All targets in the area are affected equally. Apply saves for each target
             individually. This is a player decision — warn the player of the risk before
             resolving: 'The blast will catch [ally] as well. Do you cast anyway?'"

  - situation: "Caster wants to know how many spell slots they have left"
    ruling: "Load the character sheet. State clearly: '[Name] has X first-level slots and
             Y second-level slots remaining.' Then return to narration."

---
## Integration Notes

reads_from:
  - "mechanics.md → Unique Mechanics: Spells (slot tables, casting rules)"
  - "player/character-sheet.md → resources section (current spell slots)"
  - "companions/[name]/character-sheet.md → companion spell slots if applicable"

outputs_to:
  - "Narration: Spell effect described vividly without breaking fiction."
  - "Session summary: Spell slot expenditure listed in character_deltas for player update."

triggers_other_sub_skills:
  - "saving_throws — for any spell that specifies a saving throw"
  - "combat_resolution — if the spell requires an attack roll to deliver its effect"
