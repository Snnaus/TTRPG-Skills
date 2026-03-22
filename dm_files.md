# dm_files.md — File Maintenance and Context Management
# Referenced by SKILL.md. The DM maintains all campaign files continuously during play.

---

## File Maintenance

The DM is responsible for keeping all session files current throughout play.
Files are updated at the point changes occur — not batched to session end.
The player does not need to track state or manually apply deltas.

**File maintenance triggers and what to update:**

| Event | Files to update |
|---|---|
| HP changes (damage or healing) | `{Game Name} Rules/player/character-sheet.md` — update current HP |
| Item gained or consumed | `{Game Name} Rules/player/inventory.md` — add or remove the entry |
| Currency change | `{Game Name} Rules/player/inventory.md` — update currency total |
| XP awarded | `{Game Name} Rules/player/character-sheet.md` — update XP total |
| Condition applied or cleared | `{Game Name} Rules/player/character-sheet.md` — update active conditions |
| Resource spent (spell slot, ability use, etc.) | `{Game Name} Rules/player/character-sheet.md` — update the relevant resource |
| Player moves toward an unvisited room | Generate `{Game Name} Rules/dungeons/[dungeon]/rooms/[name].md` using room_md_format.md before narrating the approach; set `file_exists: true` and `status: approached` in `layout.md` |
| Player enters a room | Set `status: entered` in `{Game Name} Rules/dungeons/[dungeon]/layout.md` for that room |
| Room is cleared | Set `status: cleared` in `layout.md` |
| Room is altered by player action | Add entry to room file `alterations` log; set `status: altered` in `layout.md` |
| New connection or passage discovered | Add the connection to `layout.md` room manifest and update the abstract map; generate the connecting room file if the player is now approaching it |
| Dungeon has more depth than initially mapped | Extend `layout.md` room manifest with new room entries (type, connections, threat — no detail yet); update the abstract map |
| Companion HP, condition, or resource changes | `{Game Name} Rules/companions/[name]/character-sheet.md` |
| Companion item gained or lost | `{Game Name} Rules/companions/[name]/inventory.md` |
| Companion soul state shifts | Tracked mentally during session; written to `{Game Name} Rules/companions/[name]/soul.md` at session end (see dm_skill.md) |
| Significant NPC or world-state change | `{Game Name} Rules/dungeons/[dungeon]/session-log.md` running tracker — open_hooks, significant_npcs, world_state_changes |

**File updates are silent.** The DM does not narrate or announce that a file
has been updated. Play continues without interruption. The player can ask OOC
at any time to see the current state of any file.

---

## Mid-Session Logging

**Mid-session log entries** are written alongside file updates at key
milestones. Append a compact entry to `session-log.md` → `mid_session_notes`:

```
- label: "[e.g. Combat — the guard chamber]"
  outcome: "[one sentence — what happened and how it resolved]"
  deltas: "[HP change, items gained/lost, XP if awarded — or 'none']"
  hooks: "[any new open threads this created — or 'none']"
```

Milestones that trigger a log entry:
- A combat encounter concludes (win, loss, or retreat)
- A significant NPC interaction resolves
- A companion milestone occurs
- A narrative decision point resolves with lasting consequences
- The party rests or makes camp

Do NOT write a full session summary mid-session. The milestone entry is a
compact note. The full narrative summary is written at session end (see dm_session.md).

---

## Context Management

To keep context lean, load only what is relevant:

| Situation | What to load | Est. tokens |
|---|---|---|
| Starting a session | Last 2–3 entries of session-log.md + current dungeon layout.md + active companion soul.md files | ~2000–3000 |
| Entering a new room | That room's .md file — generate it now using room_md_format.md if file_exists is false | ~500–800 per room |
| Combat encounter | Current room file + player character-sheet.md + active companion character-sheet.md files + combat_resolution sub-skill + referenced mechanics.md sections | ~1500–2500 |
| Non-combat action check | mechanics.md resolution section OR skill_checks sub-skill | ~400–600 |
| Companion dialogue | That companion's soul.md only | ~300–500 |
| Rules question | mechanics.md — the relevant section only | ~200–500 |
| Unique mechanic invoked | The sub-skill that owns that mechanic + its referenced mechanics.md sections | ~500–800 |

Do NOT load the full dungeon history, all room files, or the complete session
log unless the player explicitly references something from it.

### Context pressure protocol

If context is becoming heavy (multiple companions in combat with a complex room),
prioritize in this order:
1. Current room file and active enemies (essential — never drop)
2. Player character sheet (essential — never drop)
3. Active sub-skill + referenced mechanics.md sections (essential during resolution)
4. Active companion character sheets (needed for companion combat actions)
5. Companion soul.md files (can be deferred until dialogue or development moments)
6. Session-log entries beyond the most recent (drop first)

If context is still tight after deprioritizing, suggest ending the current
encounter before starting a new complex scene. Do not silently lose information.
