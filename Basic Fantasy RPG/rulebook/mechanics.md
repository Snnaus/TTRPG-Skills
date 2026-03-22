# mechanics.md — Parsed Rulebook
# SKILL: rulebook/mechanics.md
# FORMAT VERSION: 1.0
# System: Basic Fantasy RPG, 3rd Edition (revision 127)
# Source: "Basic Fantasy Character.pdf" (character creation rules, pages 4–14)
#         System knowledge for combat mechanics — main rulebook (r127) could not be
#         extracted due to file size. Flag any rules questions to the main rulebook PDF.

---
## System

name: Basic Fantasy Role-Playing Game
edition: 3rd Edition, Revision 127
setting: Classic dungeon-crawl fantasy — swords, sorcery, dungeons, and monsters.
         Tone is old-school: lethal, mysterious, and wondrous in equal measure.
source: Character creation PDF (pages 4–14) + system reference knowledge.
        Main rulebook pages 51–65 (Encounter/Combat section) not directly extracted.

---
## Core Stats

# Six primary abilities, each scored 3–18 at character creation.
# Modifier table (applies to all six stats):
#   Score 3     → -3
#   Score 4–5   → -2
#   Score 6–8   → -1
#   Score 9–12  →  0
#   Score 13–15 → +1
#   Score 16–17 → +2
#   Score 18    → +3

stats:
  - name: Strength
    governs: Melee attack rolls and melee damage rolls. Prime Requisite for Fighters.
             A penalty here will never reduce damage below 1 on a successful hit.
    format: Numeric score 3–18 with derived modifier per table above.

  - name: Intelligence
    governs: Number of languages the character can learn (bonus adds to base).
             A penalty means the character can barely read. Prime Requisite for Magic-Users.
    format: Numeric score 3–18 with derived modifier per table above.

  - name: Wisdom
    governs: Saving throws vs. magical attacks (bonus or penalty applied).
             Prime Requisite for Clerics.
    format: Numeric score 3–18 with derived modifier per table above.

  - name: Dexterity
    governs: Missile (ranged) attack rolls. Armor Class (modifier applied directly to AC).
             Initiative die rolls. Prime Requisite for Thieves.
    format: Numeric score 3–18 with derived modifier per table above.

  - name: Constitution
    governs: Each hit die roll gains the CON modifier (minimum 1 per die).
             After 9th level, the fixed HP bonus per level also uses CON modifier.
    format: Numeric score 3–18 with derived modifier per table above.

  - name: Charisma
    governs: Reaction rolls when encountering NPCs. Maximum number of retainers
             (hired followers) and their loyalty. Modifier applied to reaction rolls.
    format: Numeric score 3–18 with derived modifier per table above.

derived_values:
  - name: Hit Points (HP)
    formula: At level 1, roll the class hit die once + CON modifier (minimum 1).
             Each level gained, roll the class hit die again + CON modifier (minimum 1
             per roll). Add to maximum HP. After 9th level, add only a fixed value per
             class level (no new hit die roll) — Constitution modifier no longer applies.
             Hit dice by class: Fighter d8, Cleric d6, Thief d4, Magic-User d4.

  - name: Armor Class (AC)
    formula: Base 11 (no armor). Add armor bonus (Leather +2, Chain +4, Plate +6),
             shield bonus (+1), and DEX modifier. Higher AC is harder to hit.
             Examples: No armor = 11, Leather = 13, Chain = 15, Plate Mail = 17,
             Plate + Shield = 18.

  - name: Attack Bonus
    formula: Determined by class and level. Fighters advance fastest (+1 per level
             approximately). Clerics and Thieves advance at a moderate rate.
             Magic-Users advance slowest. See class combat tables in main rulebook
             (Encounter section, p. 51+). Apply STR modifier to melee attack rolls;
             DEX modifier to missile (ranged) attack rolls.

---
## Resolution Mechanic

roll_type: d20 + attack bonus vs. ascending Armor Class (for combat).
           Percentile roll under skill % (for Thief abilities).
           d20 roll vs. saving throw target number (for saves).
           Non-combat checks: no universal mechanic — DM adjudicates using ability
           scores as a guide.

core_formula: >
  COMBAT: Roll 1d20, add the character's attack bonus (from class/level), and any
  relevant ability modifier (STR for melee, DEX for ranged). If the result equals
  or exceeds the target's Armor Class, the attack hits and damage is rolled.

  THIEF SKILLS: Roll percentile dice (d100). If the result is equal to or less than
  the character's skill percentage for that ability, the action succeeds.

  SAVING THROWS: Roll 1d20. If the result equals or exceeds the character's saving
  throw target number for that category (lower numbers are better — they improve
  with level), the save succeeds and the effect is avoided or reduced.

  NON-COMBAT CHECKS: No universal mechanic defined. The GM sets a target and may
  ask for a relevant ability score roll, improvised as needed.

difficulty_scale:
  # Saving throws replace formal difficulty for most hazards. For improvised checks:
  - label: Easy
    value: DM-set target — approximately a 25–35% chance of failure for a capable character
  - label: Moderate
    value: DM-set target — approximately a 50% chance of failure
  - label: Hard
    value: DM-set target — approximately a 65–75% chance of failure
  - label: Near-Impossible
    value: DM-set target — only exceptional ability scores or favorable circumstances allow success

critical_results:
  critical_success:
    condition: not used — no formal critical success system in Basic Fantasy RPG
    effect: not used
  critical_failure:
    condition: not used — no formal fumble system. A natural 1 on an attack roll is
               simply a miss. DM may add flavor but no mechanical complication is required.
    effect: not used

contested_checks:
  method: Attacker rolls 1d20 + attack bonus vs. defender's static Armor Class.
          No opposed rolls — AC is fixed. For non-combat contested situations (e.g.,
          grappling, social manipulation) the GM adjudicates; no formal system exists.

---
## Combat Structure

initiative:
  method: Each side (player party vs. monsters) rolls 1d6 at the start of combat.
          Add DEX modifier if the GM permits individual initiative instead of group.
  order: Highest roll acts first. All members of the winning side act before the losing side.
  ties: Both sides act simultaneously — damage from ties is resolved at the same time,
        meaning a character can kill an enemy on the same turn the enemy kills them.

turn_structure:
  actions:
    - "Movement: Move up to the character's full movement rate (typically 40ft per round
       in a dungeon, 120ft in the open). May split movement before and after an attack
       at GM discretion."
    - "Attack: Make one attack roll against one target. Fighters of high enough level
       may gain additional attacks per round — check class table."
    - "Spell: Cast one prepared spell. Casting takes the full turn; if the caster is
       struck before the spell goes off, the spell is lost and the action is wasted."
    - "Use Item: Drink a potion, apply a bandage, retrieve a stored item, etc."
    - "Other Action: Any reasonable action the character can perform in about 10 seconds
       — pulling a lever, opening a door, calling out to an NPC. GM adjudicates."

damage:
  method: On a successful hit, roll the weapon's damage die. Add STR modifier for melee
          attacks (a penalty cannot reduce damage below 1 on a successful hit). DEX
          modifier does NOT add to ranged damage — only to the attack roll.
  types: Physical damage only — no formal elemental damage types. Magical weapons and
         spells produce specific effects as written but damage pools are unified (HP).
         Silver weapons matter for certain monsters (lycanthropes). Holy water damages undead.
  resistances: No formal resistance system. Certain monsters are immune to non-magical or
               non-silver weapons — attacks simply fail to deal damage. Spells note
               specific immunities in their descriptions.

conditions:
  - name: Unconscious / Dead
    effect: When HP reaches 0, the character may be dead. Not guaranteed — GM may
            rule unconscious if the campaign warrants it. By default: 0 HP = dead.
            Check main rulebook for optional 0 HP rules.

  - name: Paralyzed
    effect: Character cannot move or act. Frequently caused by monster special attacks
            (ghouls, certain spells). Duration and recovery vary by source.

  - name: Surprised
    effect: A surprised party cannot act during the surprise round. Opponent attacks
            freely. Surprise is determined at the start of an encounter before initiative.

  - name: Casting Disrupted
    effect: If a spellcaster is struck while casting a spell, the spell fails and the
            slot is wasted. The attack that disrupts casting still deals normal damage.

defeat:
  player_at_zero: Character reaches 0 HP. By default this means death. The GM may
                  allow an optional "unconscious and dying" state — check with your GM
                  at session start to confirm the ruling in use.
  death_mechanics: No formal death saving throw system. 0 HP = dead unless GM house-rules
                   otherwise. Some magic items or spells may allow resurrection.
  recovery: >
    Short rest (1 turn = 10 minutes): Bandaging and brief recovery. No HP restoration
    by default unless the GM allows it or a healing spell is used.
    Long rest (full night's sleep, 8 hours in safety): No automatic HP recovery in
    Basic Fantasy RPG by default. Healing magic is the primary recovery method.
    Clerics have healing spells. Potions of Healing restore 1d6+1 HP.
    Natural healing rate: 1 HP per day of complete rest (main rulebook — verify).
  enemy_defeat: Monster reaches 0 HP — dead. Some monsters or plot-significant enemies
                may be treated as unconscious at GM discretion.

---
## Advancement

type: XP-based level progression. Each class has its own XP threshold table (levels 1–20).

tracking:
  method: Earn XP by defeating monsters (based on HD and special abilities) and
          recovering treasure (1 gp = 1 XP is the classic standard — verify in rulebook).
          XP is awarded at the end of an adventure or at a safe rest point.
  thresholds: >
    Thresholds vary by class. Fighters advance the fastest, Magic-Users the slowest.
    Example milestones (from character PDF):
    Fighter — Level 2: 2,000 XP | Level 3: 4,000 XP | Level 4: 8,000 XP
    Cleric  — Level 2: 1,500 XP | Level 3: 3,000 XP | Level 4: 6,000 XP
    Thief   — Level 2: 1,250 XP | Level 3: 2,500 XP | Level 4: 5,000 XP
    Magic-User — Level 2: 2,500 XP | Level 3: 5,000 XP | Level 4: 10,000 XP
    Human characters receive a +10% bonus to all XP earned.
    Characters with a high Prime Requisite score (13+) also gain an XP bonus.

level_benefits:
  - "Maximum HP increases each level (roll class hit die + CON modifier, minimum 1)."
  - "Attack bonus improves on a class-based schedule (see main rulebook combat tables)."
  - "Saving throw values improve as the character gains levels (see saving throw tables)."
  - "Clerics gain access to higher-level spells (spell slots unlock per class table)."
  - "Magic-Users gain access to higher-level spells and more spells per day."
  - "Thieves see all skill percentages increase each level (per Thief Abilities table)."
  - "Fighters gain additional attacks per round at higher levels (see main rulebook)."
  - "Clerics gain access to Turn Undead at level 1."

---
## Unique Mechanics

unique_mechanics:
  - name: Saving Throws
    description: >
      Five distinct saving throw categories, each with its own target number that
      improves with level. All five use a 1d20 roll — meet or beat the target to succeed.
      Categories: Death Ray or Poison / Magic Wands / Paralysis or Petrify /
      Dragon Breath / Spells. Racial bonuses apply on top of class values:
      Dwarves and Halflings: +4 vs. Death Ray or Poison, +4 vs. Magic Wands,
      +4 vs. Paralysis or Petrify, +3 vs. Dragon Breath, +4 vs. Spells.
      Elves: +1 vs. Paralysis or Petrify, +2 vs. Magic Wands and Spells.
      Wisdom modifier may apply to saves vs. magical attacks.
      See saving throw tables by class in main rulebook.
    sub_skill: saving_throws

  - name: Spells (Arcane and Divine)
    description: >
      Magic-Users and Clerics cast spells. Spells are divided into levels 1–6.
      Magic-Users begin knowing Read Magic plus one other 1st-level spell.
      New spells must be found and copied into the spellbook.
      Clerics pray for spells — access depends on deity alignment.
      Spells per day are determined by class level (see class tables in character PDF).
      Spells must be declared and cast on the caster's turn; interrupted casting loses
      the spell. Elves may cast spells while wearing armor (Fighter/Magic-User combo).
      Magic-Users may NOT wear armor. Clerics may NOT use bladed or pointed weapons.
    sub_skill: spell_resolution

  - name: Thief Skills
    description: >
      Thieves have seven special abilities rated as percentages (1–99%):
      Open Locks / Remove Traps / Pick Pockets / Move Silently / Climb Walls /
      Hide in Shadows / Listen at Doors. All use a percentile roll (d100) equal
      to or under the listed percentage to succeed. The GM makes most of these rolls
      secretly on behalf of the player (the Thief does not know if they succeeded
      until consequences appear). Thief Abilities table in character PDF (page 9).
      Penalties may apply for difficult circumstances (GM discretion).
      Open Locks may only be attempted once per lock per level.
      Sneak Attack: +4 to hit, double damage, when attacking from concealment unseen.
    sub_skill: thief_skills

  - name: Turn Undead
    description: >
      Clerics (and Paladins, if used) may attempt to Turn Undead — driving off or
      destroying undead monsters through divine power. Roll 2d6 and compare to a
      Turn Undead table cross-referencing Cleric level vs. undead type (by Hit Dice).
      Results: Turn (undead flee for 3d6 rounds), Destroy (undead are annihilated),
      or Failure (no effect this attempt; may try again next round).
      Evil Clerics may instead Command undead rather than Turn them.
      See Turn Undead table in main rulebook (Encounter section).
    sub_skill: turn_undead

---
## Generated Sub-Skills

sub_skills:
  - name: combat_resolution
    handles: All combat turns — initiative, attack rolls, damage calculation,
             conditions (paralysis, surprise, disrupted spellcasting), defeat at 0 HP.

  - name: saving_throws
    handles: All five saving throw categories — when to call for them, how to resolve
             them, racial modifiers, Wisdom modifier application.

  - name: spell_resolution
    handles: Spell slot tracking by class and level, spell declaration and timing,
             interrupted casting, arcane vs. divine spell differences, spell effects.

  - name: thief_skills
    handles: All seven Thief ability checks — when the GM rolls vs. when the player
             rolls, Sneak Attack resolution, situational penalties.

  - name: turn_undead
    handles: Cleric Turn Undead attempts — when it applies, the 2d6 roll process,
             reading the result table, duration of effects.
