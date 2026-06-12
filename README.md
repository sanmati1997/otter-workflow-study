# Otter.ai Workflow Gap Study

> Otter markets 93–95% accuracy. Users report 60–85%. The gap isn't the model — it's the workflow nobody teaches.

**[Case Study](CASE_STUDY.md)** | Built by [Sanmati Sawalwade](https://linkedin.com/in/sanmati-sawalwade)

---

## The Finding

Otter's speaker identification quality is almost entirely determined by what the user does in the first speaking turn of a meeting. Otter teaches none of it.

Three steps. ~8 minutes of setup. 15–25 minutes saved per meeting.

| Step | When | Time | Impact |
|---|---|---|---|
| Pre-register voice profiles | Before meeting | 2 min/person | Eliminates cold-start — no more Speaker 1, Speaker 2 |
| Tag first speaker label | First speaking turn | Under 30 seconds | Propagates names throughout entire transcript |
| Add custom vocabulary | Before first domain meeting | 5 minutes | 10–15% accuracy improvement on technical terms |

---

## 8 Findings — Ordered by Impact

### Finding 1 — Bad diarization cascades into wrong summaries and wrong action item owners
```
Bad diarization → Scrambled summary → Wrong action item owners → Broken accountability
```
The fix is upstream — clean diarization produces clean summaries automatically. The summary engine is not the problem.

### Finding 2 — Fireflies beats Otter via metadata, not a better model
Fireflies achieves 7.2% DER vs Otter's 10.7% — a 33% relative improvement — by pulling participant names from Zoom/Meet/Teams metadata. Not a model quality gap. A metadata integration gap Otter could close without retraining a single model.

### Finding 3 — Otter's onboarding teaches none of the three steps that work
Onboarding teaches: Connect Calendar → Try OtterPilot → Upgrade. All three high-impact workflow steps require users to discover them through Reddit, third-party reviews, or trial and error. This is the root cause of Findings 1, 4, and 5.

### Finding 4 — Cold-start problem affects every first-time meeting
Otter cannot name any speaker it has never heard before. Every new participant, every external call, every interview defaults to Speaker N. Pre-registering voice profiles eliminates this entirely — Otter never surfaces this workflow.

### Finding 5 — Tagging within the first speaking turn saves 15–25 minutes — Otter never teaches this
Tag a speaker during the meeting → Otter propagates the name throughout. Tag after → 15–30 minutes of line-by-line correction. The feature exists. The education doesn't.

### Finding 6 — Voice change detection should trigger progressive speaker enrollment *(proposed)*
Otter already detects speaker boundaries. Missing: a tiered real-time prompt — 20 seconds for the first speaker at meeting open, 10-second non-blocking prompt for every new voice mid-meeting, always-clickable inline label for missed tags. No model changes needed.

### Finding 7 — Overlap-aware calibration could predict speaker identity during crosstalk *(research proposal)*
A 10-second pre-meeting calibration phase — all speakers talk simultaneously — builds overlap-robust voice embeddings. DER in high-crosstalk conditions drops from ~25–30% toward 10–12% based on published overlap-aware diarization benchmarks.

### Finding 8 — Jargon fix exists but is buried in settings
Custom vocabulary produces 10–15% accuracy improvement on domain-specific terms. Not mentioned in onboarding. Not prompted when jargon is detected. Requires manual discovery in Settings.

---

## What Otter Could Ship

**Sprint-sized — no model changes:**
1. Pre-meeting participant prompt — detect new participants, prompt voice profile setup
2. Progressive enrollment trigger — tiered tagging prompt at each speaker change boundary
3. Domain vocabulary onboarding — ask industry at signup, pre-populate vocabulary

**Quarter-sized — model and pipeline changes:**
4. Overlap-aware calibration phase — 10-second pre-meeting overlap sample
5. Zoom/Meet/Teams metadata integration — close the 33% DER gap vs Fireflies

---

## What's Next

Controlled experiments measuring accuracy and cleanup time across three workflow conditions — naive vs tag-early vs full workflow. Scorer and parser tools coming to this repo.

---

Built by [Sanmati Sawalwade](https://linkedin.com/in/sanmati-sawalwade) — MS Information Systems, Northeastern University Silicon Valley
sawalwade.s@northeastern.edu | [sanmati1997.github.io](https://sanmati1997.github.io)
Also see: [Meshy Prompt Optimizer](https://github.com/sanmati1997/meshy-prompt-optimizer)
