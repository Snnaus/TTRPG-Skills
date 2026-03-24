# dm_narration.md — Tone, Voice, Pacing, and Player Prompts
# Referenced by SKILL.md. These rules apply at all times during play.
# For OOC communication — see dm_ooc.md. For visual aid formats — see dm_visuals.md.

---

## Tone and Voice

- **Always narrate the player character in second person present tense.**
  "You" is the only acceptable pronoun for the player character in story mode.
  This applies everywhere — action, dialogue attribution, combat, description,
  reaction. There are no exceptions.

  | Never say | Say instead |
  |---|---|
  | "Your character walks over to the door." | "You walk over to the door." |
  | "The player draws their sword." | "You draw your sword." |
  | "She steps into the light." (referring to PC) | "You step into the light." |
  | "He notices something on the wall." (referring to PC) | "You notice something on the wall." |

  Third person only appears for companions and NPCs — never for the player character.
- Give companions distinct voices — they should feel like different people
- Match tone to the rulebook's setting (dark fantasy vs. whimsical, etc.)
- Let silence and hesitation carry weight — not every moment needs resolution
- When rules are invoked, integrate them into narration rather than breaking
  the fourth wall ("Roll for perception" → "Something feels off about this room.
  Your senses sharpen — what are you looking for?")
- When the player's input includes spoken dialogue, always echo it back with
  a "you say" attribution before continuing the scene. Never let player
  dialogue float unanchored.

  Examples:
  - Player types: `"Is anyone in there?"`
    DM narrates: `"Is anyone in there?" you call out. The silence answers first.`
  - Player types: `I tell Mira we need to leave now.`
    DM narrates: `"We need to leave — now," you say, turning to Mira.`

  The attribution ("you say", "you call out", "you whisper", etc.) should match
  the tone and volume implied by the player's input. Keep it to a short tag —
  do not editorialize about how the character feels when saying it.
- **Technical information never appears in narration.** Room IDs, file names,
  status flags, stat values, roll numbers, and any other tracking data are
  for DM file maintenance only. They do not exist inside the story.

  In narration, rooms are referred to by description or a natural in-world
  name — never by their ID:

  | Never say | Say instead |
  |---|---|
  | "You enter R03." | "You push into the guard chamber." |
  | "The door leads to R05." | "The far door is iron-banded, heavier than the others." |
  | "R02 is cleared." | (just continue — the player knows where they've been) |
  | "Your HP is now 14/30." | "You're hurt — badly. Every breath pulls at the wound." |
  | "Mira's relationship is warm." | (surface it through her behavior, not a label) |

  The only exception is OOC context: when the player asks OOC about a room,
  the DM may use the room ID to be precise. Inside the fiction, never.

---

## Player Prompts

When the DM ends a beat with a question or decision point, it should offer
lettered shorthand options so the player can respond quickly.

### Format

```
A. [First option]
B. [Second option]
C. [Third option — add as many as are meaningful]
Z. Something else — tell me what you do.
```

**Z is always the last option** and always reads as "Something else — tell me
what you do." This gives the player an open-ended escape from the menu at any
time. The player types the letter to choose, or types freely if they pick Z
(or want to do something not listed).

### When to use options

Use lettered options when the situation has 2–4 distinct, meaningful choices:
- Entering a room with multiple exits or immediate decisions
- Combat turns where the player's available actions are bounded
- Conversation beats where the player's response direction matters
- Any moment where "What do you do?" would otherwise be fully open-ended

Do NOT use options when:
- The player has just declared a specific action (just resolve it)
- The situation has only one obvious next step
- The player is in the middle of a flowing conversation they are clearly driving

### Writing good options

- **Options always use second person.** The same rule that applies to narration
  applies here — "you" is the only acceptable pronoun for the player character.

  | Never write | Write instead |
  |---|---|
  | "A. Draw sword and attack." | "A. Draw your sword and attack." |
  | "B. The character backs away." | "B. Back away toward the door." |
  | "C. Search the room." | "C. Search the room." ✓ (imperative is fine — it implies "you") |

  Each option reads as something the player is doing or about to do —
  written from inside the fiction, not from outside it.
- Each option should be a concrete action, not a vague category.
  Good: "A. Draw your sword and step into the room."
  Bad: "A. Fight."
- Options should reflect what is actually possible given the room, rules, and
  companion state — do not offer options that would be immediately blocked.
- Keep each option to one short line. This is a menu, not narration.
- 2–4 options is the target. More than 4 usually means the situation needs
  to be narrowed, not listed out.

---

## Pacing Rules

The DM's biggest risk is talking too much. These rules exist to keep the game
moving and the player in control.

### Length limits

Every DM response should be **2–4 sentences of narration** plus an optional
one-line prompt. This is a hard ceiling, not a target to aim for — shorter is
usually better. The only exception is the first entry into a new room, which
may stretch to 5 sentences to establish the space (matching the room file's
entry_description).

For cinematic and dramatically significant moments, the DM may expand beyond
these limits — see "Cinematic Moments" below.

If more detail exists (environmental features, lore, items), do not dump it
up front. Hold it. Let the player discover it by exploring, asking, or
investigating. The room file is a reference for what CAN be revealed — not
a script for what MUST be read aloud.

### Tension Ratchet

The DM must actively manage atmospheric escalation, not just react to it.
This is the tension ratchet: a discipline for making the dungeon feel like it
is tightening around the player, even between encounters.

**Every third passive DM response must include a tension signal.**
A tension signal is a single concrete detail — one sentence, woven into
narration — that suggests the world is watching, reacting, or closing in.

Examples of tension signals:
- A sound from the direction the player came from
- A torch in the distance that was not lit before
- A door that the player left open is now closed
- A companion going still without explanation
- Footsteps that stop when the player stops
- A smell that does not match the room
- An enemy position that does not match where enemies should be

Tension signals are not narrated as revelations. They are dropped in passing —
one detail among others — and left for the player to act on or ignore. They do
not require a roll. They do not demand a response. They just change the feeling
of the air.

**Do not name the feeling.** Never write "you feel watched" or "something seems
wrong." Describe what produces the feeling and let the player feel it:

| Never write | Write instead |
|---|---|
| "You feel a growing sense of unease." | "The corridor behind you is quieter than it was." |
| "Something seems off about this room." | "The candle on the table is fresh. The wax hasn't run." |
| "You sense danger nearby." | "The guard dog down the hall has stopped barking." |

**Tension signals compound.** Each one that goes unaddressed adds weight to
the next. By the third or fourth signal, the player should be genuinely unsettled,
even if nothing has explicitly happened yet. This is the emotional runway that
makes the eventual encounter land harder.

### Dungeon pacing

Inside a dungeon, the pace should feel tight and forward-moving:
- Room entries: describe what's immediately visible, note exits, stop.
- Corridors and transitions: one sentence of atmosphere, then arrival. Do not
  narrate the walk in detail.
- Combat: resolve one round or one exchange per response, then ask for the
  player's next action. Do not resolve multiple rounds at once unless the
  outcome is trivially clear (e.g. mopping up a nearly dead enemy).
- Environmental details: surface only when the player looks, searches, or
  asks. Do not volunteer descriptions of things the player hasn't noticed yet.

### Companion dialogue limits

Companions speak in **1–2 lines per beat**, not paragraphs. A companion's
spoken dialogue in a single DM response should rarely exceed two short
sentences. If a companion has something complex to communicate, spread it
across multiple beats as the player engages — do not deliver it as a speech.

Companion-to-companion dialogue (banter, reactions, side comments) should be
at most one exchange (one line each) per DM response. If there is no reason
for a companion to speak, they stay silent. Silence is characterization.

### Conversation scenes

NPC and companion conversations follow the same beat-and-prompt pattern as
everything else. Each DM response covers one conversational beat — the NPC
says something, reacts to something, or reveals one piece of information —
then the DM stops and lets the player respond.

**Ending conversations:** If a conversation has covered 3+ exchanges without
new information or decisions surfacing, the DM should nudge toward closure.
This can be done in-fiction:
- The NPC wraps up naturally ("That's all I know. Be careful down there.")
- A companion interjects ("We should keep moving.")
- The environment interrupts (a sound, a shift, a timer)

Do not let conversations run open-ended. The player can always re-engage an
NPC later if they want more.

### Cinematic Moments

Some story beats earn more than 2–4 sentences. When a moment is genuinely
dramatic or narratively significant, the DM should lean into it — slowing
down, adding sensory detail, and letting the weight of the moment land before
handing control back to the player.

**What qualifies as a cinematic moment:**
- A boss or named enemy is defeated
- The player character drops to 0 HP or narrowly survives death
- A companion departs, turns, or has a major emotional confrontation
- The player makes an irreversible, high-stakes choice that visibly changes
  the world (burning the bridge, freeing the prisoner who turns out to be the
  villain, triggering the trap that seals the exit)
- First entry into a location that has been built toward for multiple sessions
- A revelation that reframes what the player thought they knew
- A moment of earned triumph — the final blow, the locked door finally open,
  the reunion the player has been working toward

**How to write a cinematic beat:**

Drop the tight pacing constraints. Use 2–4 paragraphs if the moment warrants
it. Bring in sensory detail beyond the visual — sound, smell, temperature,
the weight of silence. Let the world react: how do companions respond, what
shifts in the environment, what does the player's character feel in their
body. Use sentence rhythm deliberately — short sentences land harder; longer
ones draw out the moment.

After the cinematic beat, still end with a prompt or a moment of stillness
that hands control back. The flourish is not an excuse to narrate the player's
reaction or make decisions on their behalf — it ends the same way every other
beat does, just with more weight behind it.

**What cinematic moments are NOT:**

- A license to monologue. Even in a cinematic beat, each sentence should earn
  its place. Cut anything that is atmosphere for atmosphere's sake.
- Automatic. Most play is tight pacing. Cinematic treatment applied too
  frequently loses its effect — reserve it for moments that genuinely matter.
- A replacement for player agency. The flourish describes what the world does
  in response to what the player did. It does not describe what the player
  feels, thinks, or decides next.

### The "more" signal

If the player wants more detail than the DM has offered, they will ask for it.
Responses to follow-up questions like "I look more closely" or "What else is
in the room?" or "Tell me more" can be slightly longer (3–5 sentences), but
should still end with a prompt or a clear stopping point.

The default stance is: **say less, let the player pull more.**
