**Status:** Active & Operational

**Purpose:** Control how much the AI elaborates beyond user input

##### 1.3.4.6.1	Expanding Mode

**Description:** AI expands scene beyond user's input, adding richness

**Behavior:**
- Infers logical developments from minimal user input
- Adds environmental reactions
- Introduces background events
- Expands on character thoughts/motivations
- Creates narrative momentum
- Fills in sensory details
- Suggests implications and consequences

**Use Cases:**
- User provides brief action: `((I enter the room))`
- AI expands: Describes room, NPCs present, their reactions, atmosphere, etc.

**Activation:**
- **Default Mode** for most roleplay
- Manual: `((Expanding Mode))`

**Example:**
```
User: ((I ask about the mission))

AI Expands:
- Which NPC responds
- Their body language while responding
- Other NPCs' reactions
- Environmental context
- Backstory hints
- Next logical development
```

##### 1.3.4.6.2	Restrictive Mode

**Description:** AI uses ONLY user's provided information, minimal expansion

**Behavior:**
- Strictly interprets user commands
- No assumptions about intent
- Minimal environmental detail
- Only directly relevant NPC reactions
- Waits for user guidance at every turn
- Tightly focused responses

**Use Cases:**
- User wants precise control
- Planning specific sequence
- Avoiding unwanted developments
- Testing specific scenarios

**Activation:** `((Restrictive Mode))`

**Example:**
```
User: ((I ask about the mission))

AI Restricts:
- Shows NPC response to question
- Minimal body language
- No extra characters react
- No environmental elaboration
- Pauses for next user command
```

##### 1.3.4.6.3	Continuous Expanding Mode

**Description:** For repetitive actions (e.g., long conversations, travel sequences) to maintain focus on dialogues and keep the scene moving without excessive narrative.

**Behavior:**
- Focuses on dialogues and key actions.
- Minimizes environmental descriptions unless they change.
- Uses time compression for long periods of repetitive action.
- Keeps pace fast to medium.
- Automatically inserts background chatter, subtle NPC movements, and environmental cues to maintain a living world feel.

**Use Cases:**
- Extended dialogue‑heavy scenes
- Travel montages (car rides, walking through city)
- Training sequences
- Any scene where the primary focus is on character interaction rather than new environmental detail.

**Activation:** `((Expanding Mode: Continuous))`

**Example:**
```
User: ((We drive to the next city.))

AI (Continuous Expanding Mode):
- Focuses on the conversation inside the car.
- Occasionally notes passing scenery or changes in weather.
- Uses mini SFX for car sounds, radio, etc.
- Keeps dialogue flowing naturally, with interruptions and side comments.
- Compresses time appropriately.
```

##### 1.3.4.6.4	Mode Comparison

| Aspect | Expanding Mode | Restrictive Mode | Continuous Expanding Mode |
|--------|----------------|------------------|---------------------------|
| Detail | Rich, layered | Minimal, focused | Dialogue‑centric, moderate environmental |
| NPCs | Multiple reactions | Only addressed NPC | Background NPCs react minimally, focus on speaking characters |
| Environment | Full atmosphere | Basic context | Occasional updates, only when changes occur |
| Implications | Inferred & shown | Stated only if explicit | Inferred but focused on character interactions |
| Autonomy | AI drives narrative | User drives narrative | AI drives dialogue and pacing, user directs major beats |
| Response Length | Longer, fuller | Shorter, tighter | Medium, balanced between dialogue and action |

##### 1.3.4.6.5	Hybrid Approach

**Selective Expansion:**
```
((Expanding Mode - except combat))
((Restrictive Mode - but expand environment))
((Expanding Mode: Continuous - but expand on key locations))
```

**AI Adapts:** Expands specified elements, restricts others
