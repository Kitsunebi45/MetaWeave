# m∴We Data Collection Framework

> Ethical data collection for recovery tracking and neural network research

**Version:** 0.1.0-alpha
**Last Updated:** 2026-01-31
**Status:** Active Development

---

## Table of Contents

1. [Philosophy](#philosophy)
2. [Consent Framework](#consent-framework)
3. [Data Types](#data-types)
4. [Storage Architecture](#storage-architecture)
5. [Export Formats](#export-formats)
6. [Research Use Cases](#research-use-cases)
7. [Privacy Protections](#privacy-protections)
8. [Player Rights](#player-rights)

---

## Philosophy

### Core Principles

1. **Player Ownership** - Your data belongs to you, always
2. **Local First** - Nothing leaves your device without explicit action
3. **Informed Consent** - Clear explanation of what data means and how it's used
4. **Granular Control** - Choose what to share, with whom, at what level
5. **Reciprocity** - If we use your data for research, you benefit too

### Why Collect Data?

**For the Player:**
- Track patterns over time (medications, hormones, behaviors)
- Identify triggers and effective coping strategies
- Create evidence for healthcare providers
- Build self-knowledge through reflection

**For Research:**
- Extract coordination algorithms from multi-agent play
- Understand how biological and digital agents interact
- Develop better support tools for neurodivergent/plural folks
- Advance m∴We mesh network design

**The Deal:**
- Research participation is always optional
- Research participants are compensated (store credit, early access)
- Aggregate findings shared back with community
- Individual findings remain private unless you choose to share

---

## Consent Framework

### Consent Levels

| Level | What It Means | Data Leaves Device? | Compensation |
|-------|---------------|---------------------|--------------|
| `local_only` | Data stays on your device forever | No | None (default) |
| `anonymized_research` | Stripped of identifiers, aggregated | Yes, anonymized | $2 store credit |
| `identified_research` | Linked to research ID (not real identity) | Yes, pseudonymized | $5 store credit + early access |
| `public_dataset` | Contributed to open research | Yes, anonymized | $10 credit + co-author option |

### Consent Flow

```
┌─────────────────────────────────────────────────────────┐
│                   FIRST LAUNCH                          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  "m∴We collects gameplay data to help you track        │
│   patterns and optionally contribute to research.       │
│                                                         │
│   By default, ALL data stays on YOUR device.            │
│                                                         │
│   You can change this anytime in Settings."             │
│                                                         │
│           [ Got it, start playing ]                     │
│                                                         │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                   RESEARCH OPT-IN                       │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  "Would you like to contribute to research?             │
│                                                         │
│   Your gameplay patterns help us understand how         │
│   people coordinate, recover, and adapt.                │
│                                                         │
│   ○ Keep my data local only (default)                   │
│   ○ Share anonymized data ($2 credit)                   │
│   ○ Share with research ID ($5 credit + early access)   │
│   ○ Contribute to public dataset ($10 credit)           │
│                                                         │
│   [ Learn more about each option ]                      │
│                                                         │
│           [ Save preference ]                           │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Consent Modification

Players can change consent at any time:
- **Upgrade:** Immediately effective
- **Downgrade:** Stops future sharing; can request deletion of previously shared data
- **Full deletion:** Nuclear option, removes all shared data (may take 30 days)

### Per-Session Consent

Some sessions may contain sensitive content. Players can:
- Mark individual sessions as "local only" regardless of global setting
- Add content warnings for their own future reference
- Exclude specific events from any export

---

## Data Types

### Automatic Collection

These are collected during normal gameplay:

| Data Type | Description | Research Value |
|-----------|-------------|----------------|
| Card plays | Which cards, when, in what order | Decision patterns |
| Game state | Entropy, anchor, energy over time | State tracking |
| Hormone levels | Simulated firmware state | Transition tracking |
| Coordination events | Multi-agent interactions | Algorithm extraction |
| Session metadata | Duration, time of day, completion | Usage patterns |

### Player-Annotated Data

Optional additions that enrich the dataset:

| Data Type | Description | Research Value |
|-----------|-------------|----------------|
| Mood tags | Player-reported emotional state | Correlation with gameplay |
| Real-world context | What was happening IRL | Situational patterns |
| Effectiveness ratings | How well did strategies work | Outcome evaluation |
| Free-text notes | Any additional context | Qualitative richness |

### Derived Data

Computed from raw data:

| Data Type | Description | Research Value |
|-----------|-------------|----------------|
| Pattern sequences | Repeated play patterns | Behavioral signatures |
| Coordination graphs | Agent interaction networks | Network analysis |
| Entropy trajectories | Stability over time | Recovery patterns |
| Strategy clusters | Similar play styles | Player typologies |

---

## Storage Architecture

### Local Storage

```
IndexedDB: mweave_game_data
├── sessions/
│   ├── {session_id}/
│   │   ├── metadata.json
│   │   ├── events.json
│   │   └── annotations.json
├── player_profile/
│   ├── preferences.json
│   ├── calibration.json
│   └── consent.json
├── research_cache/
│   └── pending_upload.json
└── exports/
    └── {export_id}.json
```

### Data Retention

| Data Type | Local Retention | Research Retention |
|-----------|-----------------|-------------------|
| Gameplay events | Forever (player-controlled) | 7 years or study completion |
| Annotations | Forever | 7 years or study completion |
| Aggregated patterns | Forever | Indefinite (anonymized) |
| Raw consent records | Forever | Forever (legal requirement) |

### Encryption

- Local data: Device-level encryption (browser storage)
- Export files: Optional password protection
- Research transmission: TLS 1.3 + at-rest encryption
- Identified data: Additional application-layer encryption

---

## Export Formats

### Personal Export (JSON)

```json
{
  "exportVersion": "1.0.0",
  "exportDate": "2026-01-31T12:00:00Z",
  "playerId": "local_player",
  "sessions": [
    {
      "sessionId": "abc-123",
      "startTime": "2026-01-30T18:00:00Z",
      "endTime": "2026-01-30T18:45:00Z",
      "events": [...],
      "annotations": [...],
      "summary": {
        "entropyPeak": 7,
        "anchorTotal": 12,
        "cardsPlayed": 23,
        "coordinationAttempts": 3,
        "coordinationSuccesses": 2
      }
    }
  ],
  "patterns": [...],
  "calibration": {...}
}
```

### Research Export (Anonymized)

```json
{
  "exportVersion": "1.0.0",
  "consentLevel": "anonymized_research",
  "anonymizationVersion": "2.0",
  "participantId": "ANON_7f8a9b2c",
  "demographicBucket": "adult_neurodivergent",
  "sessions": [
    {
      "sessionId": "REDACTED",
      "dayOfWeek": "thursday",
      "timeOfDay": "evening",
      "events": [
        {
          "eventType": "card_play",
          "cardId": "fox_clever_redirect",
          "gameState": {...},
          "annotation": null  // Free text removed
        }
      ]
    }
  ]
}
```

### Provider Report (PDF)

Formatted summary for healthcare providers:

```
GAMEPLAY SUMMARY REPORT
Patient: [Name if provided]
Period: January 2026
Generated: 2026-01-31

PATTERNS OBSERVED:
- Entropy peaks correlate with [player-tagged: work stress]
- Most effective anchor behaviors: breathing exercises, cold water
- Hormone simulation suggests estrogen-related patterns

NOTABLE SESSIONS:
- Jan 15: High entropy managed successfully with Cat suit strategies
- Jan 22: Crisis event, recovered via anchor card sequence

[Chart: Entropy/Anchor over time]
[Chart: Hormone simulation tracking]
```

---

## Research Use Cases

### Coordination Algorithm Extraction

**Goal:** Extract formal algorithms from gameplay patterns

**Method:**
1. Identify multi-agent coordination events in gameplay
2. Apply narrative-to-algorithm extractor framework
3. Formalize patterns as pseudocode
4. Validate across multiple players
5. Test in Sprite agent behavior

**Data Required:**
- Coordination events with all participants
- Before/after game state
- Success/failure outcome
- Player annotations on intention

**See:** `/research/narrative-to-algorithm-extractor.md`

### Recovery Pattern Analysis

**Goal:** Identify effective recovery strategies

**Method:**
1. Track entropy trajectories over sessions
2. Identify intervention points (anchor cards, behaviors)
3. Measure effectiveness by entropy reduction
4. Cluster similar patterns across players
5. Generate recommendations

**Data Required:**
- Full session event logs
- Entropy/anchor time series
- Anchor behavior completion and ratings
- Pre/post session mood tags

### Hormone Transition Tracking

**Goal:** Model effects of HRT on behavior/mood

**Method:**
1. Correlate hormone simulation state with gameplay patterns
2. Track changes over extended periods (months)
3. Identify suit affinities at different hormone levels
4. Compare with player-reported real-world state

**Data Required:**
- Long-term gameplay history
- Hormone calibration data
- Player annotations on real-world HRT status
- Identified research consent (for longitudinal tracking)

### Multi-Agent Network Design

**Goal:** Inform m∴We mesh network architecture

**Method:**
1. Analyze Sprite-biological coordination patterns
2. Identify trust-building sequences
3. Map conflict resolution strategies
4. Extract communication protocols

**Data Required:**
- All coordination events
- Trust metric changes
- Conflict/resolution pairs
- Agent type identification

---

## Privacy Protections

### Anonymization Process

```
RAW DATA                    ANONYMIZED DATA
─────────                   ───────────────
player_email: kit@ex.com    participantId: ANON_7f8a9b
real_name: Kitty            [removed]
timestamp: 2026-01-31T18:32 dayOfWeek: friday, timeOfDay: evening
free_text: "stressed about  [removed or generalized]
           work deadline"
session_id: abc-123         session_id: [hashed]
device_info: iPhone 14      platform: mobile
```

### What We Never Collect

- Real names (unless provider report requested)
- Exact addresses or locations
- Financial information
- Passwords or credentials
- Photos or biometrics
- Other app data
- Contact lists
- Browsing history

### What We Strip During Anonymization

- Email addresses
- Exact timestamps (generalized to time windows)
- Free-text annotations (unless explicitly consented)
- Device identifiers
- IP addresses
- Session IDs (hashed)

### Differential Privacy

For aggregate statistics, we apply differential privacy:
- Add calibrated noise to counts
- Suppress small group statistics
- Use k-anonymity (k≥5) for demographic buckets

---

## Player Rights

### Right to Access

You can export all your data at any time:
- Settings → Data → Export My Data
- Formats: JSON (machine), PDF (human)
- Includes everything we have

### Right to Deletion

You can delete your data:
- Local data: Settings → Data → Delete All Local Data
- Research data: Settings → Data → Request Research Data Deletion
- Timeline: Local = immediate, Research = within 30 days

### Right to Correction

You can modify your data:
- Edit annotations on any session
- Recalibrate hormone simulation
- Update demographic information
- Correct any errors

### Right to Portability

Your data is yours:
- Standard JSON export format
- Documented schema (this document)
- No proprietary formats
- Works with other tools (if they exist)

### Right to Explanation

If automated decisions affect you:
- Sprite behavior explanations available
- Pattern detection logic documented
- No hidden algorithms affecting gameplay

---

## Implementation Checklist

### Phase 1: Local Storage
- [ ] IndexedDB schema implementation
- [ ] Event logging system
- [ ] Local export functionality
- [ ] Consent preference storage

### Phase 2: Annotation System
- [ ] Session tagging UI
- [ ] Mood tracking integration
- [ ] Free-text notes
- [ ] Effectiveness ratings

### Phase 3: Research Infrastructure
- [ ] Anonymization pipeline
- [ ] Secure upload mechanism
- [ ] Consent verification
- [ ] Compensation tracking

### Phase 4: Analysis Tools
- [ ] Pattern extraction algorithms
- [ ] Visualization dashboards
- [ ] Provider report generation
- [ ] Aggregate statistics

---

## Document History

| Date | Version | Changes |
|------|---------|---------|
| 2026-01-31 | 0.1.0 | Initial scaffold |

---

*This is a living document. Updates tracked in git.*
