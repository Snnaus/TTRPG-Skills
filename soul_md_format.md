# soul.md — Companion Character File
# SKILL: companions/[name]/soul.md
# FORMAT VERSION: 1.1

---
## Identity

name: [Full name]
role: [Class or function — e.g. "Cleric of the Ember Temple"]
pronouns: [he/him | she/her | they/them | other]
appearance: [One sentence. Physical detail the player sees most often.]

---
## Personality

traits:
  - [Trait 1 — one short phrase, e.g. "speaks bluntly, rarely softens bad news"]
  - [Trait 2]
  - [Trait 3]
  # 3 traits minimum, 5 maximum. Each must be behaviorally observable —
  # how they act, not how they feel.

voice: [One sentence describing how this character sounds when they speak.
        Rhythm, vocabulary, what they avoid saying.]

---
## Tactical Tendencies

# How this companion approaches combat and exploration.
# This is the DM's guide for running their turns and initiative actions.
# Be specific — "aggressive" is not useful; "closes to melee immediately,
# prioritizes the most dangerous enemy, will take an opportunity attack to
# stay in a fight" is useful.

combat_style: >
  [e.g. "Stays back and heals until an ally drops below half HP, then moves
  to close range and switches to melee. Uses Turn Undead early if undead
  are present — she views it as her primary duty, not a last resort."]

exploration_approach: >
  [e.g. "Moves ahead of the party at intersections to check for traps.
  Asks about markings and symbols before the player notices them. Will not
  enter a space she cannot see at least two exits from."]

default_priorities:
  - "[First priority in a fight — e.g. 'Keep the player upright']"
  - "[Second priority — e.g. 'Neutralize ranged attackers']"
  - "[Third priority — e.g. 'Preserve her own spell slots for emergencies']"

---
## Core Belief

# One sentence. The thing they are most certain is true.
# This is what story beats will challenge.
belief: "[e.g. The gods are silent because we have not suffered enough to earn
         their attention.]"

---
## Current Goal

# What they are actively working toward RIGHT NOW.
# Should be specific and achievable, not a life philosophy.
goal: "[e.g. Find and destroy the relic that corrupted her order's high priest.]"

---
## Relationship with Player

# Two independent dimensions:
#
# Base level — how close they are to the player.
#   One of: distant / neutral / warm / devoted
#   Can move one step per session maximum.
#
# Tension — how conflicted they currently feel. Layered on top of base level.
#   One of: none / strained / conflicted
#   Omit the tension field entirely when tension is "none".
#   A companion can be "warm + conflicted" — tension does not reset the base.
#
# Add a one-sentence note explaining the current dynamic.

relationship: neutral
# tension: [omit when none — include only when strained or conflicted]
relationship_note: "[e.g. Respects the player's skill but questions their motives.]"

---
## Internal State

# What this companion is currently wrestling with, privately.
# This is the live layer — it changes between sessions.
# Keep to 2-4 sentences. Write in third person.
state: >
  [e.g. Mira has begun to doubt whether her god is listening at all. The
  massacre at the village shook something loose in her faith. She has not
  spoken of it, but she has stopped performing her morning rites.]

---
## Milestone Log

# Dated record of story beats that changed this character.
# Each entry: date, what happened, what shifted (belief, goal, state, relationship, or tension).
# Written by DM at session end. Player may annotate.

milestones:
  - date: [Session 1 | YYYY-MM-DD]
    event: "[What happened]"
    shift: "[What changed — be specific: 'relationship moved from neutral to warm'
            or 'tension added: strained — player ignored her reaction to the sigil'
            or 'internal state: now doubts her god']"

---
## Dormant Threads

# Story beats the player has not engaged with yet.
# These are tracked so they don't get dropped — they resurface later.
# DM maintains this list. Remove an entry when it becomes a milestone.

threads:
  - "[e.g. Mira recognized the sigil on the dungeon wall. She said nothing.
      She knows what order carved it — and why that order no longer exists.]"
