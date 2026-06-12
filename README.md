# Otter.ai Workflow Gap Study

> Otter markets 93–95% accuracy. Users report 60–85%. The gap isn't the model — Otter has the features. Users just never find them. And in some cases, Otter uses them without telling users at all.

**[Case Study](CASE_STUDY.md)** | Built by [Sanmati Sawalwade](https://linkedin.com/in/sanmati-sawalwade)

---

## The Finding

Otter's speaker identification failures are almost entirely a surfacing and onboarding problem — not a model problem. Three features that already exist fix most of the gap. None of them are taught in onboarding.

| Feature | Where It Lives | What It Does | Who Knows About It |
|---|---|---|---|
| My Voiceprint | Account Settings → My Voiceprint | 2-min scripted reading → your voice auto-tagged forever | Almost nobody |
| Tag-early propagation | Live transcript during meeting | Tag a speaker mid-meeting → label propagates throughout | Almost nobody |
| Custom vocabulary | Settings → My Otter AI → Vocabulary | Add domain terms → 10–15% accuracy improvement | Almost nobody |

---

## 8 Findings — Ordered by Impact

### Finding 1 — Bad diarization cascades into wrong summaries and wrong action item owners
```
Bad diarization → Scrambled summary → Wrong action item owners → Broken accountability
```
The fix is upstream — clean diarization produces clean summaries automatically.

### Finding 2 — Otter has Zoom metadata import — but only for internal participants
OtterPilot pulls display names from Zoom's roster in real-time. Works for internal teams. Breaks for external guests, aliases, phone dial-ins, and partially for Teams/Meet. Fireflies handles edge cases better — 7.2% DER vs Otter's 10.7%.

### Finding 3 — Otter's onboarding teaches none of the features that actually work
Onboarding teaches: Connect Calendar → Try OtterPilot → Upgrade. My Voiceprint, tag-early propagation, and custom vocabulary all require independent discovery. This is the root cause of Findings 1, 4, and 5.

### Finding 4 — My Voiceprint exists but is one-sided, buried, and four years out of date
Last prominently documented in 2020–2021. Only trains your own voice — not colleagues or guests. No group enrollment flow. Every participant other than the account holder still hits the cold-start problem.

### Finding 5 — Passive enrollment exists but is framed as a bug, not a feature
Post-meeting tagging builds voice profiles that auto-apply to future meetings. Otter calls it "Otter learns over time." It is never marketed as passive enrollment. Tag-early propagation — the fastest path to a clean transcript — is never explained.

### Finding 6 — Otter is allegedly building voiceprints from all participants without consent
August 2025 federal class action (NDCA) alleges Otter silently captures biometric voiceprints from all meeting participants — including non-users — stores them indefinitely, and uses them for model training without consent. The technical capability is real. The consent layer is not.

### Finding 7 — Crosstalk has no solution — passive calibration from meeting chatter could fix it *(research proposal)*
Otter's own docs advise users to "avoid overlapping dialogue." Accuracy drops to 70–75% in crosstalk conditions. A passive 60-second calibration window at meeting open — using natural greeting chatter — could build overlap-robust embeddings and reduce DER from ~25–30% toward 10–12%.

### Finding 8 — Jargon fix exists but is buried in settings
Custom vocabulary produces 10–15% accuracy improvement. Not in onboarding. Not prompted when jargon is detected. Requires manual discovery.

---

## What Otter Could Ship

**Sprint-sized:**
1. Resurface My Voiceprint in onboarding and before first meetings
2. Pre-meeting group enrollment link — 60-second voice sample for all calendar participants
3. Tag-early education — surface propagation behavior at the moment a Speaker N label appears
4. Domain vocabulary onboarding — industry detection at signup
5. Smart post-meeting cleanup — show only speaker change moments, not full transcript

**Quarter-sized:**
6. Passive calibration window — first 60 seconds of meeting chatter builds crosstalk-robust embeddings
7. Extended metadata integration — match Zoom reliability for Teams and Meet

**Legal priority:**
8. Explicit voiceprint consent layer — surface what biometric data is collected, for whom, with opt-in/opt-out

---

## What's Next

Controlled experiments measuring accuracy and cleanup time across three workflow conditions — naive vs tag-early vs full workflow. Scorer and parser tools coming to this repo.

---

Built by [Sanmati Sawalwade](https://linkedin.com/in/sanmati-sawalwade) — MS Information Systems, Northeastern University Silicon Valley
sawalwade.s@northeastern.edu | [sanmati1997.github.io](https://sanmati1997.github.io)
Also see: [Meshy Prompt Optimizer](https://github.com/sanmati1997/meshy-prompt-optimizer)
