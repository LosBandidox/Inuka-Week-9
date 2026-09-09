# Capstone Progress Check — Week 9 Update
**Project:** KPC Secure AI Tooling Pipeline | **Team:** Apex Innovators | **Domain E:** HSE, Compliance & Deployment Readiness

## 1. Which ML algorithm did you choose and why?

Two complementary models make up the predictive layer, not one:

- **Isolation Forest**, trained per cycle on pressure readings plus a local rolling-mean deviation feature, to flag statistically anomalous readings that are *still inside* the hard range gate (≤200 PSI). Isolation Forest was chosen because it's unsupervised — there's no labeled "this reading preceded a failure" dataset available from simulated SCADA streams, and Isolation Forest doesn't need one. It isolates anomalies by how few random splits it takes to separate a point from the rest of the data, which suits catching subtle drift that a fixed threshold would miss entirely.
- **A rolling OLS trend forecast**, fit alongside it to estimate how many readings remain until pressure is on track to breach the hard gate — not just whether a reading is unusual right now, but whether the trend is heading toward a real problem.

Together these form a genuinely two-layer alerting design: a reactive layer (hard thresholds on pass rate and suppression rate) and a predictive layer designed to fire *before* the reactive layer would.

## 2. How did you handle class imbalance (if applicable)?

Class imbalance in the traditional supervised-learning sense doesn't directly apply here, since anomaly detection with Isolation Forest is unsupervised — there's no labeled positive/negative class to balance in the first place. But the underlying problem it solves is conceptually the same one class-imbalance techniques address elsewhere: true anomalies are rare by definition. Isolation Forest handles this natively — it's specifically designed around the idea that anomalies are few and separable in fewer random splits than normal points, so it doesn't require oversampling, class weighting, or a labeled minority class to work. The `contamination` parameter effectively sets an expected anomaly rate rather than requiring balanced training data.

## 3. What is one insight from your Feature Importance analysis that surprised you?

Isolation Forest doesn't produce a classic feature-importance ranking the way a Random Forest classifier does, but the more interesting and genuinely surprising finding came from *combining* the anomaly detector with the trend forecaster: raw pressure alone, checked only against the hard 200 PSI gate, would only ever catch a problem after the fact. Adding local rolling-mean deviation as a second signal is what lets the system flag sensor drift *while pressure readings are still well inside the safe range* — the predictive layer's whole value comes from a feature that isn't the pressure value itself, but how much the recent local average has been quietly drifting. That reframed how we think about "the important feature" for this problem: it's not a single sensor reading, it's the *shape of recent history* around that reading — which is exactly the kind of signal a static threshold-based system could never catch.

