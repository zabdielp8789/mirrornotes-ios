# MirrorNotes — Private AI Journaling for iPhone

[![App Store](https://img.shields.io/badge/App%20Store-Download-blue?logo=apple)](https://apps.apple.com/app/id6769007201)
[![iOS](https://img.shields.io/badge/iOS-17%2B-lightgrey?logo=apple)](https://apps.apple.com/app/id6769007201)
[![License](https://img.shields.io/badge/license-Proprietary-red)](https://mirrornotes.org)

> **Your journal text never leaves your iPhone. Ever.**

MirrorNotes is an AI-powered journaling app where all AI inference runs 100% on-device via **Gemma 3 1B** (CoreML). No cloud backend. No API calls. No server. Works in airplane mode.

**[Download on the App Store →](https://apps.apple.com/app/id6769007201)**  
**[Website → mirrornotes.org](https://mirrornotes.org)**

---

## What Makes It Different

Every other AI journaling app sends your text to a server. MirrorNotes doesn't.

```
Most apps:    You → your words → their server → AI model → insight → back to you
MirrorNotes:  You → your words → your iPhone  → AI model → insight
                                     ↑
                              nothing leaves here
```

The privacy guarantee is architectural: there is no network call path for journal content.

---

## Features

| Feature | Free | Core ($2.99/mo) | Deep ($4.99/mo) |
|---------|------|-----------------|-----------------|
| Unlimited entries, forever | ✓ | ✓ | ✓ |
| Full-text search (local) | ✓ | ✓ | ✓ |
| iCloud backup | ✓ | ✓ | ✓ |
| Daily Nudge | ✗ | ✓ | ✓ |
| Ask (15×/month) | ✗ | ✓ | ✗ |
| Ask (unlimited) | ✗ | ✗ | ✓ |
| Weekly Digest | ✗ | ✓ | ✓ |
| Home screen widget | ✗ | ✓ | ✓ |
| Monthly Deep Report | ✗ | ✗ | ✓ |
| Mood Timeline | ✗ | ✗ | ✓ |
| Mood Alerts | ✗ | ✗ | ✓ |

7-day free trial on all paid plans.

---

## AI Features (all on-device)

### Daily Nudge
A personalized morning reflection prompt based on your recent entries. After 4+ entries it gets genuinely personal — "You keep coming back to the word 'enough' in your entries. What would 'enough' feel like today?"

### Ask Your Journal
Ask open-ended questions. Your iPhone reads your entries and answers on-device.

```
"When was I most anxious this month?"
"What themes keep repeating?"
"What makes me feel energized?"
```

### Mood Timeline
Emotional pattern detection across days, weeks, months. Detects and visualizes tone: calm, anxious, energized, drained, etc.

### Weekly Digest
Every Sunday: a 7-day summary of your key themes, mood patterns, and what changed.

### Monthly Deep Report
Full analysis on the 1st of each month. Patterns, recurring themes, emotional arc for the month.

### Mood Alerts (Deep)
Notifies you if 3 consecutive entries register negative mood (anxious, overwhelmed, frustrated, drained, sad, numb).

---

## Technical Architecture

```
iOS (SwiftUI + SwiftData)
├── Local storage:   SwiftData (iOS 17+)
├── Cloud sync:      CloudKit (one line: ModelConfiguration(cloudKitDatabase: .automatic))
└── AI:              LocalLLMService — Gemma 3 1B via CoreML, fully on-device
```

**Key implementation details:**
- `LocalLLMService.swift` — Gemma 3 1B inference engine
- `InsightService.swift` — all system prompts for nudge/ask/digest/report
- `BGAppRefreshTask` — weekly digest trigger (Sunday 7AM)
- `RevenueCat` — subscription management, Apple IAP
- All AI responses cached in SwiftData with 24h TTL — never regenerates within cache window

**Why Gemma 3 1B is enough:**  
Personal journaling AI doesn't need GPT-4. The task is pattern-matching your own writing over time, not general world reasoning. Gemma 3 1B is fast, private, and handles it well on modern Apple Silicon.

---

## Onboarding Design

Staged — AI unlocks after 4+ entries:

```
Day 0:    3 onboarding questions + first entry
Day 1–3:  No AI. "mirror is learning — 3 more entries to first insight"
Day 4–7:  First Daily Nudge unlocks
          → Show paywall AFTER first nudge (user has felt the value)
Week 2+:  Full experience. Weekly digest on Sunday.
```

Paywall shown after the first AI insight, not before. Conversion peaks when users feel value.

---

## Privacy

- Journal text: **never transmitted**
- AI inference: **on-device only** (Gemma 3 via CoreML)
- Sync: **private iCloud** (optional, encrypted, only you have the key)
- Analytics: **none on journal content**
- Account: **not required**

---

## Download

**[App Store → apps.apple.com/app/id6769007201](https://apps.apple.com/app/id6769007201)**

Free to download. 7-day trial on AI features. No credit card required.

---

*Built with SwiftUI, SwiftData, CloudKit, Gemma 3, and CoreML.*  
*Website: [mirrornotes.org](https://mirrornotes.org)*
