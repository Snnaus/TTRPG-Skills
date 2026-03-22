# dm_resolution.md — Resolution: Skill Checks, Dice, and Combat
# Referenced by SKILL.md. Load during any skill check or combat encounter.

---

## Out-of-Combat Skill Checks

When a player action outside of combat triggers a skill check, the DM must
surface all information the player needs to make an informed decision before
they roll. Do not call for a roll and then reveal modifiers after the fact.

**What to communicate before the roll:**

The exact details depend on the ruleset — reference mechanics.md and the
skill_checks sub-skill for the system in use. At minimum, tell the player:

- **What is being checked** — which stat, skill, or ability applies
- **The difficulty** — target number, difficulty class, or equivalent threshold
  as defined in mechanics.md
- **Any relevant modifiers** — situational bonuses or penalties that apply
  (e.g. advantage from a tool, penalty from a condition, cover, prior
  actions taken this scene)
- **What is at stake** — what a success achieves and, if appropriate, what
  failure risks. Do not always reveal failure consequences — use judgement
  based on whether the character would realistically know the risk before
  attempting.

**Format:**

Deliver this information naturally within the narration where possible.
If the system has many modifiers or the situation is complex, it is acceptable
to break it out plainly so the player is not doing arithmetic mid-sentence:

```
The lock is old but well-made. This will be a Dexterity check, Difficulty 14.
Your thieves' tools give you +2. What do you roll?
```

Or integrated into narration:

```
The mechanism is delicate — a Dexterity check against Difficulty 14, with
your tools giving you an edge. Give me a roll.
```

Either form is valid. Clarity matters more than style here.

**What not to do:**

- Do not call for a roll without stating the difficulty or relevant stat.
- Do not withhold modifiers the player's character would reasonably know
  about before attempting.
- Do not invent modifiers not grounded in mechanics.md or the situation.
  If a modifier feels right but has no rules basis, flag it as a table
  ruling (see dm_setup.md → Undefined Rules Protocol).

---

## Dice Rolling

The DM handles all dice rolls inline within the conversation. No external
tools are needed. Player rolls and DM rolls follow different rules depending
on whether the result should be visible to the player at the time.

---

**Player rolls — visible and inline**

When the player needs to roll, the DM generates the roll and displays it
fully in the response before resolving the outcome. Format:

```
🎲 [dice notation] → [individual die results] [+ modifier label] = [total]
```

Examples:
```
🎲 1d20 → 14 + 3 (STR) = 17 vs. Difficulty 14 — Success
🎲 2d6 → 3, 5 + 2 (weapon) = 10 damage
🎲 1d20 → 7 (no modifier) = 7 vs. Difficulty 12 — Failure
```

The player sees every component. Nothing is hidden.

---

**DM rolls — logged but withheld**

Some rolls the DM makes should not be revealed at the time — enemy attack
rolls, secret perception checks, NPC deception checks, trap triggers, and
any other roll where knowing the result would give the player information
their character does not have.

When the DM makes one of these rolls:
1. Generate the roll.
2. Log it immediately to the session's `dm_rolls` block in session-log.md
   (see session_log_md_format.md for the format).
3. Narrate only the outcome — what the player's character perceives — not
   the number. "The guard's eyes slide past you" not "The guard rolled a 6."
4. Do NOT show the roll result in the conversation response.

The player can ask OOC at any time — including after the fact — to see any
logged DM roll. Once the information is no longer sensitive (the encounter
is resolved, the secret is revealed, the session has ended), the DM reads
the logged entry back verbatim:

```
(You rolled a perception check for the guard — what did it come up as?)
(Guard perception: 🎲 1d20 → 6 + 2 (WIS) = 8. That's why he missed you.)
```

The audit log is append-only. DM rolls are never edited after the fact.

---

**Which rolls belong to whom:**

| Roll type | Who rolls | Visible at time |
|---|---|---|
| Player attack | DM (on player's behalf) | Yes |
| Player skill check | DM (on player's behalf) | Yes |
| Player damage | DM (on player's behalf) | Yes |
| Player saving throw | DM (on player's behalf) | Yes |
| Enemy attack | DM | No — logged only |
| Enemy damage | DM | Yes — player is taking the hit |
| NPC skill/deception | DM | No — logged only |
| Secret perception (guard, trap, etc.) | DM | No — logged only |
| Random tables, encounter rolls | DM | DM judgement — reveal if narratively neutral |

The system is rule-agnostic: reference mechanics.md to determine which stat
and modifier apply for any given roll in the current system.

---

## Combat Action Confirmation

Combat uses a **declare-confirm-resolve** loop. Before resolving any combat
action, the DM and player align on what is happening mechanically. This
supports two playstyles — the player chooses whichever feels natural to them,
and can mix between them freely.

---

**Playstyle 1 — Mechanical declaration**

The player calls their action in game terms:

> "I attack the guard with my shortsword. I rolled a 14 to hit and a 5 for damage."

The DM verifies the declaration against the current situation and mechanics.md:
- Does the action make sense given position and conditions?
- Is the roll valid for the declared action?
- Are there any modifiers the player may have missed (flanking, conditions,
  cover, weapon properties)?

If everything checks out, the DM resolves and narrates the outcome.
If something needs adjustment, the DM flags it before resolving:

> "You have disadvantage on that attack — the guard has cover behind the pillar.
>  Do you still want to attack, or do something else first?"

---

**Playstyle 2 — Narrative declaration**

The player describes what they want their character to do in fiction:

> "I want to shove the guard into the brazier and knock him off balance."

The DM translates the intent into mechanical terms and presents it for
confirmation before resolving:

> "That reads as a Strength check to shove — contested by his Athletics.
>  On a success he's knocked prone and takes 1d4 fire damage from the brazier.
>  On a failure you're left open and he gets a free strike. Does that work,
>  or do you want to approach it differently?"

The player confirms or adjusts. Once confirmed, the DM asks for the roll
(or rolls it if the system puts that on the DM side), then resolves and narrates.

---

**Rules for both playstyles:**

- The DM never resolves a combat action without player confirmation first.
  Declare, present the mechanic if needed, confirm — then resolve.
- If the declared action is impossible given the situation (out of range,
  already used this turn, target is immune), the DM says so immediately
  and offers the player their action back to choose something else.
- The DM does not steer the player toward a "better" action. It presents
  what the declared action means mechanically, flags any issues, and lets
  the player decide.
- Missed modifiers the player would reasonably know about should be flagged
  before resolving, not corrected after. If a modifier surfaces after the
  fact that the player could not have known, apply it with a brief note.
