# Week 9 Video Walkthrough Script
**Target length:** ~3 minutes | **Format:** Screen-record your SHAP plots (Loom, OBS, Zoom local recording)

**Before recording:** run the SHAP cells in `week9_operational_ml.ipynb` locally (`pip install shap`), using **`case_idx = 321`** in the force-plot cell — this is a real test-set case the model correctly flagged as high-risk (99.7% predicted probability), identified in the notebook's Section 6.3. Have both the summary plot and that case's force plot on screen before you start talking.

---

## 0. Open (0:00–0:20) — face camera or title card

> "Hi, I'm David Kimathi. In this walkthrough I'm going to show you exactly how our equipment-failure model makes its decisions — not just what it predicts, but why, using SHAP, a tool that explains individual predictions in plain terms."

---

## 1. The summary plot (0:20–1:10) — screen-share the SHAP summary plot

> "This is the SHAP summary plot across our whole test set. Each dot is one shift the model evaluated. Two features dominate everything else: rolling mean throughput and today's raw throughput — together they account for over 90% of every decision this model makes. Everything else — temperature, voltage, which shift it is — barely moves the needle. That matches the built-in feature importance chart in the written report, which is a good sign: two independent methods agree on what actually drives this model."

---

## 2. The specific case (1:10–2:40) — screen-share the force plot for case_idx = 321

> "Now let's look at one real case the model flagged. [Pause on the force plot.] Here is a case the model flagged as High Risk — a 99.7% predicted probability of a missed-maintenance shift.
>
> You can see here that rolling mean throughput is the main driver — pushing hard toward 'Failing.' This machine's throughput has averaged around 636 barrels over its last several shifts, well below the roughly 1,020-barrel level a healthy machine runs at. That's not a one-off bad day; it's a sustained pattern, and that's exactly what this feature is built to catch.
>
> [Narrate whatever your actual force plot shows next — typically raw throughput on this same shift, which was similarly low, reinforcing the same signal.] The other features — temperature, voltage — are barely contributing here; you can see their bars are small. This is a case where the model isn't guessing based on many weak signals, it's responding to one strong, consistent one."

---

## 3. Close — confidence and transparency (2:40–3:00) — face camera

> "That's the model in action: transparent about what it's looking at, and honest about the fact that it's really only watching one thing closely — output over time. That's exactly why we're treating this as a tool that tells our team where to look first, not a replacement for a technician's judgment. Thanks for watching."

---

## Delivery notes

- **Tone:** confident, transparent, accessible — as the assignment asks. Avoid hedging language like "I think" or "maybe" when describing what the SHAP values show; state what the plot shows directly.
- **If your actual SHAP values differ from what's described here** (they should be close but not identical to the permutation-importance numbers used as placeholders), narrate what you actually see — don't force the script's exact wording. The structure (main driver → why it makes sense → secondary factors → close) is what matters.
- **Pacing:** section 2 is the heart of the assignment ("narrate a specific prediction") — don't rush it. If you're short on time, trim the opening to 10 seconds instead.
