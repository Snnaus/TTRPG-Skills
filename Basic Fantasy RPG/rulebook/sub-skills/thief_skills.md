# thief_skills.md — Generated Sub-Skill
# SKILL: rulebook/sub-skills/thief_skills.md
# FORMAT VERSION: 1.0
# Parent system: Basic Fantasy RPG, 3rd Edition (r127)

---
## Purpose

handles: All seven Thief ability checks — when and how to roll them, who rolls,
         Sneak Attack resolution, and situational penalties.
invoked_when: >
  The player's character is a Thief (or Elf Magic-User/Thief) and attempts one of
  the seven Thief abilities, or declares a Sneak Attack.
does_not_handle: >
  Non-Thief improvised stealth or lockpicking attempts — those are DM adjudication,
  not Thief skill rolls. Sneak Attack damage is resolved in combat_resolution after
  this sub-skill confirms the Thief is in position.

---
## Rules Reference

# From mechanics.md — Unique Mechanics: Thief Skills
# Thief Abilities table from character PDF (page 9) — percentage values at each level.

SEVEN THIEF ABILITIES:
  1. Open Locks      — unlock a lock without the key (one attempt per lock per level)
  2. Remove Traps    — rolled twice: once to detect, once to disarm
  3. Pick Pockets    — lift an item from a target without being noticed
  4. Move Silently   — pass through an area without making sound (GM rolls)
  5. Climb Walls     — scale sheer surfaces with few or no handholds
  6. Hide in Shadows — conceal the Thief's presence in any shadowed area (GM rolls)
  7. Listen at Door  — detect sounds through a closed door or wall (GM rolls)

PERCENTAGE VALUES (selected levels from character PDF — roll d100, equal or under = success):

  Level | Open Locks | Remove Traps | Pick Pockets | Move Silently | Climb Walls | Hide | Listen
    1   |     25     |      20      |      30      |      25       |     80      |  10  |   30
    2   |     30     |      25      |      35      |      30       |     81      |  15  |   34
    3   |     35     |      30      |      40      |      35       |     82      |  20  |   38
    4   |     40     |      35      |      45      |      40       |     83      |  25  |   42
    5   |     45     |      40      |      50      |      45       |     84      |  30  |   46
   10   |     68     |      63      |      74      |      68       |     89      |  53  |   65
   15   |     83     |      78      |      94      |      83       |     94      |  68  |   80
   20   |     88     |      83      |      99      |      93       |     99      |  73  |   95

  (Full table in character PDF, page 9)

WHO ROLLS:
  Player rolls: Open Locks, Remove Traps, Climb Walls.
  GM rolls (secretly): Move Silently, Hide in Shadows, Listen at Door, Pick Pockets.
  The Thief always believes they are moving silently and hiding successfully — the GM
  reveals failure only through consequences, not by announcing a failed roll directly.

SNEAK ATTACK:
  Requirements: Thief attacks from behind an opponent who is unaware of their presence.
  The GM may call for a Move Silently or Hide roll first to confirm the Thief is unseen.
  Attack: +4 bonus to attack roll. On hit: double normal damage.
  Limitations: May not be used on the same target twice in a single combat encounter.
               Can be performed bare-handed (subduing damage — knockout, not lethal).
               Can use the flat of a blade (also subduing damage, +0 to hit, normal damage).

---
## Resolution Procedure

steps:
  1. "IDENTIFY THE ABILITY. The Thief declares what they are attempting. Match it to
      one of the seven abilities. If it doesn't match any, it's an improvised action —
      adjudicate with an ability score check instead."

  2. "CHECK PRECONDITIONS.
      Open Locks: requires Thieves' picks and tools (else -20% penalty or impossible).
      Hide in Shadows: Thief must remain still. Moving breaks concealment.
      Climb Walls: Cannot be done in plate mail. Chain mail imposes a penalty (GM sets).
      Sneak Attack: Thief must be behind and undetected. Call Move Silently or Hide
                    first if the Thief is not already confirmed as hidden."

  3. "DETERMINE WHO ROLLS.
      Player rolls: Open Locks, Remove Traps, Climb Walls — tell the player their
      current percentage and ask them to roll d100.
      GM rolls secretly: Move Silently, Hide, Listen, Pick Pockets — roll internally.
      Do not announce a failed secret roll. Surface consequences through narration."

  4. "APPLY SITUATIONAL MODIFIERS. Add or subtract percentage points for difficult
      circumstances. Examples:
      — Slimy or wet wall surface: -20% to Climb Walls
      — Very loud ambient noise: -10% to Listen
      — Target is alert and watching: -20% to Pick Pockets
      — Magical lock: GM discretion, may make Open Locks impossible or add -20%"

  5. "RESOLVE THE ROLL.
      Roll ≤ modified percentage: success. Narrate the outcome with confidence.
      Roll > modified percentage: failure.
        — Open Locks/Remove Traps: tell the player immediately (they know it failed).
          Open Locks: cannot try again until next level.
          Remove Traps: first roll (detect) failing means they don't know it's there.
                         Second roll (disarm) failing triggers the trap.
        — Pick Pockets: if the roll exceeds the target by more than 2× the percentage,
          the victim notices. Narrate accordingly.
        — Secret rolls: do not reveal the failure. Narrate as if uncertain — let the
          consequence reveal it (the Thief thinks they're hidden; the guard notices anyway)."

  6. "SNEAK ATTACK — if confirmed hidden and attacking from behind:
      Add +4 to the attack roll. Call combat_resolution with this modifier noted.
      If the attack hits: double the damage roll. Narrate a vicious, unexpected strike."

---
## Edge Cases

edge_cases:
  - situation: "Non-Thief player wants to attempt lock-picking or moving silently"
    ruling: "No formal roll exists for non-Thieves. Adjudicate: is it plausible given
             their background and current equipment? If yes, set a chance (25–50%
             depending on situation) and roll d100. Do not use Thief skill percentages."

  - situation: "Thief wants to use Sneak Attack against an enemy who has already been
               in combat with them this round"
    ruling: "The enemy is aware of the Thief. Sneak Attack is unavailable unless the
             Thief has used Move Silently or Hide to re-establish concealment. Resolving
             whether the Thief successfully vanishes mid-combat is DM adjudication."

  - situation: "Thief tries to Listen through a 3-foot stone wall"
    ruling: "Apply a significant penalty (-30% or more). Very thick stone may make
             it impossible. If impossible: tell the player before they roll."

---
## Integration Notes

reads_from:
  - "mechanics.md → Unique Mechanics: Thief Skills"
  - "player/character-sheet.md → level (to look up percentage) and skills section"

outputs_to:
  - "Narration: Successes described confidently; failures revealed through consequences."
  - "combat_resolution: Calls back with Sneak Attack modifier if applicable."

triggers_other_sub_skills:
  - "combat_resolution — for the actual Sneak Attack roll and damage after confirming position"
