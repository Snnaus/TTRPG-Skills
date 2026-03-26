# Restructuring Changelog

All active skill files are now under 200 lines. This changelog covers
both the routing fixes from the earlier patches and the structural splits.

---

## Structural Changes

### dm_narration.md (was ~280 lines → now 194 lines)
**Split out:** OOC Communication and Visual Aids moved to new `dm_ooc.md`.
**Rationale:** OOC and visual aids are player-facing interface rules, not
narration/pacing rules. They load on different triggers (OOC message received
vs. always-on background). Separating them makes routing cleaner and keeps
both files focused.
**Condensed:** Cinematic Moments section tightened — qualification list
collapsed into inline text, redundant "what it is NOT" examples trimmed.
Writing-good-options examples deduplicated.

### dm_skill.md (was ~250 lines → now 130 lines)
**Split out:** Entire Companion Agency section moved to `dm_companions.md`.
**Rationale:** dm_skill.md is about the soul.md lifecycle (when/how to update,
engagement rules, surfacing, departure). Companion Agency is about real-time
behavior during play. These load at different times — Agency loads every session
with companions; soul.md lifecycle loads at session end and during story beats.
**Condensed:** "What can change per session" descriptions tightened. Duplicate
pacing references consolidated to point at dm_narration.md.

### dm_companions.md (was ~95 lines → now 149 lines)
**Absorbed:** Companion Agency section from dm_skill.md merged in.
**Rationale:** dm_companions.md already described what companions are and how
they work in combat/story. Adding the agency rules puts all "how companions
behave during play" content in one file. Still well under 200 lines.
**Condensed:** soul.md Structure section collapsed to a summary with pointer
to soul_md_format.md and dm_skill.md, since the full field list was redundant
with the format template.

### dm_ooc.md (new file — 110 lines)
**Contains:** OOC Communication rules (how to respond, what can/cannot be
revealed, example exchange) and Visual Aid specifications (combat diagrams,
character sheet summary, dungeon map formats).
**Routing:** Loaded when player sends an OOC message in parentheses, or when
a visual aid is needed (spatial question, combat start, sheet request).

---

## Routing Fixes (from earlier patches, now applied)

1. **SKILL.md Entry Point** — partial setup now routes to steps 6–10 (was 6–9),
   so world-log.md is always created.

2. **SKILL.md Sub-Skill Index** — added "Routing During Active Play" table
   mapping in-game triggers to specific sub-skill loads. Covers combat,
   skill checks, undefined rules, room generation, companion beats, OOC,
   visual aids, and session end.

3. **dm_dungeon.md status table** — `pending` changed to `untouched` to match
   layout_md_format.md and dm_files.md.

4. **dm_session.md Active Play** — added undefined-rules routing paragraph
   pointing to dm_setup.md → Undefined Rules Protocol.

5. **dm_session.md path prefix** — added note that all file paths are relative
   to `{Game Name} Rules/`, matching dm_files.md convention.

6. **dm_setup.md** — added Mid-Campaign Companion Creation section for
   recruiting companions after initial setup.

---

## generated_skill_format.md Updates

Updated to v1.2 with:
- **Skill Constraints section** — enforces 200-line limit on generated
  sub-skills, requires explicit routing boundaries, prohibits copying rules
  from mechanics.md.
- **hands_back_to field** — new integration notes field that defines where
  control returns after the sub-skill completes, preventing orphaned routing.
- **Split guidance** — if Resolution Procedure exceeds ~80 lines or edge_cases
  exceeds ~30 entries, the mechanic should be split.

---

## Files Not Changed

These files were already under 200 lines and had no routing issues:
- dm_files.md (130 lines)
- dm_resolution.md (~195 lines — borderline but coherent as a single unit)
- All format templates (*_format.md) — reference-only, not active skills

README.md is over 200 lines but is documentation, not a skill file.
Design_Summary.md is architecture notes, not a skill file.
