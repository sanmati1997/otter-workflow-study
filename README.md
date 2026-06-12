# Otter.ai Workflow Gap Study

> Otter markets 93–95% accuracy. Users report 60–85%. The gap isn't the model — it's the workflow nobody teaches.

**[Case Study](CASE_STUDY.md)** | Built by [Sanmati Sawalwade](https://linkedin.com/in/sanmati-sawalwade)

---

## The Finding

Otter's speaker identification quality is almost entirely determined by what the user does in the first 30 seconds of a meeting. Otter teaches none of it.

Three steps. ~8 minutes of setup. 15–25 minutes saved per meeting.

| Step | When | Time | Impact |
|---|---|---|---|
| Pre-register voice profiles | Before meeting | 2 min/person | Eliminates cold-start — no more Speaker 1, Speaker 2 |
| Tag first speaker label | First 30 seconds | 30 seconds | Propagates names throughout entire transcript |
| Add custom vocabulary | Before first domain meeting | 5 minutes | 10–15% accuracy improvement on technical terms |

---

## 6 Findings

### Finding 1 — Cold-start problem affects every first-time meeting
Otter cannot name any speaker it has never heard before. Every new participant, every external call, every interview — all default to Speaker N. Otter's onboarding never explains this.

### Finding 2 — Tagging within 30 seconds propagates through the entire transcript
Most users discover this feature only after spending 20+ minutes cleaning a transcript manually. Tag during the meeting → clean export. Tag after → line-by-line correction.

### Finding 3 — Fireflies beats Otter on diarization via metadata, not a better model
Fireflies achieves 7.2% DER vs Otter's 10.7% — a 33% relative improvement — by pulling participant names from Zoom/Meet/Teams metadata. Not a model quality gap. A metadata integration gap.

### Finding 4 — Bad diarization cascades into wrong summaries and wrong action item owners
```
Bad diarization → Scrambled summary → Wrong action item owners → Broken accountability
```
The fix is upstream — clean diarization produces clean summaries automatically.

### Finding 5 — Jargon fix exists but is buried
Custom vocabulary produces 10–15% accuracy improvement on domain-specific terms. Not mentioned in onboarding. Not prompted when jargon is detected. Requires manual discovery.

### Finding 6 — Otter's onboarding teaches Connect Calendar → Try OtterPilot → Upgrade
None of the three high-impact workflow steps surface in onboarding. All require users to discover them through Reddit, third-party reviews, or trial and error.

### Finding 7 — Voice change detection should trigger progressive speaker enrollment
Otter already detects speaker boundaries — the trigger exists in the pipeline. What is missing is a tiered real-time prompt: 20-second window for the first speaker at meeting open, 10-second non-blocking prompt for every new voice detected mid-meeting, and an always-clickable inline label for any missed tags. 30 seconds is too long mid-meeting — speaker turns last 5–10 seconds in fast conversations.

### Finding 8 — Overlap-aware calibration could predict speaker identity during crosstalk
A 10-second pre-meeting calibration phase — all speakers talk simultaneously — builds overlap-robust voice embeddings. When crosstalk happens during the meeting, the system uses those fingerprints to decompose mixed audio rather than dropping it. Based on published overlap-aware diarization benchmarks, DER in high-crosstalk conditions drops from ~25–30% toward 10–12%.

---

## What Otter Could Ship

**Sprint-sized — no model changes:**
1. **Pre-meeting participant prompt** — detect new participants from calendar invite, prompt voice profile setup
2. **Progressive enrollment trigger** — fire a tagging prompt at each speaker change boundary (Finding 7)
3. **Domain vocabulary onboarding** — ask industry at signup, pre-populate custom vocabulary

**Quarter-sized — model and pipeline changes:**
4. **Overlap-aware calibration phase** — 10-second pre-meeting overlap sample builds crosstalk-robust embeddings (Finding 8)
5. **Zoom/Meet/Teams metadata integration** — pull participant display names at meeting start, close the 33% DER gap vs Fireflies without model retraining (Finding 3)

---

## What's Next

Controlled experiments measuring accuracy and cleanup time across three workflow conditions — naive vs tag-early vs full workflow. Scorer and parser tools coming to this repo.

---

Built by [Sanmati Sawalwade](https://linkedin.com/in/sanmati-sawalwade) — MS Information Systems, Northeastern University Silicon Valley  
sawalwade.s@northeastern.edu | [sanmati1997.github.io](https://sanmati1997.github.io)  
Also see: [Meshy Prompt Optimizer](https://github.com/sanmati1997/meshy-prompt-optimizer)
