# character-sheet.md — Character Sheet
# SKILL: player/character-sheet.md
# FORMAT VERSION: 1.0
# System: Basic Fantasy RPG, 3rd Edition (revision 127)

---
## Identity

name: Caerwyn
player_or_companion: player
role: Magic-User
ancestry: Elf
background: A wandering elf scholar whose research into old ruins drew the attention of something she would rather not name — so she left her tower, took a dagger, and started asking questions underground instead.

level: Level 1
advancement_track: 0 XP (next level: 2,500 XP) — +5% XP bonus from Prime Requisite (INT 15)

---
## Vitals

hit_points:
  current: 3
  maximum: 3

temporary_points: not applicable

death_state: not applicable — at full HP
# Note: Basic Fantasy RPG default is 0 HP = dead. Confirm with GM at session start
# whether an optional unconscious/dying rule is in use.

---
## Resources

resources:
  - name: Spell Slots (Level 1)
    current: 1
    maximum: 1
    recharge: After a full night's rest (8 hours in safety). Spells must be re-memorized
              from spellbook — 1 hour of study required. If the spellbook is unavailable,
              no spells can be recovered.

---
## Stats

stats:
  STR: 8   # modifier: -1 (melee attack rolls, melee damage; penalty cannot reduce damage below 1)
  INT: 15  # modifier: +1 (Prime Requisite — grants +5% XP bonus; +1 bonus language)
  WIS: 9   # modifier:  0 (saves vs. magical attacks)
  DEX: 7   # modifier: -1 (missile attack rolls, Armor Class, initiative)
  CON: 10  # modifier:  0 (HP per hit die)
  CHA: 10  # modifier:  0 (NPC reactions, retainer limit and loyalty)

derived:
  armor_class: 10          # base 11 (no armor), DEX -1
  attack_bonus_melee: +0   # then apply STR -1 to attack roll and damage (min 1 damage on hit)
  attack_bonus_ranged: +0  # then apply DEX -1 to attack roll; DEX does NOT add to ranged damage
  movement: 40ft per round (dungeon) / 120ft per round (open ground)

  saving_throws:
    death_ray_or_poison: 13   # Magic-User base
    magic_wands: 12           # Magic-User base 14, Elf +2
    paralysis_or_petrify: 12  # Magic-User base 13, Elf +1
    dragon_breath: 16         # Magic-User base
    spells: 13                # Magic-User base 15, Elf +2
    # Note: WIS modifier (0) applies to saves vs. magical attacks — no change here.

---
## Skills and Proficiencies

skills: []
# Basic Fantasy RPG does not define a discrete skill system.
# Non-combat tasks are resolved by GM adjudication using ability scores as a guide.

proficiencies:
  - "Weapons: Dagger, walking staff only (Magic-User class restriction)"
  - "Armor: None — Magic-Users may not wear armor of any kind"
  - "Language: Common"
  - "Language: Elvish"
  - "Language: Dwarvish"

---
## Abilities and Features

abilities:
  - name: Darkvision
    description: Sees in total darkness up to 60ft (black and white only). Does not require
                 a light source in dark environments.
    source: Ancestry trait — Elf

  - name: Detect Secret Doors
    description: Automatically notices secret or hidden doors on a 1-in-6 chance when moving
                 within 10ft; 2-in-6 when actively searching. No action required for passive detection.
    source: Ancestry trait — Elf

  - name: Immune to Ghoul Paralysis
    description: Immune to the paralysis caused by ghoul touch attacks. Other sources of
                 paralysis (spells, certain monsters) still apply.
    source: Ancestry trait — Elf

  - name: Spellcasting (Arcane)
    description: May cast one memorized 1st-level spell per day. If struck while casting,
                 the spell is lost and the slot is wasted. Spells are re-memorized from
                 the spellbook after a full night's rest (1 hour study).
    source: Class feature — Magic-User, Level 1

  - name: XP Bonus (+5%)
    description: Earns 5% additional XP on all awards because INT (Prime Requisite) is 13+.
    source: Class feature — Magic-User (Prime Requisite rule)

---
## Spellbook

spells_known:
  - name: Read Magic
    level: 1
    description: Allows reading of magical writing, spell scrolls, and runic inscriptions.
                 Duration 1 turn. Does not consume a spell slot when used to read writing
                 already identified as magical.

  - name: Sleep
    level: 1
    description: Puts 2d8 HD worth of living creatures to sleep within a 30ft area.
                 No saving throw. Affects weakest HD creatures first.
                 Does not affect undead, constructs, or creatures with more than 4+1 HD.
                 Sleeping creatures can be slain automatically (1 round per creature).
                 Duration 4d4 turns or until woken.

spell_memorized:
  - Sleep
  # Re-memorize after rest. Swap to Read Magic if magical text is anticipated.

---
## Conditions

conditions: []

---
## Notes

notes: >
  Caerwyn is extremely fragile in direct combat (3 HP, AC 10, STR/DEX both at -1).
  Sleep is her primary offensive tool — capable of neutralizing entire groups of weak
  enemies in one cast. Once it is spent, she has a dagger and her wits.
  Darkvision makes her the party's eyes in unlit dungeons.
  The spellbook is irreplaceable — losing it means no spell recovery until a new one
  is found or purchased (25 gp). It is stored in the scroll case during travel.
  Background and personality to be developed in play.
