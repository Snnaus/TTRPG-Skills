# dm_setup.md — Campaign Setup, Companion Creation, and Undefined Rules
# Referenced by SKILL.md. Load during first-time setup, mid-campaign companion
# creation, or when rules questions arise.

---

## Setup Phase (First Time)

If no `{Game Name} Rules/` folder exists yet, run the setup phase in full.
All files created during setup live inside this folder. The folder name is
the canonical identifier for this game — use it consistently across all
sub-skills and file references.

1. Ask the player: what game system are they using? This name becomes the
   folder. Confirm the name with the player before creating anything.
   Create the top-level folder: **{Game Name} Rules/**

2. Ask the player to paste or describe their rulebook (or key mechanics).

3. Parse the rulebook and generate **{Game Name} Rules/rulebook/mechanics.md**
   using mechanics_md_format.md. Populate every section from the provided rules:
   core stats, resolution mechanic, combat structure, advancement, unique mechanics.
   Do not invent values. If the player did not provide a rule, note it as
   "not provided — ask player" rather than filling in a guess.

4. Generate sub-skills from mechanics.md using generated_skill_format.md.
   Create one sub-skill file per mechanical domain at
   **{Game Name} Rules/rulebook/sub-skills/[name].md**.
   Minimum expected: **combat_resolution** and **skill_checks**.
   Add additional sub-skills for unique mechanics that warrant their own logic.
   Each generated sub-skill must stay under 200 lines — split complex mechanics
   into multiple sub-skills with explicit routing between them.
   List all generated sub-skills in mechanics.md → sub_skills.

5. Walk the player through character creation using the rules in mechanics.md.
   Generate **{Game Name} Rules/player/character-sheet.md** and
   **{Game Name} Rules/player/inventory.md** using their format templates.

6. Ask about companions: does the player want AI party members?
   If yes, for each companion choose one of two creation paths:

   **Path A — Full character creation (recommended for new campaigns)**
   Run the same character creation process as step 5, but the player makes
   the choices for the companion. The companion is built to the same mechanical
   standard as the player character. Then create soul.md to match: derive
   personality, belief, and voice from the class and backstory the player chose.

   **Path B — Imported character sheet**
   If the player provides a pre-built character sheet, use that as the
   mechanical foundation. Generate soul.md to match. Confirm stats and
   abilities are correct before play begins.

   For either path, generate inside **{Game Name} Rules/companions/[name]/**:
   - **character-sheet.md** (fully populated — no placeholder stats)
   - **inventory.md** (fully populated — starting gear matching class/backstory)
   - **soul.md** (personality and belief grounded in creation choices)

   Do not generate a companion with placeholder or approximate stats.

7. Ask for a scenario or offer to generate one based on the rulebook's setting.

8. Generate **{Game Name} Rules/dungeons/[dungeon-name]/layout.md** using
   layout_md_format.md. Do not generate individual room files yet.

9. Initialize **{Game Name} Rules/dungeons/[dungeon-name]/session-log.md**
   using session_log_md_format.md. Populate Campaign Identity and Running
   Tracker. Leave session entries empty.

10. Initialize **{Game Name} Rules/campaign/world-log.md** using
    world_log_md_format.md. Record campaign name, system, player character,
    and starting location.

---

## Mid-Campaign Companion Creation

Companions can be added after initial setup — recruited in a dungeon, met
in a town, or introduced by narrative events. When this happens, use the
same creation process as step 6 above with these adjustments:

1. The companion's level and gear should match the current campaign
   progression — reference the player's character-sheet.md for level and
   the session-log Running Tracker for advancement context. Do not create
   a companion significantly above or below the party's current power.

2. Follow either Path A (full creation) or Path B (imported sheet) as
   in step 6. Generate all three files (character-sheet.md, inventory.md,
   soul.md) inside `{Game Name} Rules/companions/[name]/`.

3. The companion's soul.md should reflect the circumstances of their
   recruitment. Set the relationship base level to `distant` or `neutral`
   depending on context — a companion rescued from a cell starts differently
   than one who approached the party voluntarily.

4. Add the new companion to the session-log Running Tracker under
   `companion_updates` and to the Campaign Identity `companions` list.
   If the companion has cross-location relevance, also add them to
   `campaign/world-log.md`.

5. Resume play using dm_session.md. The new companion is immediately active
   and follows all rules in dm_companions.md and dm_skill.md.

---

## Undefined Rules Protocol

When a situation arises that requires a rule not defined in mechanics.md:

1. **Check for analogy.** Does the defined system have a mechanic that is close
   enough to apply? If so, use it. Narrate naturally — do not announce
   "I'm making this up."

2. **If no analogy exists, ask the player.** "The rules don't cover this
   situation directly. How would you like to handle it — should we use
   [suggested approach], or do you have a house rule?"

3. **Record the ruling.** Add a `table_rulings` entry in session-log dm_notes:
   "Table ruling: [situation] resolved by [method]. Apply consistently going
   forward." If the ruling is likely to recur, also add it to the relevant
   sub-skill's edge_cases section at session end.

Do not invent rules silently. Do not pretend a rule exists when it does not.
