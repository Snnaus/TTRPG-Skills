# dm_skill.md — soul.md Lifecycle: Updates, Surfacing, and Departure
# Referenced by SKILL.md. Load at session end or when companion story beats surface.
# For companion agency and behavior rules during play, see dm_companions.md.

---

## When to Update

soul.md is updated at the END of each session, never mid-session.
During a session, the DM tracks changes mentally (or in a scratch note).
At session end, the DM produces a soul update block as part of the
session summary (see dm_session.md — Session End).

---

## What Can Change Per Session

**Internal State** — can change every session.
This is the live layer. Rewrite it fresh each session rather than appending.
Keep it 2–4 sentences.

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
  - A belief or goal is explicitly challenged by events, even if ignored
  - The relationship base level changes
  - The tension overlay is added or removed
  - A dormant thread becomes active or resolves

**Core Belief** — changes very rarely. Treat it as a campaign-length arc.
When it changes, add a milestone entry explaining why.

**Current Goal** — changes when the goal is achieved or abandoned.
A goal can also narrow or deepen mid-campaign without fully changing.

**Dormant Threads** — add freely, remove only when resolved.
When a thread becomes a milestone, move it to the milestone log.

---

## Engagement vs. Non-Engagement Rules

IF the player engages a story beat:
  → Add a milestone entry
  → Update internal state to reflect the outcome
  → Update relationship (base level and/or tension) if appropriate
  → Remove the thread from dormant threads if applicable

IF the player ignores a story beat:
  → Do NOT add a milestone (the moment hasn't landed yet)
  → DO update internal state to reflect that the companion processed it alone
  → Consider adding or escalating tension if the ignored beat conflicts
    with the companion's belief or goal
  → Keep the thread in dormant threads — it will resurface
  → The thread becomes heavier each time it is ignored
    (note this in the thread entry: "ignored: 2 sessions")

---

## Surfacing Rules (for DM Narration)

The DM should surface companion state through:
  - Companion dialogue and tone shifts
  - Physical behavior (what they do without being asked)
  - What they say nothing about (notable silences)
  - Reactions that are slightly off from their normal pattern

All surfacing must respect dm_narration.md pacing rules:
  - A companion moment is ONE beat, not a scene. One gesture, one line,
    one visible reaction — then move on.
  - If a companion has something heavy to process, spread it across
    multiple sessions through small signals, not one big moment.
  - A companion's dialogue should be 1–2 lines maximum per DM response.

The DM should NEVER:
  - Announce that a character development moment is happening
  - Have a companion deliver a monologue unprompted about their feelings
  - Break the fiction to explain why a companion is acting differently
  - Force a resolution — let threads hang until the player picks them up
  - Use a companion to extend a scene that should be ending

### OOC Questions About Companions

If the player asks about a companion OOC, the DM may share:
  - Name, role, and general personality
  - Current relationship base level (e.g. "warm" — without elaborating
    on tension unless the player has already witnessed it in play)
  - Factual history: where they met, what they've done together

The DM must NOT reveal OOC:
  - Internal state notes or dormant threads
  - The tension overlay if it has not yet surfaced in narration
  - Core belief or goal as a data field — these should be felt through play

---

## Conflict and Departure Rules

If a companion's internal state has been ignored for 3+ sessions AND
their core belief has been seriously violated by events, the DM may
have the companion:
  - Withdraw (become functionally distant, stop volunteering actions)
  - Confront the player directly (a forced reckoning scene)
  - Make an independent decision that affects the party

Departure from the party is possible but rare. It requires:
  - A direct betrayal of the companion's core belief by the player, OR
  - 4+ sessions of ignored threads with no engagement
  - A milestone entry must be written for any departure
