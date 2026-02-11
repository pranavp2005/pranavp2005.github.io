---
title: "Traffic Accident Detection & Tracking on Google Maps–Style Data"
order: 8
collection: portfolio
excerpt: "End-to-end incident detection from noisy user reports + GPS-derived travel times using hypothesis tests, SPRT, ARIMA forecasting, and changepoint detection."
teaser: projects/nanogpt-domain.pnge
header:
  teaser: projects/nanogpt-domain.png
---

Built a Google Maps traffic incident pipeline that (1) detects accidents from noisy crowdsourced reports, (2) tracks persistence via travel-time behavior, and (3) determines clearance when traffic returns to normal. Implemented and compared classical statistical testing, sequential decision-making, time-series forecasting, and changepoint methods in Python.

- GitHub: TODO (paste repo link)
- Demo: TODO (optional)

Notes
=====

What I built
------------
- **Log parsing + feature engineering:** Parsed car telemetry at Point A / Point B and joined it with accident report logs; computed per-car travel durations and aggregated signals into **10-minute intervals**.
- **Accident detection (reports):** Implemented **binomial hypothesis testing** per interval (H₀: baseline report rate ≈ 1%) and visualized detected windows.
- **Accident detection (telemetry):** Implemented a **likelihood ratio test** on travel-time distributions to detect incident regimes even if reports are noisy or missing.
- **Persistence + clearance (online):**
  - **Sequential estimation:** Running mean vs **EMA** with different forgetting factors to balance responsiveness and stability.
  - **SPRT:** Sequential Probability Ratio Test with explicit error controls (α=β=0.05) to emit **“Accident detected”** and **“Cleared”** events.
- **Time-series forecasting:** Built rolling **AR / ARMA / ARIMA** forecasts over resampled 10-minute mean durations to anticipate expected traffic and highlight sustained deviations.
- **Changepoint detection:** Prepared **1037 travel-duration observations** and applied **CUSUM**, **Page–Hinkley** (online drift), and **PELT** (offline segmentation) to estimate incident start/clear boundaries.

Key takeaways
-------------
- Combining **noisy human reports** with **behavioral telemetry** yields more reliable incident detection than either source alone.
- **Sequential methods (EMA/SPRT/Page–Hinkley)** are well-suited for real-time monitoring; **offline methods (PELT)** provide cleaner retrospective boundaries.
- Thresholds (confidence levels, penalties, CUSUM h) directly trade off **false alarms vs missed incidents**, and should be tuned to the product’s risk tolerance.
