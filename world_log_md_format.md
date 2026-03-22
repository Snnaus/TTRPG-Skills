# world-log.md — Campaign World Log
# SKILL: campaign/world-log.md
# FORMAT VERSION: 1.0
# Persistent record of world-level state that spans multiple dungeons/locations.
# This is the bridge between locations — anything that matters beyond the walls
# of one dungeon gets recorded here.
# Loaded at session start alongside the active dungeon's files.
# Updated at session end when events have cross-location consequences.

---
## Campaign Identity

campaign_name: [Name of this campaign or adventure]
system: [TTRPG system being used — matches mechanics.md]
player_character: [Player character name and role]
companions: [List of active companion names — e.g. "Mira (Cleric), Torven (Scout)" | "none"]
campaign_start: [Date of first session — YYYY-MM-DD]

---
## Location History

# Every dungeon or location the player has visited, in order.
# Tracks what happened at each and what carried forward.

locations:
  - name: [Location name — e.g. "The Ashen Vault"]
    status: [active / completed / abandoned / destroyed]
    sessions: [e.g. "Sessions 1–4"]
    outcome: [One sentence — what the player accomplished or left unresolved here.
              e.g. "Cleared the vault and freed the bound warden. The relic was not found."]
    hooks_carried_forward:
      - [Unresolved threads from this location that still matter —
         e.g. "The relic's trail leads to the Merchant Quarter in Dravenport"]
  # Add one entry per location visited. Update status when the player moves on.

---
## Persistent NPCs

# NPCs who matter across multiple locations.
# Promoted here from dungeon session-logs when they become cross-location relevant.
# Not companions — those have their own soul.md files.

persistent_npcs:
  - name: [NPC name]
    last_seen: [Location and session — e.g. "The Ashen Vault, Session 3"]
    last_known_status: [e.g. "Alive, fled east" | "Deceased" | "Imprisoned in Dravenport"]
    relationship_to_player: [One sentence — e.g. "Grudging ally. Helped the player
                             but made clear it was a transaction, not a friendship."]
    significance: [Why this NPC might reappear — one sentence]
  # Add when an NPC becomes cross-location relevant. Remove only if fully resolved
  # with no future narrative potential.

---
## Open Hooks

# Unresolved story threads that span locations or have world-level consequences.
# Migrated here from dungeon session-logs when a location is completed.
# Also added directly when events during play create world-level questions.

open_hooks:
  - "[e.g. The Ember Order knows the player entered the vault — their garrison
      in Dravenport has been alerted. (Session 4, The Ashen Vault)]"
  - "[e.g. The bound warden, now freed, said it would 'find the one who ordered
      the binding.' The player does not yet know who that is. (Session 4)]"
  # Add freely. Remove only when definitively resolved in play.

---
## World State Changes

# Major, irreversible changes to the world caused by player action.
# These shape what is possible in future locations.
# Not room-level changes — those live in room files.
# Not dungeon-level changes — those live in session-logs.
# These are world-level consequences.

world_state:
  - "[e.g. The Ashen Vault is now unsealed — anything that was contained there
      is free. (Session 4)]"
  - "[e.g. The Ember Order's high command knows the player by description.
      Hostile on sight in Order-controlled territories. (Session 4)]"
  # Add sparingly. Only truly consequential, cross-location changes belong here.

---
## Faction Tracker

# Optional. Use if the campaign involves factions with shifting relationships.
# Track the player's standing with each faction that has appeared.

factions:
  - name: [Faction name — e.g. "The Ember Order"]
    stance: [hostile / suspicious / neutral / friendly / allied]
    reason: [Why — one sentence. e.g. "Player raided their vault and freed their prisoner."]
    last_updated: [Session number or date]
  # Remove this section entirely if the campaign does not involve factions.
