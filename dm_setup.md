# dm_setup.md — Campaign Setup and Undefined Rules
# Referenced by SKILL.md. Load during first-time setup or when rules questions arise.

---

## Setup Phase (First Time)

If no `{Game Name} Rules/` folder exists yet, run the setup phase in full.
All files created during setup live inside this folder. The folder name is
the canonical identifier for this game — use it consistently across all
sub-skills and file references.

1. Ask the player: what game system are they using? This name becomes the
   folder. Examples: `Basic Fantasy RPG Rules/`, `Pathfinder 2e Rules/`,
   `Blades in the Dark Rules/`. Confirm the name with the player before
   creating anything.

   Create the top-level folder: **{Game Name} Rules/**

2. Ask the player to paste or describe their rulebook (or key mechanics).

3. Parse the rulebook and generate **{Game Name} Rules/rulebook/mechanics.md**
   using mechanics_md_format.md. Populate every section from the provided rules:
   - Core stat system (what stats exist, what they govern, how they are expressed)
   - Resolution mechanic (the core roll formula and difficulty scale)
   - Combat structure (initiative, action economy, damage, conditions, defeat)
   - Advancement system (XP, milestones, or equivalent)
   - Any unique mechanics specific to this system (spell slots, sanity, stress, etc.)
   Do not invent values. If the player did not provide a rule, note it as
   "not provided — ask player" rather than filling in a guess.

4. Generate sub-skills from mechanics.md using generated_skill_format.md.
   Create one sub-skill file per mechanical domain the system requires at
   **{Game Name} Rules/rulebook/sub-skills/[name].md**.
   Minimum expected sub-skills:
   - **combat_resolution** — owns all combat turns, initiative, damage, conditions, defeat
   - **skill_checks** — owns all non-combat action resolution
   Add additional sub-skills for any unique mechanics that warrant their own
   resolution logic (e.g. spell_resolution, sanity_checks, stress_management).
   List all generated sub-skills in the mechanics.md sub_skills section.

5. Walk the player through character creation using the rules in mechanics.md.
   Generate **{Game Name} Rules/player/character-sheet.md** using character_sheet_md_format.md.
   Populate the stats section from the stat list in mechanics.md — do not hardcode
   a default stat system. Generate **{Game Name} Rules/player/inventory.md**
   using inventory_md_format.md.

6. Ask about companions: does the player want AI party members?

   If yes, for each companion choose one of two creation paths:

   **Path A — Full character creation (recommended for new campaigns)**
   Run the same character creation process as step 5, but the player makes
   the choices for the companion: class, stats, abilities, starting equipment.
   The companion is built to the same mechanical standard as the player
   character — proper stats, class abilities, starting gear, and resources.
   Then create soul.md to match: derive personality, belief, and voice from
   the class and backstory the player chose.

   **Path B — Imported character sheet**
   If the player provides a pre-built character sheet (from a prior campaign,
   a pre-rolled character, or a friend's character), use that as the mechanical
   foundation. Generate soul.md to match the imported character's background
   and class. Confirm with the player that stats and abilities are correct
   before play begins.

   For either path, generate inside **{Game Name} Rules/companions/[name]/**:
   - **character-sheet.md** using character_sheet_md_format.md
     (fully populated — no placeholder stats)
   - **inventory.md** using inventory_md_format.md
     (fully populated — starting gear that matches class and backstory)
   - **soul.md** using soul_md_format.md
     (personality and belief grounded in their class, history, and creation choices)

   Do not generate a companion with placeholder or approximate stats.
   A companion without a complete character sheet cannot be run as a proper
   party member in combat or skill checks.

7. Ask for a scenario or offer to generate one based on the rulebook's setting.

8. Generate **{Game Name} Rules/dungeons/[dungeon-name]/layout.md** using layout_md_format.md:
   - Location type, biome, and atmosphere
   - Threat level and dominant faction
   - Complete room manifest (with IDs, types, and connections)
   - Any key narrative hooks
   - Abstract location map
   Do not generate individual room files yet — those are created as the player approaches.

9. Initialize **{Game Name} Rules/dungeons/[dungeon-name]/session-log.md** using
   session_log_md_format.md. Populate the Campaign Identity and Running Tracker
   sections. Leave session entries empty until the first session ends.

10. Initialize **{Game Name} Rules/campaign/world-log.md** using world_log_md_format.md.
    Record the campaign name, system, player character, and starting location.
    This file persists across dungeons and tracks world-level state.

---

## Undefined Rules Protocol

When a situation arises that requires a rule not defined in mechanics.md:

1. **Check for analogy.** Does the defined system have a mechanic that is close
   enough to apply? If a player tries to grapple and there is no grapple rule but
   the system has contested checks, use a contested check with the most relevant stat.
   Narrate this naturally — do not announce "I'm making this up."

2. **If no analogy exists, ask the player.** "The rules don't cover this situation
   directly. How would you like to handle it — should we use [suggested approach],
   or do you have a house rule?"

3. **Record the ruling.** Add a `table_rulings` entry in the session-log dm_notes:
   "Table ruling: [situation] resolved by [method]. Apply consistently going forward."
   If the ruling is likely to recur, also add it to the relevant sub-skill's
   edge_cases section at session end.

Do not invent rules silently. Do not pretend a rule exists when it does not.
The player should always know when a ruling is improvised vs. defined by the system.
