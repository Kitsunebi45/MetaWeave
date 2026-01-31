# Neural Network Mapping

> Extracting coordination algorithms from gameplay for multi-agent systems

**Version:** 0.1.0-alpha
**Last Updated:** 2026-01-31
**Status:** Active Development

---

## Table of Contents

1. [Overview](#overview)
2. [The Extraction Pipeline](#the-extraction-pipeline)
3. [Pattern Categories](#pattern-categories)
4. [From Gameplay to Algorithm](#from-gameplay-to-algorithm)
5. [Training Data Structure](#training-data-structure)
6. [Network Architecture Targets](#network-architecture-targets)
7. [Validation Framework](#validation-framework)
8. [m∴We Mesh Integration](#mwe-mesh-integration)

---

## Overview

### The Core Insight

Human coordination—especially among neurodivergent and plural folks—has evolved sophisticated patterns for managing:
- Competing internal priorities
- Resource scarcity
- Trust verification
- Conflict resolution
- State recovery

These patterns, when formalized, become **algorithms for multi-agent coordination**.

### The Pipeline

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Gameplay   │────▶│  Pattern    │────▶│  Algorithm  │────▶│   Neural    │
│   Events    │     │  Detection  │     │  Extraction │     │   Network   │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
                           │                   │
                           ▼                   ▼
                    ┌─────────────┐     ┌─────────────┐
                    │  Narrative  │     │  Formal     │
                    │  Annotation │     │  Pseudocode │
                    └─────────────┘     └─────────────┘
```

### Why This Works

1. **Rich Signal** - Gameplay decisions encode complex reasoning
2. **Structured Context** - Game state provides clean input features
3. **Repeated Trials** - Many games = many data points
4. **Multi-Agent** - Sprites + humans = real coordination data
5. **Ground Truth** - Outcomes (success/failure) provide labels

---

## The Extraction Pipeline

### Stage 1: Event Collection

Raw gameplay events captured in real-time:

```javascript
// Example event stream
[
  { type: "turn_start", entropy: 4, anchor: 3, energy: 5 },
  { type: "card_play", card: "fox_clever_redirect", target: "entropy" },
  { type: "entropy_change", old: 4, new: 3, source: "fox_clever_redirect" },
  { type: "coordination_attempt", initiator: "player", target: "sprite_ember" },
  { type: "coordination_result", success: true, mechanism: "negotiation" },
  { type: "turn_end", entropy: 3, anchor: 5, energy: 3 }
]
```

### Stage 2: Pattern Detection

Sliding window analysis identifies recurring sequences:

```python
def detect_patterns(event_stream, window_size=10):
    """
    Find repeated subsequences in event stream
    """
    patterns = {}

    for i in range(len(event_stream) - window_size):
        window = event_stream[i:i + window_size]
        signature = extract_signature(window)

        if signature in patterns:
            patterns[signature].append(window)
        else:
            patterns[signature] = [window]

    # Filter to patterns that occur multiple times
    recurring = {k: v for k, v in patterns.items() if len(v) >= 3}

    return recurring
```

### Stage 3: Narrative Annotation

Players and researchers add context to detected patterns:

```json
{
  "patternId": "entropy_spike_recovery_001",
  "signature": "entropy_rise → anchor_play → entropy_stabilize",
  "occurrences": 7,
  "playerAnnotation": "This is what I do when I feel dissociation coming on",
  "researcherAnnotation": "Classic grounding response pattern",
  "narrativeDescription": "When entropy spikes above 6, player immediately plays an anchor card, followed by a pause (no plays for 2 turns), then resumes normal play at lower entropy."
}
```

### Stage 4: Algorithm Extraction

Apply the narrative-to-algorithm framework (see `/research/narrative-to-algorithm-extractor.md`):

```
Algorithm: Entropy Spike Recovery

STATE:
- Entropy crosses threshold (>6)
- Anchor cards available in hand
- Energy sufficient for play

TRIGGERS:
- Entropy increase event
- New entropy > 6
- Previous entropy <= 6

COORDINATION:
- Internal check: "Do I have resources?"
- If yes: immediate anchor play
- If no: enter conservation mode

RESOLUTION:
- Entropy reduced by anchor value
- Enter recovery period (reduced plays)
- Resume normal when entropy < 4

PSEUDOCODE:
```python
def entropy_spike_response(game_state, hand):
    if game_state.entropy > 6 and game_state.prev_entropy <= 6:
        # Spike detected
        anchor_cards = [c for c in hand if c.type == "anchor"]

        if anchor_cards and game_state.energy >= min(c.cost for c in anchor_cards):
            best_anchor = max(anchor_cards, key=lambda c: c.anchor_value)
            play_card(best_anchor)
            enter_recovery_mode(duration=2)
        else:
            enter_conservation_mode()
```
```

### Stage 5: Neural Network Encoding

Convert algorithm to training data:

```json
{
  "input": {
    "game_state": {
      "entropy": 7,
      "prev_entropy": 5,
      "anchor": 2,
      "energy": 4,
      "hand_composition": {
        "anchor_cards": 2,
        "action_cards": 3,
        "creature_cards": 1
      }
    },
    "context": {
      "turn_number": 12,
      "recent_entropy_trend": "rising",
      "coordination_available": true
    }
  },
  "expected_output": {
    "action_type": "play_card",
    "card_type": "anchor",
    "urgency": "high",
    "follow_up": "recovery_mode"
  },
  "algorithm_reference": "entropy_spike_recovery",
  "outcome": "success"
}
```

---

## Pattern Categories

### Recovery Patterns

Sequences that restore stability after disruption:

| Pattern | Trigger | Response | Outcome |
|---------|---------|----------|---------|
| Entropy Spike Recovery | entropy > threshold | anchor play + pause | stability restored |
| Energy Debt Recovery | energy < 0 | rest cards + reduced plays | energy positive |
| Crisis Intervention | entropy > 9 | emergency anchor sequence | crisis averted |
| Cascade Prevention | 3+ entropy gains in row | preemptive anchor | cascade stopped |

### Coordination Patterns

Multi-agent interaction sequences:

| Pattern | Agents | Mechanism | Outcome |
|---------|--------|-----------|---------|
| Cooperative Play | player + sprite | synchronized card play | bonus effect |
| Negotiated Resolution | competing sprites | bid/counterbid | winner selected |
| Trust Building | any two agents | repeated successful coordination | trust score increases |
| Conflict De-escalation | opposing goals | anchor + pause | conflict dissolved |

### Adaptation Patterns

Responses to changing conditions:

| Pattern | Stimulus | Adaptation | Duration |
|---------|----------|------------|----------|
| Hormone Shift Response | firmware change | suit preference change | until next shift |
| Resource Scarcity Mode | low energy | efficiency prioritization | until recovery |
| High Entropy Play | entropy 6-8 | high-risk high-reward | variable |
| Integration Pursuit | diverse suits available | balanced play | until victory |

### Meta Patterns

Patterns about patterns:

| Pattern | Observation | Inference | Application |
|---------|-------------|-----------|-------------|
| Strategy Switching | repeated failure | try different approach | flexibility marker |
| Pattern Recognition | opponent repeats | predict next move | counter-play |
| Self-Modeling | review own patterns | identify habits | optimization |

---

## From Gameplay to Algorithm

### Example 1: The "Check Before Leap" Pattern

**Observed Gameplay:**
```
Turn 5: Player hovers over card, doesn't play, ends turn
Turn 6: Entropy drops naturally, player plays the card
Turn 7: Success, no entropy spike
---
Turn 12: Player hovers over card, doesn't play, ends turn
Turn 13: Entropy drops naturally, player plays the card
Turn 14: Success, no entropy spike
```

**Narrative Annotation:**
"I've learned to wait for entropy to settle before making big plays. If I'm above 4, I check if it's trending down before committing."

**Extracted Algorithm:**
```python
def check_before_leap(intended_action, game_state):
    """
    Delay high-impact actions until entropy stabilizes
    """
    # Define high-impact threshold
    if intended_action.entropy_risk < 3:
        return PROCEED  # Low risk, just do it

    # Check current stability
    if game_state.entropy <= 4:
        return PROCEED  # Already stable

    # Check trend
    if game_state.entropy_trend == "falling":
        # Decide: wait or act?
        if game_state.entropy - game_state.predicted_next_entropy >= 2:
            return WAIT_ONE_TURN  # Worth waiting

    if game_state.entropy_trend == "rising":
        # Getting worse, might need to act now
        if game_state.entropy < 7:
            return WAIT_ONE_TURN  # Still time
        else:
            return PROCEED_WITH_CAUTION  # Can't wait

    return PROCEED  # Default to action
```

### Example 2: The "Coalition Formation" Pattern

**Observed Gameplay:**
```
Coordination Event: Player proposes team play with Sprite Ember
  - Ember's goal: high entropy plays
  - Player's goal: stability
  - Initial: incompatible

Player plays Cat suit card (comfort, reduces Ember's entropy preference)
Ember's modified goal: medium entropy plays
Coordination re-attempted: SUCCESS

Player and Ember execute combined play
  - Ember contributes entropy
  - Player contributes anchor
  - Net result: powerful play, stable state
```

**Narrative Annotation:**
"Ember and I have different styles, but if I can shift the vibe a little with a comfort play, we can find common ground. It's like... compromising on the energy level of the room."

**Extracted Algorithm:**
```python
def coalition_formation(agent_a, agent_b):
    """
    Find common ground between agents with different goals
    """
    # Assess compatibility
    compatibility = calculate_goal_overlap(agent_a.goals, agent_b.goals)

    if compatibility > DIRECT_COOPERATION_THRESHOLD:
        return COOPERATE_DIRECTLY

    if compatibility < INCOMPATIBLE_THRESHOLD:
        return ABANDON_COALITION

    # Partial compatibility: try modulation
    modulation_options = find_modulation_plays(agent_a, agent_b)

    for option in modulation_options:
        simulated_compatibility = simulate_post_modulation(
            agent_a, agent_b, option
        )

        if simulated_compatibility > DIRECT_COOPERATION_THRESHOLD:
            # Found a bridge!
            execute_modulation(option)
            return COOPERATE_AFTER_MODULATION

    # No bridge found
    return COEXIST_WITHOUT_COOPERATING

def find_modulation_plays(agent_a, agent_b):
    """
    Find cards that shift one agent's preferences toward compatibility
    """
    modulations = []

    for card in agent_a.available_cards:
        if card.affects_preferences:
            new_goals_b = apply_preference_shift(agent_b.goals, card.effect)
            new_compatibility = calculate_goal_overlap(agent_a.goals, new_goals_b)

            if new_compatibility > calculate_goal_overlap(agent_a.goals, agent_b.goals):
                modulations.append({
                    'card': card,
                    'improvement': new_compatibility - compatibility,
                    'target': agent_b
                })

    return sorted(modulations, key=lambda m: m['improvement'], reverse=True)
```

---

## Training Data Structure

### Input Features

```python
input_schema = {
    # Current game state
    "entropy": float,           # 0-10
    "anchor": float,            # 0-10
    "energy": float,            # can be negative
    "turn_number": int,

    # Trends (computed)
    "entropy_trend": categorical,  # rising, falling, stable
    "entropy_velocity": float,      # rate of change
    "anchor_trend": categorical,
    "energy_trend": categorical,

    # Hand composition
    "hand_size": int,
    "anchor_cards_available": int,
    "action_cards_available": int,
    "suit_distribution": dict,     # {suit: count}

    # Hormone state (firmware)
    "estrogen_level": float,
    "testosterone_level": float,
    "cortisol_level": float,
    "dopamine_level": float,
    "serotonin_level": float,

    # Multi-agent context
    "agents_present": list,        # IDs of active agents
    "coordination_available": bool,
    "trust_levels": dict,          # {agent_id: trust_score}
    "pending_negotiations": list,

    # History (sliding window)
    "recent_plays": list,          # Last 5 plays
    "recent_outcomes": list,       # Success/failure
    "patterns_active": list        # Currently matching patterns
}
```

### Output Labels

```python
output_schema = {
    # Action selection
    "action_type": categorical,    # play_card, end_turn, coordinate, anchor_behavior
    "action_target": str,          # Card ID or agent ID
    "action_urgency": float,       # 0-1 priority

    # Strategic context
    "strategy_mode": categorical,  # aggressive, defensive, recovery, coordination
    "time_horizon": categorical,   # immediate, short_term, long_term

    # Coordination (if applicable)
    "coordination_intent": categorical,  # propose, accept, reject, counter
    "coordination_target": str,
    "concession_willing": float,   # 0-1 flexibility

    # Meta
    "confidence": float,           # Model's confidence in this action
    "algorithm_invoked": str       # Which extracted algorithm this matches
}
```

### Training Example

```json
{
  "input": {
    "entropy": 6.5,
    "anchor": 2.0,
    "energy": 3.0,
    "turn_number": 8,
    "entropy_trend": "rising",
    "entropy_velocity": 1.5,
    "hand_size": 5,
    "anchor_cards_available": 2,
    "estrogen_level": 0.7,
    "cortisol_level": 0.8,
    "agents_present": ["player", "sprite_ember"],
    "coordination_available": true,
    "trust_levels": {"sprite_ember": 0.6},
    "recent_plays": ["fox_01", "cat_03", "action_05"],
    "patterns_active": ["entropy_rising_sequence"]
  },
  "output": {
    "action_type": "play_card",
    "action_target": "cat_anchor_07",
    "action_urgency": 0.85,
    "strategy_mode": "recovery",
    "time_horizon": "immediate",
    "confidence": 0.78,
    "algorithm_invoked": "entropy_spike_recovery"
  },
  "outcome": {
    "success": true,
    "entropy_after": 4.0,
    "pattern_completed": "entropy_spike_recovery"
  }
}
```

---

## Network Architecture Targets

### Model 1: Action Predictor

**Purpose:** Given game state, predict optimal action

**Architecture:**
```
Input Layer: Game state features (normalized)
    ↓
LSTM Layer: Process recent history sequence
    ↓
Attention Layer: Focus on relevant state elements
    ↓
Dense Layers: Feature combination
    ↓
Output Layer: Action probabilities
```

**Training:**
- Supervised learning on successful plays
- Reinforcement learning for long-term strategy

### Model 2: Coordination Predictor

**Purpose:** Predict coordination success probability

**Architecture:**
```
Input: Agent A state + Agent B state + History
    ↓
Siamese Network: Encode each agent's features
    ↓
Interaction Layer: Model relationship dynamics
    ↓
LSTM: Process coordination history
    ↓
Output: Success probability + suggested mechanism
```

**Training:**
- Binary classification on coordination outcomes
- Learn what factors predict successful coordination

### Model 3: Pattern Recognizer

**Purpose:** Identify which known algorithm matches current situation

**Architecture:**
```
Input: Event sequence (variable length)
    ↓
1D CNN: Extract local patterns
    ↓
LSTM: Capture sequence dependencies
    ↓
Attention: Weight important events
    ↓
Classification: Match to known algorithms
```

**Training:**
- Multi-class classification
- Continual learning as new patterns are extracted

### Model 4: Sprite Agent

**Purpose:** Autonomous gameplay agent

**Architecture:**
```
World Model: Predict game state transitions
    ↓
Planner: Search future action sequences
    ↓
Value Network: Evaluate positions
    ↓
Policy Network: Select actions
    ↓
Communication Module: Coordinate with others
```

**Training:**
- Self-play with other Sprites
- Human-Sprite gameplay data
- Algorithm library as behavioral primitives

---

## Validation Framework

### Internal Validation

**Holdout Testing:**
- 80/10/10 train/val/test split
- Stratify by pattern type and player

**Cross-Validation:**
- K-fold by session (sessions from same player stay together)
- Leave-one-player-out for generalization testing

**Metrics:**
- Action prediction accuracy
- Coordination success prediction AUC
- Pattern recognition F1

### External Validation

**Human Evaluation:**
- Show model decisions to players
- "Would you have done this?" rating
- Explanability assessment

**Gameplay Testing:**
- Sprite agents play against humans
- Track coordination success rates
- Compare to baseline (random, simple heuristics)

**Transfer Testing:**
- Do patterns extracted from Player A work for Player B?
- Cross-demographic validation
- Cross-game-mode validation

### Fairness Evaluation

**Demographic Parity:**
- Model performs equally across demographic groups
- No systematic bias against any player type

**Individual Fairness:**
- Similar players get similar predictions
- Personal calibration respects individual differences

---

## m∴We Mesh Integration

### How This Feeds the Larger Project

The m∴We card game is a **research instrument** for the m∴We mesh network:

```
Card Game Algorithms → Sprite Behavior → Mesh Node Behavior

Patterns like:
- "Check before leap" → Cautious message propagation
- "Coalition formation" → Dynamic node clustering
- "Entropy recovery" → Network self-healing
- "Trust building" → Reputation system mechanics
```

### Key Transfers

| Game Concept | Mesh Concept |
|--------------|--------------|
| Entropy | Network instability/congestion |
| Anchor | Consensus/synchronization points |
| Coordination | Multi-node message passing |
| Sprites | Autonomous mesh agents |
| Hormone system | Network-wide state parameters |
| Trust scores | Node reputation |

### Research Questions

1. Can coordination algorithms from human plural systems improve multi-agent coordination in distributed networks?

2. Do biological agents (humans) and digital agents (Sprites) develop novel coordination patterns when they interact?

3. Can self-healing patterns from dissociation recovery inform network resilience?

4. What trust-building mechanisms transfer from game coordination to mesh authentication?

---

## Implementation Roadmap

### Phase 1: Collection Infrastructure
- [ ] Event logging system
- [ ] Pattern detection algorithms
- [ ] Annotation interface

### Phase 2: Extraction Tools
- [ ] Narrative-to-algorithm pipeline integration
- [ ] Pseudocode generation
- [ ] Pattern library structure

### Phase 3: Neural Network Training
- [ ] Training data pipeline
- [ ] Model architecture implementation
- [ ] Training infrastructure

### Phase 4: Sprite Integration
- [ ] Sprite behavior engine
- [ ] Pattern-based action selection
- [ ] Human-Sprite coordination

### Phase 5: Mesh Transfer
- [ ] Algorithm adaptation for mesh context
- [ ] Simulation testing
- [ ] Live mesh integration

---

## Document History

| Date | Version | Changes |
|------|---------|---------|
| 2026-01-31 | 0.1.0 | Initial scaffold |

---

*This is a living document. Updates tracked in git.*
