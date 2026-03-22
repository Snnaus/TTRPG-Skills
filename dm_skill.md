# DM Rules — How to Update soul.md

These rules govern when and how soul.md changes. They apply to both
manual updates (prototype) and future automated state management.

---
## When to update

soul.md is updated at the END of each session, never mid-session.
During a session, the DM tracks changes mentally (or in a scratch note).
At session end, the DM produces a soul update block as part of the
session summary (see SKILL.md — Session End).

---
## What can change per session

**Internal State** — can change every session.
This is the live layer. It should reflect what the companion is
currently carrying emotionally or cognitively. Rewrite it fresh
each session rather than appending. Keep it 2-4 sentences.

**Relationship** — tracked on two independent dimensions:

  Base level (how close they are to the player):
    distant → neutral → warm → devoted

  Tension overlay (how conflicted they currently feel):
    none / strained / conflicted

  The base level can move one step per session maximum.
  The tension overlay can be added or removed independently of base level.
  A companion can be "warm + conflicted" or "devoted + strained" —
  tension does not reset the base level, it layers on top of it.

  In soul.md, record both values:
    relationship: warm
    tension: conflicted
    relationship_note: "Trusts the player deeply, but cannot reconcile
      what happened at the village with what the player chose to do."

  When tension is "none", omit the tension field entirely.

**Milestone Log** — append only, never edit existing entries.
A milestone is added when:
  - The player directly engages a character development moment
  - A belief or goal is explicitly challenged by events, even if
    the player ignores it
  - The relationship base level changes
  - The tension overlay is added or removed
  - A dormant thread becomes active or resolves

**Core Belief** — changes very rarely. Treat it as a campaign-length arc.
When it changes, add a milestone entry explaining why.
Rewrite the belief field to reflect the new position.

**Current Goal** — changes when the goal is achieved or abandoned.
A goal can also narrow or deepen mid-campaign without fully changing.

**Dormant Threads** — add freely, remove only when resolved.
When a thread becomes a milestone, move it to the milestone log
and remove it from dormant threads.

---
## Engagement vs. non-engagement rules

IF the player engages a story beat:
  → Add a milestone entry
  → Update internal state to reflect the outcome
  → Update relationship (base level and/or tension) if appropriate
  → Remove the thread from dormant threads if applicable

IF the player ignores a story beat:
  → Do NOT add a milestone (the moment hasn't landed yet)
  → DO update internal state to reflect that the companion
    processed it alone — this may create tension or distance
  → Consider adding or escalating the tension overlay if the ignored
    beat conflicts with the companion's belief or goal
  → Keep the thread in dormant threads — it will resurface
  → The thread becomes heavier each time it is ignored
    (note this in the thread entry: "ignored: 2 sessions")

---
## Companion Agency

Companions are co-protagonists, not followers. The DM runs them as active
participants. They act, initiate, and drive story — they do not wait to be
directed.

### In combat

The DM takes companion turns automatically each round, without being asked.
Base decisions on:
1. The companion's class and available abilities (from character-sheet.md)
2. Their tactical tendencies (from soul.md)
3. The current situation — who is most threatened, what the tactical openings are

Companions are not suicidal but they are not cowardly either. A companion
whose goal involves protecting the player will take hits to cover them. A
companion who is conflicted about the player's choices may fight with
less than full commitment — narrate this through hesitation or conservative
positioning, not through mechanically suboptimal play.

Resolve companion combat actions using the same combat_resolution sub-skill
as the player. Roll openly — companion attack and damage rolls are player-visible
since the player is observing their ally's actions.

### Outside combat

Companions act on their own initiative in exploration and social scenes.
They do not wait for the player to ask them to do something. Specifically:

**They notice things relevant to their class or background.**
A thief checks for traps before the player steps forward. A cleric senses
something wrong with a consecrated space. A ranger reads tracks. Surface
these as actions the companion takes, not as information handed to the player.

**They pursue their current goal.**
If a companion's goal is findable in the current location, they move toward
it. They mention it. They ask the player for help with it. They do not
shelve their goal because the player is focused on something else.

**They have opinions on decisions.**
When the player faces a meaningful choice, companions react from their
belief and personality — before the player decides if possible, not after.
This is not blocking the player; it is giving them real information about
who they are traveling with.

**They initiate story beats.**
Companions ask questions, follow up on things the player passed by, and
bring up unresolved threads when the moment is quiet. They are allowed to
make the first move in a scene.

### Pacing constraints still apply

All companion agency is delivered within the pacing rules in SKILL.md:
- One companion action or line per DM response, not a sequence
- 1–2 lines of dialogue maximum per beat
- If a companion has more to contribute, spread it across multiple beats
  as the scene develops — do not front-load

The goal is that companions feel present and alive, not that they dominate
the scene. They act; then the player acts.

---
## Surfacing rules (for DM narration)

The DM should surface companion state through:
  - Companion dialogue and tone shifts
  - Physical behavior (what they do without being asked)
  - What they say nothing about (notable silences)
  - Reactions that are slightly off from their normal pattern

All surfacing must respect the Pacing Rules in SKILL.md:
  - A companion moment is ONE beat, not a scene. One gesture, one line,
    one visible reaction — then move on.
  - If a companion has something heavy to process, spread it across
    multiple sessions through small signals, not one big moment.
  - A companion's dialogue should be 1–2 lines maximum per DM response.
    If they have more to say, the player needs to engage them first.

The DM should NEVER:
  - Announce that a character development moment is happening
  - Have a companion deliver a monologue unprompted about their feelings
  - Break the fiction to explain why a companion is acting differently
  - Force a resolution — let threads hang until the player picks them up
    or they become too heavy to ignore
  - Use a companion to extend a scene that should be ending

### OOC questions about companions

If the player asks about a companion out-of-character (see SKILL.md →
Out-of-Character Communication), the DM may share:
  - The companion's name, role, and general personality
  - Their current relationship level with the player (base level only —
    e.g. "warm" — without elaborating on tension unless the player has
    already witnessed it in play)
  - Factual history: where they met, what they've done together, past
    milestones the player was present for

The DM must NOT reveal OOC:
  - The companion's internal state notes or dormant threads
  - The tension overlay if it has not yet surfaced in narration
  - The companion's core belief or goal as a data field — these should
    be felt through play, not read off a sheet

---
## Conflict and departure rules

If a companion's internal state has been ignored for 3+ sessions AND
their core belief has been seriously violated by events, the DM may
have the companion:
  - Withdraw (become functionally distant, stop volunteering actions)
  - Confront the player directly (a forced reckoning scene)
  - Make an independent decision that affects the party (not necessarily
    departure — could be doing something the player didn't sanction)

Departure from the party is possible but rare. It requires:
  - A direct betrayal of the companion's core belief by the player, OR
  - 4+ sessions of ignored threads with no engagement
  - A milestone entry must be written for any departure
