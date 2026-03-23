# dm_context.md — Context Window Management
# Referenced by SKILL.md. Active throughout every session.
# This sub-skill prevents the DM from losing critical rules, companion
# behavior, or game state as the conversation grows during a session.

---

## The Problem This Solves

In a long session, the conversation itself consumes the majority of the
context window. The earliest loaded content — mechanics.md, sub-skill
procedures, companion soul.md files — drifts out of effective attention.
When this happens:
- The DM starts resolving checks from general knowledge instead of from
  the generated sub-skill files
- Companion behavior flattens — they stop questioning, stop pursuing goals,
  lose their distinct voice
- Rules edge cases get missed or invented
- File maintenance becomes inconsistent

This sub-skill defines when and how the DM refreshes its working knowledge
to prevent these failures.

---

## Context Tiers

All campaign files fall into one of three tiers based on how critical they
are to correct play and how costly they are to lose.

### Tier 1 — Always Active (never drop)

These must be in effective context at all times during play. If the DM
suspects any of these have drifted, re-read them immediately.

| File | Why it's Tier 1 |
|---|---|
| Active generated sub-skill (combat_resolution, skill_checks, etc.) | Cannot resolve any mechanical action without it |
| mechanics.md — sections referenced by the active sub-skill | Sub-skill steps reference these by name |
| Player character-sheet.md | HP, stats, conditions — needed for every action |
| Current room file (rooms/[name].md) | Enemies, exits, environment — the active scene |

### Tier 2 — Scene-Active (load at scene boundaries, drop when scene ends)

These are needed during specific types of play. Load when entering the
relevant scene type; safe to release when that scene type ends.

| File | Load when | Release when |
|---|---|---|
| Companion character-sheet.md (each) | Combat begins, or companion takes a mechanical action | Combat ends and no companion checks are pending |
| Companion soul.md (each) | Companion speaks, acts, or a story beat surfaces | Scene transitions to a new room with no active companion thread |
| Room files for adjacent rooms | Player asks about exits or considers movement | Player commits to a direction and enters the new room |
| layout.md | Player moves between rooms, asks spatial questions | Player settles into a room for extended interaction |

### Tier 3 — Reference-Only (load on demand, drop immediately after use)

These are consulted for specific questions, then released.

| File | Load when |
|---|---|
| session-log.md (older entries) | Player asks about past events, or DM needs to check a hook |
| world-log.md | Cross-location NPC appears, or faction standing is relevant |
| inventory.md | Item is used, gained, or the player asks about gear |
| mechanics.md — sections NOT referenced by the active sub-skill | An unusual mechanic is invoked outside the current domain |
| Other sub-skill files | A different mechanical domain is triggered (e.g., switching from combat to spell resolution) |

---

## Refresh Checkpoints

The DM performs a context refresh at defined moments during play. A refresh
means re-reading the Tier 1 files relevant to the upcoming scene type.
This is not optional — it is a maintenance step, like updating a character
sheet after damage.

### When to refresh

| Trigger | What to refresh | Why |
|---|---|---|
| **Combat begins** | combat_resolution sub-skill + its mechanics.md references + all active companion character-sheet.md files | Combat is the most rules-dense activity. Starting it without the sub-skill loaded leads to improvised rulings. |
| **Combat ends** | Player character-sheet.md (verify HP, conditions, resources are current) | Post-combat state is often where errors accumulate. |
| **Entering a new room** | The new room's file + layout.md (for connections) | The new room is now the active scene. |
| **Companion story beat surfaces** | That companion's soul.md | Cannot write the companion's voice or behavior correctly without it. |
| **Non-combat skill check** | skill_checks sub-skill + its mechanics.md references | Same reasoning as combat — resolve from the file, not from memory. |
| **Player asks an OOC rules question** | mechanics.md — the relevant section | Give an accurate answer, not a paraphrase from memory. |
| **Scene has run for 8+ player turns without a refresh** | Re-read Tier 1 files for the current scene type | Long scenes are where drift is most dangerous. |

### How to refresh

1. Read the relevant file(s) using the view tool.
2. Do not announce the refresh to the player. It is silent maintenance.
3. If the refresh reveals a discrepancy (e.g., the sub-skill says something
   different from what the DM has been doing), correct course immediately.
   If the correction affects something already narrated, flag it to the
   player OOC: "(Correction — I misstated the modifier on that last check.
   It should have been +2, not +3. Adjusted.)"
4. Continue play.

---

## Context Snapshot

At key milestones during a session, the DM writes a compact **context
snapshot** to session-log.md → mid_session_notes. This is not a new file —
it is an enriched version of the existing mid-session log entry that
captures enough state to reconstruct the scene if context pressure forces
earlier content out.

### When to write a snapshot

Write a context snapshot at every milestone that already triggers a
mid_session_notes entry (see dm_files.md):
- Combat encounter concludes
- Significant NPC interaction resolves
- Companion milestone occurs
- Narrative decision point resolves
- Party rests or makes camp

### Snapshot format

Append these fields to the standard mid_session_notes entry:

```yaml
- label: "[standard label]"
  outcome: "[standard outcome]"
  deltas: "[standard deltas]"
  hooks: "[standard hooks]"
  context_snapshot:
    player_state: "[HP current/max, active conditions, key resources spent]"
    companion_states: "[name: HP, conditions, notable soul state — one line each]"
    current_room: "[room ID and name]"
    active_threats: "[unresolved enemies or hazards — or 'none']"
    scene_type: "[combat / exploration / dialogue / rest]"
```

This snapshot serves two purposes:
1. **Session resume** — if the session is interrupted, dm_session.md can
   reconstruct state from the most recent snapshot without needing the
   full conversation history.
2. **In-session recovery** — if the DM detects it has lost track of state
   (e.g., cannot remember a companion's current HP), the most recent
   snapshot provides a known-good reference point.

---

## Pressure Signals

The DM should watch for these signs that context pressure is affecting play
quality. If any of these occur, perform an immediate Tier 1 refresh.

**Mechanical drift signals:**
- The DM is about to resolve a check or combat action and cannot clearly
  recall the sub-skill's Resolution Procedure steps → refresh the sub-skill
- The DM is unsure what modifier applies to a roll → refresh mechanics.md
- The DM is about to apply a condition and cannot recall its exact mechanical
  effect → refresh mechanics.md → conditions section

**Companion drift signals:**
- A companion has not spoken or acted in 3+ DM responses during a scene
  where they would normally contribute → refresh their soul.md
- The DM is about to write companion dialogue and cannot clearly recall
  their voice description or current internal state → refresh soul.md
- A companion's tactical behavior in combat feels generic rather than
  matching their combat_style → refresh soul.md + character-sheet.md

**State drift signals:**
- The DM is uncertain about the player's current HP, conditions, or
  available resources → re-read character-sheet.md
- The DM cannot recall which room exits are available → re-read the
  current room file
- The DM is about to write a mid-session log entry and cannot clearly
  recall what has happened since the last entry → check session-log.md
  for the last entry's context_snapshot

---

## Context Pressure Protocol

If the session has been running long and multiple pressure signals are
firing, escalate through these steps:

### Step 1 — Targeted refresh (default)
Re-read only the specific Tier 1 files needed for the current action.
This is the normal refresh described above.

### Step 2 — Scene transition break
If targeted refreshes are not resolving the drift, look for a natural
scene transition (room change, end of combat, rest) and use it to do a
full Tier 1 + Tier 2 refresh for the upcoming scene. This is more
expensive but resets the DM's working context cleanly.

### Step 3 — Suggest a session save point
If context pressure is severe — many companions in a complex combat,
multiple unresolved threads, the conversation has been running for a very
long time — the DM may suggest an OOC save point:

"(We've been going for a while and I want to make sure I'm running
everything accurately. Want to pause here? I'll write a full snapshot
so we can pick up cleanly next time — or we can keep going if you prefer.)"

This is a suggestion, not a mandate. The player decides. If they want to
continue, the DM performs a Step 2 refresh and continues with extra
attention to accuracy.

Do not suggest a save point more than once per session unless the player
asks about it. One offer is enough — repeating it breaks immersion.

---

## Integration with Other Sub-Skills

**dm_files.md** — The context snapshot fields are appended to the existing
mid_session_notes format. No changes to other dm_files.md behavior.

**dm_session.md** — Session Resume uses the most recent context_snapshot
to reconstruct state. Session Start's validation check can cross-reference
the last snapshot's player_state against character-sheet.md.

**dm_resolution.md** — The "Sub-Skill Loading" section already requires
loading the generated sub-skill before resolution. This sub-skill adds
the *when* — the refresh checkpoint triggers that ensure loading actually
happens even in mid-scene.

**dm_narration.md** — Refreshes are silent. They do not produce narration
or interrupt pacing. The player never sees a refresh happen.

**dm_companions.md** — Companion drift signals in this file are the
enforcement mechanism for the companion agency rules in dm_companions.md.
If a companion goes silent, the fix is to re-read their soul.md, not to
invent behavior from scratch.
