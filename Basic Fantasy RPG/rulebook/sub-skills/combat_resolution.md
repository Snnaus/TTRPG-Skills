# combat_resolution.md — Generated Sub-Skill
# SKILL: rulebook/sub-skills/combat_resolution.md
# FORMAT VERSION: 1.0
# Parent system: Basic Fantasy RPG, 3rd Edition (r127)

---
## Purpose

handles: All combat turns — initiative, attack rolls, damage, conditions, defeat.
invoked_when: >
  Any time hostile action begins: a monster attacks, the player declares an attack,
  an ambush occurs, or any participant draws a weapon with intent to harm. Remains
  active until all enemies are defeated, flee, or the combat is otherwise resolved.
does_not_handle: >
  Saving throws triggered during combat (see saving_throws sub-skill).
  Spell effects during combat (see spell_resolution — call it when a spell is cast,
  then return here for its aftermath). Thief Sneak Attack setup (see thief_skills —
  call it to determine if the Thief is hidden; Sneak Attack damage is resolved here).

---
## Rules Reference

# From mechanics.md — Combat Structure section, reproduced here for fast access.

INITIATIVE
  Each side rolls 1d6 at the start of combat. Player may add DEX modifier if GM permits.
  Highest roll acts first. All members of that side act before the other side.
  On a tie: both sides act simultaneously. Damage is applied immediately; a character
  can be killed on the same action they deliver a killing blow.

TURN STRUCTURE (each combatant, each round)
  Move: up to full movement rate (~40ft dungeon / ~120ft open field).
  Attack OR Cast Spell OR Use Item OR Other Action (one significant action per turn).
  Movement may be split before and after the action at GM discretion.

ATTACK ROLL
  Melee:   1d20 + Attack Bonus + STR modifier ≥ target AC → hit
  Ranged:  1d20 + Attack Bonus + DEX modifier ≥ target AC → hit
  Range modifiers for missile weapons:
    Short range (+1 to the roll) / Medium range (no modifier) / Long range (-2 to the roll)
  Attack Bonus is determined by class and level — consult class tables in main rulebook.

DAMAGE
  Melee:  Roll weapon die + STR modifier. Minimum 1 on a successful hit.
  Ranged: Roll weapon die only. DEX modifier does NOT add to ranged damage.
  Weapon damage dice (from character PDF):
    Dagger: 1d4 | Hand Axe: 1d6 | Shortsword/Warhammer/Mace: 1d6
    Longsword/Scimitar/Battle Axe: 1d8 | Two-Handed Sword/Pole Arm/Great Axe: 1d10
    Club/Staff/Cudgel: 1d4 | Sling stone: 1d4 | Sling bullet: 1d4
    Shortbow: 1d6 | Longbow: 1d8 | Light Crossbow: 1d6 | Heavy Crossbow: 1d8

ARMOR CLASS VALUES
  No Armor: 11 | Leather: 13 | Chain Mail: 15 | Plate Mail: 17
  Shield: +1 to AC (stacks with armor)
  DEX modifier applied directly to AC.

CONDITIONS (combat-relevant)
  Surprised: Cannot act during the surprise round. Opponent attacks freely.
  Casting Disrupted: If the caster is hit while casting, spell is lost. Damage still applied.
  Paralyzed: Cannot move or act. Attackers gain advantage (GM may grant +4 to hit or auto-hit).
  Dead / At Zero HP: By default 0 HP = dead. Confirm optional house rules with player at session start.

---
## Resolution Procedure

steps:
  1. "ESTABLISH COMBAT. Hostile intent declared or monster attacks. Announce: combat begins."

  2. "CHECK FOR SURPRISE. Did one side fail to notice the other? If yes, the surprised side
      loses their first turn entirely. Surprised characters cannot act or defend normally.
      Roll 1d6: on 1–2, that side is surprised (adjust for racial abilities — Elves and
      Halflings reduce surprise chance for the party)."

  3. "ROLL INITIATIVE. Each side rolls 1d6. Announce the turn order: 'The [monsters] act
      first this round.' On a tie, simultaneous — resolve damage from both sides before
      removing any casualties."

  4. "WINNING SIDE ACTS. For each acting character or monster on the winning side:
      a. Declare their action (attack, spell, move, item use).
      b. If attacking: roll 1d20 + attack bonus + relevant modifier.
         Compare result to target's AC. Equal or higher = hit.
      c. If hit: roll weapon damage die + modifier. Apply to target's HP.
      d. If casting: spell goes off (call spell_resolution). Announce effect.
      e. If using an item: apply its effect immediately.
      f. Narrate the outcome in second person for player actions; third person for monsters."

  5. "LOSING SIDE ACTS. Repeat step 4 for the other side. If a character was killed in
      step 4 during simultaneous initiative, they still act this round."

  6. "APPLY END-OF-ROUND EFFECTS. Any conditions with round-based duration tick down.
      Announce if any condition expires."

  7. "CHECK COMBAT STATUS.
      - All enemies at 0 HP or fled → combat ends. Narrate the outcome.
      - Player at 0 HP → character is dead (or unconscious per house rule). Narrate.
      - Combat ongoing → return to step 3 for the next round."

  8. "POST-COMBAT. Note HP losses. Surviving enemies may be looted. Award XP at session end
      (not mid-session — track it in the session summary). Update room status in layout.md."

---
## Edge Cases

edge_cases:
  - situation: "Player wants to do something not on the action list (e.g., shove an enemy, disarm)"
    ruling: "Allow it. Roll 1d20 + STR or DEX modifier (whichever fits) vs. a target the GM sets
             based on the enemy's size and resistance. On success, narrate the effect — push back,
             drop weapon, etc. This is not a formal rule; adjudicate consistently."

  - situation: "Monster has immunity to normal weapons"
    ruling: "Non-magical weapons simply deal no damage. Announce this on the first failed hit
             with flavor: 'Your blade passes through it as if through smoke.' The player should
             infer they need silver, magic, or fire. Don't state the rule directly — let them
             figure it out."

  - situation: "Multiple monsters of the same type attacking one player"
    ruling: "Each monster rolls its attack separately. There is no ganging-up bonus in Basic
             Fantasy RPG unless the monster's description specifies one. Resolve each attack
             in order, applying damage before the next attack — a player could be killed mid-sequence."

  - situation: "Player tries to flee combat"
    ruling: "Player moves at full movement rate away from enemies. Enemies may pursue or attack
             the fleeing character (GM discretion). A character in melee who turns to flee may
             take a free attack from the enemy. Fleeing ends combat for that character."

  - situation: "Player attacks a surprised enemy or an enemy that doesn't know they're there"
    ruling: "Call thief_skills if the player is a Thief using Sneak Attack. For non-Thieves:
             the player may get a free attack before initiative is rolled (the surprised enemy
             cannot act). Treat it as a normal attack — no bonus damage, just initiative advantage."

  - situation: "Spellcaster is hit while casting"
    ruling: "Spell is lost. The slot for that spell is expended. The hit deals normal damage.
             Announce: 'The blow breaks your concentration — the spell unravels.' Update spell
             slots in the session summary."

---
## Integration Notes

reads_from:
  - "mechanics.md → Combat Structure (initiative, turn structure, defeat rules)"
  - "mechanics.md → Core Stats (STR for melee attack/damage, DEX for ranged attack/AC)"
  - "player/character-sheet.md → current HP, attack bonus, equipped weapon, AC"
  - "companions/[name]/character-sheet.md → companion HP and attack stats"
  - "dungeons/[dungeon-name]/rooms/[current-room].md → enemy stats, cover, hazards, zones"

outputs_to:
  - "Narration: DM describes each attack, hit, miss, and defeat in second-person present tense."
  - "Session summary: Net HP changes for player and companions, noted as character_deltas."
  - "Room file: Update room status to 'cleared' when all enemies are defeated."
  - "session-log.md: Key combat events noted in key_events at session end."

triggers_other_sub_skills:
  - "spell_resolution — when any character or monster declares a spell action"
  - "saving_throws — when an attack or effect requires a save (poison, paralysis, etc.)"
  - "thief_skills — when a Thief declares a Sneak Attack (to confirm hidden status first)"
  - "turn_undead — when a Cleric declares a Turn Undead attempt against undead enemies"
