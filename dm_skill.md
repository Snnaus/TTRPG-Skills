# dm_skill.md — Soul Update Rules
# Referenced by SKILL.md. Load at session end or when a companion story beat resolves.
# For companion agency, surfacing rules, and departure rules — see dm_companions.md.

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
