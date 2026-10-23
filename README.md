# Awesome-ML-Model-Monitoring-Drift-Detection

# Top ML Model Monitoring & Drift Detection Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Production Drift Detection, Silent Failure Estimation & Alert Fatigue Prevention*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **ML Model Monitoring & Drift Detection**. These tools watch deployed models for data drift, performance degradation, and silent failures — catching the cases where your model keeps returning predictions but they've quietly stopped being right.

**Examples** include Evidently, NannyML, alibi-detect, whylogs, and the managed observability platforms (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, performance estimation without ground truth, and alerting that doesn't cry wolf — ideal for ML engineers who need visibility into production models without per-model SaaS pricing.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **Arize AI** — **The managed observability platform with ML and LLM tracing in one place.** **Auto Threshold options** determine alert bounds from historical data without manual tuning, and **API-Triggered Monitors** evaluate only when called (ideal for CI/CD or post-retraining checks) . **Data Fabric** syncs production traces to your warehouse in Iceberg format every 60 minutes . **Webhooks fire on status transitions** (`monitor.triggered`, `monitor.cleared`, `monitor.no_data`) with full payload details . **Downtime scheduling** silences monitors during known quiet periods . **Best for teams wanting managed monitoring** with broad LLM and ML coverage without operating infrastructure.

- **Fiddler AI** — **The explainability-first monitoring platform.** **Monitoring charts support up to 20 columns and 6 metric queries per chart** for model-to-model comparison . **Embedded root cause analytics** covers data drift, data integrity, and performance for binary, multiclass, and regression models . **Raw chart data exportable to CSV or Parquet** for further analysis . **Best for teams needing root-cause investigation** alongside drift alerts.

## Open-Source GitHub Projects

- **Evidently** — **The most complete open-source framework for ML and LLM evaluation and monitoring.** Apache 2.0 licensed. **100+ built-in metrics** spanning data drift, model quality, and LLM judges for RAG and generative tasks . **Reports** summarize evals and export to JSON, Python dict, HTML, or the monitoring UI; **Test Suites** add pass/fail conditions for CI/CD and regression testing . **Self-host the open-source monitoring dashboard** or use Evidently Cloud with a free tier for alerting and user management . **Works with tabular and text data** — not just classical ML, but also LLM output evaluation . **Best for teams wanting one library** covering both predictive ML and LLM-powered systems, with a self-hosted dashboard path.

- **NannyML** — **The silent-failure specialist that estimates performance without ground truth.** Apache 2.0 licensed. **CBPE (Confidence-Based Performance Estimation)** estimates classification metrics like ROC AUC when labels are delayed or absent; **DLE (Direct Loss Estimation)** does the same for regression . **PCA-based multivariate drift detection** monitors reconstruction error over time, while statistical tests handle univariate feature drift and model output drift . **Intelligent alerting** weeds out drift alerts that don't impact expected performance — directly combatting alert fatigue . **Ranker** prioritizes alerts by other criteria when needed . **Best for teams with delayed labels** — fraud, credit risk, or any domain where outcomes arrive weeks after predictions .

- **alibi-detect** — **The detection-focused library for outliers, adversarial inputs, and drift.** **Source-available** under Business Source License 1.1 (changed from Apache in v0.11.5) . **Supports tabular data, text, images, and time series** with both **TensorFlow and PyTorch backends** for drift detection . **Online and offline detectors** for production and batch use . **v0.13.0** added Python 3.12 support and numerical stability fixes for spectral residual and Mahalanobis detectors . **Note**: the BSL license means it is **not OSI-approved open source** — review terms before commercial deployment. **Best for teams needing detection primitives** to embed in custom monitoring pipelines, accepting the license change.

- **whylogs** — **The efficient, mergeable data profiling library.** Apache 2.0 licensed. **Generates compact statistical profiles** that capture distributions, missing values, and custom metrics — more faithful than sampling and far smaller than raw data . **Profiles are mergeable**, enabling distributed and streaming logging with aggregation across any time granularity . **Data constraints** validate that incoming data matches expectations, failing CI/CD pipelines when violated . **Profiles can be sent to WhyLabs** (managed platform with a free Starter tier) or analyzed locally . **Best for teams wanting lightweight data logging** that can run anywhere and merge across environments.

### Additional Strong Open-Source Options

- **argus-sdk** — Self-hosted LLM drift detection with **derived signals only** (output tokens, latency, finish reason — no prompt or completion text). **Welford's online algorithm** builds a baseline after 200 events; **Mann-Whitney U test with Bonferroni correction** runs every 60 seconds against the current window . **Hysteresis state machine** fires alerts at drift score 0.7 and clears at 0.4 for three consecutive windows — designed to prevent flapping . **MIT licensed**, single Go binary with SQLite and a Next.js dashboard . **Best for teams wanting private, lightweight LLM drift monitoring** without shipping prompt data to a vendor.

- **mcp-ml-monitor** — **MCP agent for ML monitoring** with **KS-Test, PSI, and Wasserstein** drift detection, performance tracking, and **LangFlow visual pipeline** integration . **Auto-remediation** includes Kubernetes rollback playbooks, GitHub issue creation, and Slack alerts . **Best for teams exploring agent-driven monitoring** with automated response workflows.

**Frameworks for building custom systems**: Combine **Evidently** for broad ML and LLM evaluation with a self-hosted dashboard, **NannyML** for performance estimation when labels are delayed and alert-fatigue-aware drift detection, **whylogs** for lightweight mergeable data profiling across environments, and **alibi-detect** for specialized outlier and adversarial detection — to build a monitoring stack tailored to your ground-truth availability, model types, and tolerance for operational overhead.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Model monitoring tools differ significantly in ground-truth requirements, metric coverage, and licensing. **NannyML is uniquely valuable when labels are delayed or absent** — CBPE and DLE estimate performance without waiting for outcomes, and its alerting explicitly filters drift that doesn't impact expected performance . **Evidently covers both classical ML and LLM evaluation** in one library with a self-hosted dashboard option . **alibi-detect's license changed from Apache to Business Source License 1.1 in v0.11.5** — it is source-available but not OSI-approved open source . **whylogs is a profiling library, not a monitoring platform** — it generates profiles that you analyze locally or ship to WhyLabs . **Drift detection is not the same as performance degradation** — NannyML's core insight is that many drift alerts don't affect model quality, and alerting on all of them causes fatigue .
- Self-hosted open-source solutions require proper baseline data collection, threshold tuning against historical behavior, and integration with your alerting stack (Slack, PagerDuty, or webhooks).

---

**Made for ML engineers monitoring production models where silent failures are the real risk.**
Let's make model monitoring more open, ground-truth-independent, and alert-fatigue-aware.
