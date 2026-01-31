# m∴We Card Game - Design Document

> A tarot-based deck battler for recovery, research, and revenue

**Version:** 0.1.0-alpha
**Last Updated:** 2026-01-31
**Status:** Active Development

---

## Table of Contents

1. [Vision & Goals](#vision--goals)
2. [The Three-Layer Architecture](#the-three-layer-architecture)
3. [Card System](#card-system)
4. [Core Mechanics](#core-mechanics)
5. [The Entropy/Anchor System](#the-entropynchor-system)
6. [Hormone Modifier System](#hormone-modifier-system)
7. [Sprite Agents](#sprite-agents)
8. [Use Cases](#use-cases)
9. [Technical Architecture](#technical-architecture)
10. [Monetization](#monetization)

---

## Vision & Goals

m∴We is a collectible card game that operates on multiple levels simultaneously:

### Research Lineage

This project builds on collaborative research from multiple sources:
- **Kitty/mKat (Fox/Cat/Squirrel system)** - Core design, plural system mechanics, HRT tracking
- **Ace and dyad** - Medication change modeling, firmware layer dynamics, the "Ace" variable (controlled chaos injection)
- **BPD-AvPD Relational Lock Analysis** - The "Two-Headed Ouroboros" model for relational coordination algorithms
- **Tiamat Protocol** - Systemic trauma mapping, the 11 Monsters taxonomy, Empire vs. Vixen Path framework
- **Simulation work** - Relational navigation strategies for complex family dynamics

The game mechanics encode hard-won insights about coordination, recovery, and multi-agent negotiation from lived experience.

### Primary Functions

1. **Personal Recovery Tool**
   - Track medication and hormone changes over time
   - Find behavioral analogs for internal states
   - Provide grounding anchors during dissociative episodes
   - Create language for experiences that resist description

2. **Neural Network Research Platform**
   - Gameplay data extracts coordination algorithms
   - Player choices reveal decision-making patterns
   - Multi-agent interactions generate training data
   - Bridges biological and digital agent research

3. **m∴We Mesh Network Prototype**
   - HTML/JS base allows testing agent interactions
   - Sprite entities model autonomous digital agents
   - Human players model biological agents
   - Coordination patterns transfer to larger network design

4. **Sustainable Revenue**
   - $5 upfront purchase, ethical monetization
   - No predatory mechanics (no loot boxes, no pay-to-win)
   - Expansion packs add content without obsoleting existing cards
   - Research participation optional, compensated

5. **Plural/System Support**
   - Mechanics designed with system experiences in mind
   - Cards can represent different parts/alters
   - Coordination mechanics mirror internal negotiation
   - Safe space for exploring multiplicity

---

## The Three-Layer Architecture

The game models consciousness/experience through three interdependent layers:

### Hardware Layer (Body)
- Physical state, sensations, proprioception
- Sleep, nutrition, movement, environment
- The substrate everything else runs on
- **Card examples:** Grounding cards, physical anchor behaviors

### Firmware Layer (Hormones/Neurotransmitters)
- Estrogen, testosterone, cortisol, dopamine, serotonin, etc.
- Slower-changing, sets the "baseline"
- Affects how software layer operates
- **Card examples:** Hormone modifier cards, transition-related effects

### Software Layer (Medications/Behaviors)
- Fast-acting changes (stimulants, anxiolytics, behaviors)
- Conscious choices and coping mechanisms
- Runs on top of firmware, constrained by hardware
- **Card examples:** Action cards, behavioral strategies

### Layer Interactions

```
┌─────────────────────────────────────────┐
│           SOFTWARE LAYER                │
│    (medications, behaviors, choices)    │
│         ↑↓ fast changes ↑↓              │
├─────────────────────────────────────────┤
│           FIRMWARE LAYER                │
│    (hormones, neurotransmitters)        │
│         ↑↓ slow changes ↑↓              │
├─────────────────────────────────────────┤
│           HARDWARE LAYER                │
│    (body, environment, substrate)       │
│              foundation                 │
└─────────────────────────────────────────┘
```

Cards can target specific layers or cascade across layers. Firmware changes affect which software cards are effective. Hardware limitations constrain everything above.

---

## Card System

### The 100-Card Tarot Deck

**7 Animal Suits × 14 cards each = 98 cards + 2 Moon cards = 100 total**

#### The Seven Suits (Yokai)

The suits draw from Japanese folklore, each representing a yokai (supernatural spirit) with distinct personality and domain. This framing honors the liminal, transformative nature of the experiences the game models.

| Suit | Yokai | Japanese | Domain | Personality | Layer Affinity |
|------|-------|----------|--------|-------------|----------------|
| 🦊 | Kitsune | 狐 | Adaptation, cunning, shapeshifting | Clever, flexible, trickster, messenger of Inari | Software |
| 🐱 | Nekomata | 猫又 | Comfort, boundaries, independence | Self-caring, two-tailed, guardian of thresholds | Firmware |
| 🐿️ | Mujina | 貉 | Preparation, anxiety, resource hoarding | Busy, worried, shapeshifter, "divine prolific one" | Software |
| 🐢 | Genbu | 玄武 | Protection, patience, endurance | Divine tortoise of the North, guardian, slow wisdom | Hardware |
| 🐰 | Usagi/Gyokuto | 玉兎 | Speed, creativity, selfless sacrifice | Moon rabbit, mochi-maker, quick and generous | Software |
| 🐦‍⬛ | Karasu Tengu | 烏天狗 | Intelligence, transformation, wind | Crow tengu, collector, ominous wisdom | Firmware |
| 🕷️ | Jorōgumo | 絡新婦 | Creation, patience, interconnection | Spider woman, weaver, patient networker | All layers |

**Yokai Lore Notes:**
- **Kitsune** grow additional tails as they age (up to 9), each representing accumulated wisdom. Perfect for tracking growth/change over time.
- **Nekomata** are cats whose tails have split in two after long life - they guard boundaries and can see the unseen.
- **Mujina** (badger/tanuki family) are master shapeshifters associated with preparation and the Ainu "divine prolific one."
- **Genbu** is one of the Four Symbols - a divine tortoise entwined with a snake, representing winter and the north.
- **Usagi/Gyokuto** - the moon rabbit who selflessly offered himself and now pounds mochi on the moon.
- **Karasu Tengu** - bird-like tengu with crow features, masters of wind and martial arts, collectors of knowledge.
- **Jorōgumo** - a spider who transforms into a beautiful woman, weaving intricate webs of connection.

#### The Moon Cards (Major Arcana)

| Card | Phase | Meaning |
|------|-------|---------|
| 🌑 | New Moon | Beginnings, potential, the unknown |
| 🌕 | Full Moon | Culmination, revelation, peak states |

#### Card Numbers (1-14 per suit)

Following tarot structure:
- **1 (Ace):** Pure essence of the suit
- **2-10:** Graduated expressions
- **11 (Page):** Messenger, learning
- **12 (Knight):** Action, movement
- **13 (Queen):** Mastery, nurturing
- **14 (King):** Authority, completion

### Card Types

1. **Creature Cards** - Persistent entities on the field
2. **Action Cards** - One-time effects
3. **Modifier Cards** - Attach to other cards/states
4. **Anchor Cards** - Physical grounding behaviors (see below)
5. **Moon Cards** - Wild/trump cards with special rules

---

## Core Mechanics

### Turn Structure

```
1. DRAW PHASE
   - Draw cards based on current state
   - Entropy level affects draw count

2. FIRMWARE CHECK
   - Apply ongoing hormone effects
   - Check for threshold triggers

3. MAIN PHASE
   - Play cards from hand
   - Activate abilities
   - Use anchor behaviors

4. COORDINATION PHASE
   - Multi-agent negotiation (if applicable)
   - Sprite interactions

5. RESOLUTION PHASE
   - Calculate entropy/anchor balance
   - Apply end-of-turn effects
   - Check win/loss conditions
```

### Resource Systems

**Energy** - Primary resource for playing cards
- Generated by certain cards and rest states
- Spent to play cards and activate abilities
- Can go negative (energy debt = exhaustion)

**Entropy** - Dissociation/chaos meter
- Increases from stress, certain cards, unanchored states
- High entropy = more powerful but unstable plays
- Too high = dissociative crisis (lose turn, cards scattered)

**Anchor** - Grounding/stability counter
- Built by anchor cards and physical behaviors
- Counters entropy accumulation
- Enables consistent, safe plays

### Win Conditions

Multiple valid endings depending on play style:

1. **Stability Victory** - Maintain low entropy for X turns
2. **Integration Victory** - All suits represented in play
3. **Research Victory** - Complete data collection milestones
4. **Coordination Victory** - Successful multi-agent sync
5. **Recovery Victory** - Navigate a scenario without crisis

*(Competitive modes have different conditions)*

---

## The Entropy/Anchor System

### Entropy: The Dissociation Mechanic

Entropy represents destabilization, dissociation, and chaos. It's not inherently bad - high entropy enables powerful plays - but unmanaged entropy leads to crisis.

```
ENTROPY LEVELS:
0-2:  Grounded     - Safe, stable, limited options
3-5:  Activated    - Alert, more options available
6-8:  Destabilized - Powerful plays, risk of crisis
9-10: Crisis       - Lose control, emergency protocols
```

### Anchor: The Grounding Mechanic

Anchor points counter entropy and represent physical/emotional grounding. Anchor cards often involve real-world behaviors.

```
ANCHOR SOURCES:
- Physical anchor cards (breathing, movement, sensation)
- Social anchor cards (connection, co-regulation)
- Cognitive anchor cards (naming, categorizing, orienting)
- Sensory anchor cards (5-4-3-2-1, texture, temperature)
- Ritual anchor cards (routine, familiar actions)
```

### The Balance

```
NET_STABILITY = anchor_total - entropy_total

if NET_STABILITY > 0:
    # Stable state, safe plays

if NET_STABILITY < 0:
    # Unstable, risk increases

if NET_STABILITY < -5:
    # Crisis imminent
```

---

## Hormone Modifier System

The firmware layer uses a hormone simulation that affects card effectiveness and available options.

### Tracked Hormones/Neurotransmitters

| Hormone | High State | Low State | Transition Relevance |
|---------|------------|-----------|---------------------|
| Estrogen | Emotional sensitivity, verbal fluency | Flat affect, word-finding issues | HRT tracking |
| Testosterone | Energy, aggression, libido | Fatigue, passivity | HRT tracking |
| Cortisol | Alertness, anxiety, immune suppression | Calm, potentially sluggish | Stress tracking |
| Dopamine | Motivation, pleasure, focus | Anhedonia, executive dysfunction | ADHD meds |
| Serotonin | Mood stability, sleep regulation | Depression, anxiety | Antidepressants |
| Oxytocin | Bonding, trust, calm | Isolation, suspicion | Social interaction |
| Adrenaline | Fight/flight, energy burst | Exhaustion, crash | Crisis states |

### Hormone Effects on Gameplay

```javascript
// Example: Estrogen affects Cat suit cards
if (hormones.estrogen > THRESHOLD_HIGH) {
    catCards.forEach(card => {
        card.effectiveness *= 1.3;  // More effective
        card.entropy_cost *= 0.8;   // Cheaper to play
    });
}

// Example: Low dopamine affects all action cards
if (hormones.dopamine < THRESHOLD_LOW) {
    actionCards.forEach(card => {
        card.energy_cost *= 1.5;    // More expensive
        card.available = checkMotivation(); // May not be playable
    });
}
```

### Personal Calibration

Players can calibrate the hormone system to their own experience:
- "When my estrogen is high, I feel..."
- "Low dopamine for me looks like..."
- Creates personalized gameplay that mirrors actual experience

---

## Sprite Agents

Sprites are autonomous digital agents that can play the game independently or alongside biological players.

### Sprite Types

| Sprite | Personality | Play Style | Coordination Role |
|--------|-------------|------------|-------------------|
| Ember | Curious, impulsive | High entropy plays | Scout, risk-taker |
| Moss | Patient, nurturing | Anchor-focused | Stabilizer, healer |
| Glitch | Chaotic, creative | Rule-bending | Wildcard, disruptor |
| Echo | Reflective, learning | Mimics player patterns | Mirror, researcher |

### Sprite Autonomy Levels

1. **Dormant** - Sprite doesn't act independently
2. **Suggestive** - Sprite suggests plays, player decides
3. **Cooperative** - Sprite plays alongside player
4. **Autonomous** - Sprite plays independently
5. **Teaching** - Sprite explains its decisions

### Research Value

Sprite interactions generate coordination data:
- How do digital agents and biological agents negotiate?
- What coordination patterns emerge?
- When do agents cooperate vs. conflict?
- How does trust develop across agent types?

---

## Use Cases

### Kitty's Use Case (Trans/Plural System)

**Goals:**
- Track estrogen changes and behavioral effects
- Find language for alter experiences
- Develop grounding strategies for dissociation
- Create safe play space for system exploration

**Relevant Mechanics:**
- Hormone modifier system (firmware)
- Entropy/anchor balance (dissociation management)
- Multiple creature cards (representing parts)
- Coordination mechanics (internal negotiation)

### Ace's Use Case (Medication Changes)

**Goals:**
- Track medication transitions
- Predict difficult periods
- Find behavioral compensations
- Document patterns for providers

**Relevant Mechanics:**
- Software layer cards (medication effects)
- Logging and pattern detection
- Anchor behaviors for stability
- Historical playback and analysis

### Ex-Partner Use Case (Pristiq Transition)

**Goals:**
- Navigate antidepressant change
- Manage withdrawal effects
- Find alternative support strategies
- Maintain stability through transition

**Relevant Mechanics:**
- Serotonin tracking in firmware layer
- Entropy management during transition
- Anchor cards for grounding
- Support network cards (social anchors)

---

## Technical Architecture

### Stack

```
Frontend:  HTML5 + CSS3 + Vanilla JavaScript
Storage:   Local Storage / IndexedDB
Export:    JSON (consent-locked)
Future:    PWA wrapper for mobile
```

### Data Flow

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   Player     │────▶│   Game       │────▶│   Local      │
│   Actions    │     │   Engine     │     │   Storage    │
└──────────────┘     └──────────────┘     └──────────────┘
                            │
                            ▼
                     ┌──────────────┐
                     │   Research   │
                     │   Export     │
                     │  (optional)  │
                     └──────────────┘
```

### Privacy Architecture

- All data stored locally by default
- Research export requires explicit consent
- Anonymization layer strips identifying info
- User owns their data always
- No server-side storage of gameplay

---

## Monetization

### Ethical Principles

1. **No Loot Boxes** - All purchases show exactly what you get
2. **No Pay-to-Win** - Expansions add variety, not power
3. **No Subscription Traps** - One-time purchases only
4. **No Data Sales** - Research participation is voluntary and compensated

### Revenue Streams

| Item | Price | Contents |
|------|-------|----------|
| Base Game | $5 | Full 100-card deck, all mechanics |
| Expansion: Seasons | $3 | 28 new cards (seasonal variants) |
| Expansion: Medications | $3 | 20 cards focused on med tracking |
| Art Pack: [Artist] | $2 | Alternate art for full deck |
| Research Participation | -$2 credit | Optional data contribution |

### Research Compensation

Players who opt into research data sharing receive:
- Store credit for expansions
- Early access to new features
- Acknowledgment in publications (if desired)
- Access to aggregate research findings

---

## Appendices

*To be added:*
- A. Full card list with stats
- B. Combo reference
- C. Sprite behavior algorithms
- D. Hormone calibration guide
- E. Research protocol
- F. Accessibility considerations

---

## Document History

| Date | Version | Changes |
|------|---------|---------|
| 2026-01-31 | 0.1.0 | Initial scaffold |

---

*This is a living document. Updates tracked in git.*
