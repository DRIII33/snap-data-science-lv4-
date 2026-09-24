# Snap Growth Analytics Portfolio Project Blueprint

**Project title:** Measuring a Synthetic Snapchat Growth Experiment: Activation, Retention, and Subscription Conversion

**Repository:** `DRIII33/snap-data-science-lv4-`

**Status:** Portfolio design and executable implementation specification. Statistical results are **EXECUTION-DEPENDENT RESULT — MUST BE GENERATED AFTER RUNNING THE PROVIDED CODE**.

> **Project disclaimer:** This is a portfolio project. It is not an official Snap Inc. project, does not use confidential Snap data, and does not claim access to Snap systems, models, metrics, employees, or processes. All generated records are **SYNTHETIC DATA**. Any simulated treatment effect is disclosed as a data-generating assumption. No Snap endorsement is implied.

## 1. Executive Project Overview

This project simulates a product-growth analytics engagement for a hypothetical Snapchat product team. The team wants to know whether a redesigned onboarding and feature-discovery experience improves early activation, day-28 retention, and premium-subscription conversion without harming guardrail metrics.

The project demonstrates the capabilities requested in the Data Scientist, Level 4 job description: SQL and Python analysis, product metrics, data mining, statistical modeling, A/B testing, causal reasoning, dashboards, cross-functional communication, scalable data preparation, data-quality validation, and responsible AI-tool use. It deliberately does **not** claim to demonstrate Snap's internal technology stack or business results.

**Primary decision:** Should the hypothetical product team expand the treatment experience beyond the experiment population?

**Primary estimand:** Intention-to-treat difference in day-28 retention between randomized treatment and control users.

**Secondary estimands:** Activation, subscription conversion, engagement, and guardrail differences.

**Success evidence:** A reproducible data pipeline, validated analytical dataset, pre-specified methodology, confidence intervals and effect sizes, an executive dashboard, and recommendations tied only to executed results.

## 2. Job Description Alignment

| Job-description requirement | Portfolio component | Evidence produced | Tool | Deliverable | Status |
|---|---|---|---|---|---|
| Quantitative analysis and data mining | Cohort, funnel, retention, and experiment analysis | Reproducible metrics and statistical outputs | BigQuery, Python | `sql/06_analysis_views.sql`, notebook | Explicitly demonstrated |
| Statistical modeling | Difference-in-means and regression-adjusted sensitivity analysis | Estimates, CI, diagnostics | Python/statsmodels | `notebooks/03_statistical_analysis.ipynb` | Explicitly demonstrated |
| Core product metrics | Activation, D28 retention, subscription conversion, sessions | Metric definitions and views | BigQuery | `docs/data_dictionary.md` | Explicitly demonstrated |
| A/B testing | Randomized treatment and control assignment | ITT estimate, balance checks, guardrails | Python | Statistical notebook | Explicitly demonstrated |
| Causal methods | Randomized experiment; optional CUPED sensitivity | Treatment, unit, estimand, assumptions | Python | `docs/statistical_methodology.md` | Explicitly demonstrated |
| SQL/big-data querying | Raw-to-analytical transformations | BigQuery-compatible scripts | BigQuery SQL | `sql/` | Explicitly demonstrated |
| Python or R | Generation, validation, analysis | Executable Python | Colab/Python | `src/`, notebooks | Explicitly demonstrated |
| Visuals, dashboards, reports | Looker Studio specification and views | KPI design and wireframes | Looker Studio | `dashboards/` | Explicitly demonstrated |
| Cross-functional collaboration | Stakeholder/RACI and decision memo | Product-facing operating model | Markdown | `docs/stakeholder_operating_model.md` | Supporting evidence |
| Independent project execution | End-to-end dependency plan | Complete reproducibility instructions | Markdown | `README.md` | Supporting evidence |
| Product sense / Snapchat understanding | Snapchat-relevant but clearly hypothetical scenario | Product funnel rationale | Markdown | `docs/business_problem.md` | Supporting evidence |
| AI-tool use with statistical integrity | AI-use protocol and human review checklist | Prompt/output validation record | Markdown | `docs/ai_use_protocol.md` | Supporting evidence |
| Machine learning | Not required for the causal question | No unnecessary model | N/A | `docs/statistical_methodology.md` | Not demonstrated; intentionally excluded |
| Snap internal systems/data | Not available | Explicit limitation | N/A | `Project_Disclaimer.md` | Not demonstrated |

## 3. Business Scenario

**Who:** Hypothetical Snapchat Product Growth, Product Analytics, and Engineering stakeholders. The scenario is inferred from the job description's explicit collaboration with product managers, engineers, product marketers, and designers; it is not a claim about Snap's actual team structure.

**What:** A redesigned onboarding and feature-discovery flow is randomly assigned to eligible new users. The product team needs evidence about activation, retention, premium conversion, and user-experience guardrails.

**Why:** A higher early-value experience could improve durable engagement and monetization, but optimizing one short-term metric could reduce quality or create misleading gains. A Level 4 data scientist would define metrics, validate data, analyze the experiment, and convert results into a launch recommendation.

**Where:** Hypothetical Snapchat mobile onboarding and early product-discovery funnel.

**When:** Configurable synthetic observation window; default 90 days beginning `2026-01-01`.

**Business outcome:** Make a launch/iterate/stop decision using retention and activation as primary outcomes, subscription conversion as a secondary outcome, and notification opt-outs, reports, and session-quality proxies as guardrails.

## 4. Business Problem and Analytical Questions

**Primary problem:** Determine whether the hypothetical onboarding treatment causally improves durable user value enough to justify expansion.

**Secondary problems:**
1. Early activation may not translate into durable retention.
2. Subscription conversion may differ by treatment while being underpowered.
3. Aggregate results may hide heterogeneous effects by market, device, or acquisition channel.
4. Event data may contain duplicates, missingness, impossible timestamps, and leakage risks.
5. A dashboard could make an invalid experiment appear decision-ready.

**Questions:**
1. Does treatment change activation within seven days?
2. Does treatment change day-28 retention?
3. Does treatment change subscription conversion within 28 days?
4. Does treatment change sessions, messages, or AR-feature discovery?
5. Are guardrails materially worse?
6. Are effects consistent across pre-treatment segments?
7. Are the conclusions sensitive to covariate adjustment and missing-data handling?
8. What data-quality or measurement issues limit the decision?

## 5. Hypotheses and Estimands

| ID | Null | Alternative | Metric/population | Unit | Method | Alpha/effect/CI | Interpretation |
|---|---|---|---|---|---|---|---|
| H1 | Treatment and control have equal D28 retention | Treatment changes D28 retention | Randomized eligible new users | User | Difference in proportions; logistic regression sensitivity | Two-sided alpha .05; risk difference and ratio; bootstrap or Wilson CI | Expansion requires positive practical effect and no material guardrail harm |
| H2 | Equal seven-day activation | Treatment changes activation | Same | User | Difference in proportions | Alpha .05; risk difference and CI | Secondary evidence of early product value |
| H3 | Equal 28-day subscription conversion | Treatment changes conversion | Same | User | Difference in proportions; Fisher/exact sensitivity for sparse cells | Alpha .05; risk difference and CI | Do not claim revenue impact without price/eligibility data |
| H4 | Equal notification opt-out/report guardrails | Treatment changes guardrails | Same | User | Difference in proportions | Alpha .05; CI; practical threshold pre-specified | Any harmful direction triggers investigation |

**Practical thresholds (ASSUMPTION):** Define before execution, for example: at least +1 percentage point D28 retention, no guardrail decline worse than -0.5 points, and a confidence interval that is decision-compatible. These thresholds are not Snap standards.

## 6. Data Strategy and Synthetic Data-Generating Process

Synthetic data is selected because internal Snapchat event data is unavailable, privacy-sensitive, and not reproducible by a portfolio reviewer. No public dataset is required because a public dataset would not provide randomized onboarding exposure, user-level event history, and subscription outcomes in one coherent structure.

### Entities and grains

- `users`: one row per synthetic user; primary key `user_id`.
- `experiment_assignments`: one row per user assignment; `user_id` foreign key.
- `events`: one row per product event; unique `event_id`; foreign key `user_id`.
- `subscriptions`: zero or one row per user for the simulated observation period.
- `daily_user_features`: one row per user-day, generated after event aggregation.

### Simulated relationships

The generator creates plausible associations among acquisition channel, market, device, latent propensity, treatment, activation, retention, engagement, and subscription. Treatment is assigned by a deterministic seeded randomization independent of pre-treatment variables. The generator may include a documented treatment effect for pipeline validation, but the expected recovered effect is not reported until code is run.

**Known limitation:** Because the data-generating process is simulated, recovery of an embedded effect validates implementation rather than proving a real product effect.

### Missingness, noise, and outliers

- Small configurable missingness in optional device/channel fields.
- Duplicate-event injection is optional for validation testing and must be removed or flagged.
- Heavy-tailed session/message counts.
- Timestamp boundary cases.
- No outcome is constructed from post-treatment variables used as predictors.

## 7. BigQuery Architecture

**Project ID:** `driiiportfolio`  
**Datasets:** `snap_growth_raw`, `snap_growth_transform`, `snap_growth_analytics`, `snap_growth_dashboard`

| Dataset | Table/view | Grain | Key columns | Partition/cluster |
|---|---|---|---|---|
| raw | `users` | user | `user_id` | cluster `market, device_type` |
| raw | `experiment_assignments` | user assignment | `user_id` | cluster `treatment_group` |
| raw | `events` | event | `event_id` | partition `event_date`; cluster `user_id, event_name` |
| raw | `subscriptions` | user subscription | `user_id` | partition `subscription_date` |
| transform | `clean_events` | valid event | `event_id` | partition `event_date`; cluster `user_id, event_name` |
| analytics | `user_experiment_metrics` | user | `user_id` | cluster `treatment_group, market` |
| analytics | `experiment_results` | metric/segment | `metric_name, segment_name, segment_value` | none |
| dashboard | `kpi_daily` | date/treatment | `metric_date, treatment_group` | partition `metric_date` |
| dashboard | `executive_summary` | one result/metric | `metric_name` | none |
| dashboard | `data_quality_summary` | check | `check_name` | none |

**Expected default size (ASSUMPTION):** 50,000 users and approximately 1–3 million events, configurable downward for Colab. Exact counts are execution-dependent.

### Schema summary

| Table | Column | Type | Description | Key | Nullable | Source |
|---|---|---|---|---|---|---|
| users | user_id | STRING | Synthetic user ID | PK | no | generator |
| users | signup_date | DATE | Eligibility date |  | no | generator |
| users | market | STRING | Synthetic market group |  | no | generator |
| users | device_type | STRING | Device category |  | no | generator |
| users | acquisition_channel | STRING | Acquisition source |  | yes | generator |
| experiment_assignments | user_id | STRING | Assigned user | PK/FK | no | generator |
| experiment_assignments | treatment_group | STRING | control/treatment |  | no | generator |
| experiment_assignments | assignment_ts | TIMESTAMP | Assignment time |  | no | generator |
| events | event_id | STRING | Event ID | PK | no | generator |
| events | user_id | STRING | Event owner | FK | no | generator |
| events | event_ts | TIMESTAMP | Event timestamp |  | no | generator |
| events | event_name | STRING | Event type |  | no | generator |
| events | session_id | STRING | Session identifier |  | yes | generator |
| subscriptions | user_id | STRING | Subscriber | PK/FK | no | generator |
| subscriptions | subscription_date | DATE | Conversion date |  | no | generator |
| subscriptions | plan | STRING | Synthetic plan |  | no | generator |

## 8. Repository Design

**Recommended repository name:** `snap-growth-experiment-analytics`  
**Description:** `Synthetic end-to-end product-growth experiment analytics project aligned to Snap Data Scientist Level 4 skills.`

```text
snap-growth-experiment-analytics/
├── README.md
├── Executive_Summary.md
├── Dashboard_Executive_Summary.md
├── Project_Disclaimer.md
├── LICENSE
├── .gitignore
├── requirements.txt
├── docs/
│   ├── business_problem.md
│   ├── data_dictionary.md
│   ├── data_architecture.md
│   ├── data_flow.md
│   ├── job_description_alignment.md
│   ├── statistical_methodology.md
│   ├── stakeholder_operating_model.md
│   ├── ai_use_protocol.md
│   └── limitations.md
├── data/README.md
├── sql/
│   ├── 01_create_datasets.sql
│   ├── 02_create_raw_tables.sql
│   ├── 03_data_quality_checks.sql
│   ├── 04_transform.sql
│   ├── 05_feature_engineering.sql
│   ├── 06_analysis_views.sql
│   ├── 07_dashboard_views.sql
│   └── 08_final_validation.sql
├── notebooks/
│   ├── 01_data_generation.ipynb
│   ├── 02_data_validation.ipynb
│   └── 03_statistical_analysis.ipynb
├── src/
│   ├── data_generation/generate_synthetic_data.py
│   ├── validation/validate_data.py
│   └── analysis/experiment_analysis.py
├── dashboards/
│   ├── README.md
│   └── dashboard_specification.md
├── outputs/
│   ├── figures/.gitkeep
│   └── reports/.gitkeep
└── tests/data_quality_tests.md
```

## 9. Reproducible Python Generator

Save the following as `src/data_generation/generate_synthetic_data.py`. It is intentionally modest enough for Colab free resources; increase configuration only after profiling.

```python
from pathlib import Path
import numpy as np
import pandas as pd

SEED = 20260922
N_USERS = 50_000
START = pd.Timestamp("2026-01-01", tz="UTC")
OUT = Path("data/synthetic")
rng = np.random.default_rng(SEED)
OUT.mkdir(parents=True, exist_ok=True)

markets = np.array(["north_america", "europe", "rest_of_world"])
devices = np.array(["ios", "android", "web"])
channels = np.array(["organic", "paid_social", "referral", "search"])
users = pd.DataFrame({
    "user_id": [f"u_{i:07d}" for i in range(N_USERS)],
    "signup_date": (START + pd.to_timedelta(rng.integers(0, 60, N_USERS), unit="D")).date,
    "market": rng.choice(markets, N_USERS, p=[.35, .30, .35]),
    "device_type": rng.choice(devices, N_USERS, p=[.48, .48, .04]),
    "acquisition_channel": rng.choice(channels, N_USERS, p=[.55, .20, .15, .10]),
    "latent_propensity": np.clip(rng.normal(0, 1, N_USERS), -3, 3)
})

assign = pd.DataFrame({
    "user_id": users.user_id,
    "treatment_group": rng.choice(["control", "treatment"], N_USERS),
    "assignment_ts": pd.to_datetime(users.signup_date, utc=True) + pd.to_timedelta(rng.integers(0, 86_400, N_USERS), unit="s")
})

# SIMULATED DATA-GENERATING ASSUMPTION: treatment modestly increases activation.
base_activation = 1 / (1 + np.exp(-(0.2 + .55 * users.latent_propensity)))
treatment_lift = np.where(assign.treatment_group.eq("treatment"), 0.08, 0.0)
activated = rng.random(N_USERS) < np.clip(base_activation + treatment_lift, .01, .99)

n_events = int(N_USERS * 28)
user_idx = rng.integers(0, N_USERS, n_events)
events = pd.DataFrame({
    "event_id": [f"e_{i:09d}" for i in range(n_events)],
    "user_id": users.user_id.to_numpy()[user_idx],
    "event_ts": START + pd.to_timedelta(rng.integers(0, 90 * 86_400, n_events), unit="s"),
    "event_name": rng.choice(["app_open", "message_sent", "story_view", "lens_used", "feature_discovered"], n_events, p=[.40, .18, .22, .12, .08]),
    "session_id": [f"s_{i:010d}" for i in range(n_events)]
})

# Ensure activated users have at least one discovery event; this is simulated product logic.
activated_ids = users.loc[activated, "user_id"].to_numpy()
extra = pd.DataFrame({
    "event_id": [f"e_extra_{i:08d}" for i in range(len(activated_ids))],
    "user_id": activated_ids,
    "event_ts": START + pd.to_timedelta(rng.integers(0, 7 * 86_400, len(activated_ids)), unit="s"),
    "event_name": "feature_discovered",
    "session_id": [f"s_extra_{i:08d}" for i in range(len(activated_ids))]
})
events = pd.concat([events, extra], ignore_index=True)

# Retention is simulated from activation and latent propensity, not calculated from post-treatment events.
user_frame = users.merge(assign, on="user_id")
retention_p = 1 / (1 + np.exp(-(-1.0 + .9 * user_frame.latent_propensity + .9 * activated + .10 * user_frame.treatment_group.eq("treatment"))))
retained = rng.random(N_USERS) < retention_p
subscription_p = 1 / (1 + np.exp(-(-3.2 + .5 * user_frame.latent_propensity + .25 * activated + .08 * user_frame.treatment_group.eq("treatment"))))
subscriber = rng.random(N_USERS) < subscription_p
subscriptions = user_frame.loc[subscriber, ["user_id"]].copy()
subscriptions["subscription_date"] = pd.to_datetime(user_frame.loc[subscriber, "signup_date"], utc=True) + pd.to_timedelta(rng.integers(1, 29, len(subscriptions)), unit="D")
subscriptions["plan"] = rng.choice(["plus", "lens_plus"], len(subscriptions), p=[.75, .25])

# Persist latent labels only for validation/reproducibility; exclude from analytical features.
users["simulated_activation_label"] = activated
users["simulated_d28_retained_label"] = retained

for name, frame in [("users", users), ("experiment_assignments", assign), ("events", events), ("subscriptions", subscriptions)]:
    frame.to_csv(OUT / f"{name}.csv", index=False)

assert users.user_id.is_unique
assert assign.user_id.is_unique
assert events.event_id.is_unique
assert set(assign.user_id).issubset(set(users.user_id))
assert set(events.user_id).issubset(set(users.user_id))
assert set(subscriptions.user_id).issubset(set(users.user_id))
assert set(assign.treatment_group).issubset({"control", "treatment"})
assert events.event_ts.notna().all()
print({"users": len(users), "assignments": len(assign), "events": len(events), "subscriptions": len(subscriptions)})
print(users.isna().sum())
```

**Expected resource profile:** execution-dependent; the default is designed to fit ordinary Colab memory more comfortably than a massive event simulation. Measure actual RAM, runtime, and CSV sizes after execution; do not claim them in advance.

## 10. Data Validation Framework

Required checks: completeness, uniqueness, referential integrity, allowed categories, date bounds, duplicate events, event-to-user joins, treatment balance, leakage, outliers, and distribution anomalies.

Example Python checks:

```python
def quality_report(users, assign, events, subscriptions):
    checks = []
    def add(name, expected, actual, status, remediation="None"):
        checks.append({"check": name, "expected": expected, "actual": actual, "status": status, "remediation": remediation})
    add("user_pk_unique", "0 duplicates", int(users.user_id.duplicated().sum()), "PASS" if users.user_id.is_unique else "FAIL")
    add("assignment_fk", "all users exist", int((~assign.user_id.isin(users.user_id)).sum()), "PASS" if assign.user_id.isin(users.user_id).all() else "FAIL")
    add("event_fk", "all users exist", int((~events.user_id.isin(users.user_id)).sum()), "PASS" if events.user_id.isin(users.user_id).all() else "FAIL")
    add("event_pk_unique", "0 duplicates", int(events.event_id.duplicated().sum()), "PASS" if events.event_id.is_unique else "FAIL")
    add("allowed_treatment", "control/treatment", sorted(assign.treatment_group.unique().tolist()), "PASS" if set(assign.treatment_group) <= {"control", "treatment"} else "FAIL")
    add("null_user_ids", "0", int(users.user_id.isna().sum()), "PASS" if users.user_id.notna().all() else "FAIL")
    return pd.DataFrame(checks)
```

**Data Quality Report:** The `actual` and `status` fields must be populated by execution. Do not write “clean” before running these checks. Expected status is `PASS` for intentionally valid generated data; injected defects must produce `FAIL` and be documented as remediation tests.

## 11. BigQuery SQL Plan

Use explicit schemas rather than relying only on autodetection. CSV loading is supported through the BigQuery console, `bq`, or client libraries; see [Google's dataset documentation](https://docs.cloud.google.com/bigquery/docs/datasets) and [CSV loading documentation](https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-csv).

### `sql/01_create_datasets.sql`

```sql
CREATE SCHEMA IF NOT EXISTS `driiiportfolio.snap_growth_raw` OPTIONS(location='US');
CREATE SCHEMA IF NOT EXISTS `driiiportfolio.snap_growth_transform` OPTIONS(location='US');
CREATE SCHEMA IF NOT EXISTS `driiiportfolio.snap_growth_analytics` OPTIONS(location='US');
CREATE SCHEMA IF NOT EXISTS `driiiportfolio.snap_growth_dashboard` OPTIONS(location='US');
```

### `sql/02_create_raw_tables.sql`

Create raw tables with the schema in Section 7. Partition `events` by `DATE(event_ts)` and cluster by `user_id, event_name`. For reproducibility, the repository should include the exact `CREATE TABLE` statements generated from the loaded CSV schema; never use `SELECT *` in analytical SQL.

### `sql/03_data_quality_checks.sql`

```sql
SELECT 'duplicate_event_id' AS check_name, COUNT(*) AS failures
FROM (
  SELECT event_id FROM `driiiportfolio.snap_growth_raw.events`
  GROUP BY event_id HAVING COUNT(*) > 1
)
UNION ALL
SELECT 'orphan_event_user', COUNT(*)
FROM `driiiportfolio.snap_growth_raw.events` e
LEFT JOIN `driiiportfolio.snap_growth_raw.users` u USING (user_id)
WHERE u.user_id IS NULL
UNION ALL
SELECT 'invalid_treatment', COUNT(*)
FROM `driiiportfolio.snap_growth_raw.experiment_assignments`
WHERE treatment_group NOT IN ('control', 'treatment');
```

### `sql/04_transform.sql`

```sql
CREATE OR REPLACE TABLE `driiiportfolio.snap_growth_transform.clean_events`
PARTITION BY event_date CLUSTER BY user_id, event_name AS
SELECT DISTINCT
  event_id, user_id, DATE(event_ts) AS event_date, event_ts,
  LOWER(TRIM(event_name)) AS event_name, session_id
FROM `driiiportfolio.snap_growth_raw.events`
WHERE event_id IS NOT NULL AND user_id IS NOT NULL
  AND event_ts IS NOT NULL
  AND event_name IN ('app_open','message_sent','story_view','lens_used','feature_discovered');
```

### `sql/05_feature_engineering.sql`

```sql
CREATE OR REPLACE TABLE `driiiportfolio.snap_growth_analytics.user_experiment_metrics`
CLUSTER BY treatment_group, market AS
WITH base AS (
  SELECT u.user_id, u.signup_date, u.market, u.device_type,
         u.acquisition_channel, a.treatment_group, a.assignment_ts
  FROM `driiiportfolio.snap_growth_raw.users` u
  JOIN `driiiportfolio.snap_growth_raw.experiment_assignments` a USING (user_id)
), agg AS (
  SELECT b.user_id,
    COUNTIF(e.event_name = 'app_open' AND e.event_date BETWEEN b.signup_date AND DATE_ADD(b.signup_date, INTERVAL 6 DAY)) > 0 AS activated,
    COUNTIF(e.event_date BETWEEN b.signup_date AND DATE_ADD(b.signup_date, INTERVAL 27 DAY)) > 0 AS d28_retained,
    COUNTIF(e.event_name = 'feature_discovered' AND e.event_date BETWEEN b.signup_date AND DATE_ADD(b.signup_date, INTERVAL 6 DAY)) > 0 AS discovered_feature,
    COUNTIF(e.event_name = 'message_sent' AND e.event_date BETWEEN b.signup_date AND DATE_ADD(b.signup_date, INTERVAL 27 DAY)) AS messages_28d,
    COUNTIF(e.event_name = 'app_open' AND e.event_date BETWEEN b.signup_date AND DATE_ADD(b.signup_date, INTERVAL 27 DAY)) AS opens_28d
  FROM base b LEFT JOIN `driiiportfolio.snap_growth_transform.clean_events` e USING (user_id)
  GROUP BY b.user_id
)
SELECT b.*, a.* EXCEPT(user_id),
  EXISTS(SELECT 1 FROM `driiiportfolio.snap_growth_raw.subscriptions` s
         WHERE s.user_id=b.user_id AND s.subscription_date BETWEEN b.signup_date AND DATE_ADD(b.signup_date, INTERVAL 27 DAY)) AS subscribed_28d
FROM base b JOIN agg a USING (user_id);
```

### `sql/06_analysis_views.sql`

Create a view grouped by treatment and optional pre-treatment segments containing users, activation rate, D28 retention rate, subscription conversion, means, and guardrails. Use denominators based on users, not events.

### `sql/07_dashboard_views.sql`

Create:
- `kpi_daily`: daily eligible-user counts and treatment rates.
- `executive_summary`: treatment/control metric estimates and execution-populated CI/p-values.
- `data_quality_summary`: check name, expected, actual, status, remediation.

### `sql/08_final_validation.sql`

Validate one row per user in `user_experiment_metrics`, no orphan keys, no post-treatment feature in pre-treatment adjustment set, and no join multiplication. Any failed check blocks publication.

## 12. Statistical Methodology

The primary analysis is an intention-to-treat randomized comparison because treatment assignment is the causal intervention. The primary result should be a risk difference with a 95% confidence interval. A logistic regression may be used as a pre-specified sensitivity analysis with only pre-treatment covariates. Bootstrap intervals may be used for skewed count outcomes.

**Why not automatically use ML?** The core decision is causal and the synthetic sample is structured for interpretable experiment measurement. A predictive model is not necessary. Adding ML would risk distracting from the business question and introducing leakage. A future extension could predict subscription propensity only if a separate decision requires targeting and if temporal validation is implemented.

**Assumptions/diagnostics:** randomization, assignment integrity, no material interference, correct outcome windows, independent user-level units, adequate sample size, no sample-ratio mismatch, pre-treatment covariate balance, and reliable event instrumentation. Inspect balance tables, treatment proportions, outcome counts, missingness, distributions, and sensitivity to regression adjustment.

**Multiple testing:** D28 retention is primary. Secondary metrics are labeled exploratory or adjusted using a documented method. Do not select the most favorable metric after execution.

## 13. Statistical Notebook Structure

`notebooks/03_statistical_analysis.ipynb` must contain:

1. `01_Project_Setup`: versions, seed, paths, alpha, practical thresholds.
2. `02_Load_Data`: load the analytical extract only.
3. `03_Data_Validation`: grain, assignment, missingness, duplicate and join checks.
4. `04_Exploratory_Data_Analysis`: cohort, treatment balance, distributions.
5. `05_Feature_Engineering`: pre-treatment features and outcomes; leakage review.
6. `06_Methodology`: estimand, hypotheses, test selection.
7. `07_Assumption_Checks`: balance, SRM, sample size, outcome windows.
8. `08_Statistical_Analysis`: ITT estimates, optional regression sensitivity.
9. `09_Effect_Size`: risk difference, relative risk, standardized count effects.
10. `10_Confidence_Intervals`: 95% intervals and practical thresholds.
11. `11_Sensitivity_Analysis`: regression adjustment, exclusions, missingness.
12. `12_Visualization`: confidence-interval plots, funnel/retention charts.
13. `13_Insights`: descriptive, diagnostic, statistical, business findings.
14. `14_Business_Recommendations`: only after results exist.
15. `15_Final_Validation`: checklist and export of result tables.

Every result cell must label numerical outputs **EXECUTION-DEPENDENT RESULT — MUST BE GENERATED AFTER RUNNING THE PROVIDED CODE** until the notebook has actually run.

## 14. Understanding the Data Flow: From Synthetic Data to Statistical Insights

**Synthetic/Public Source Data** → Python/Colab generates relational user, assignment, event, and subscription records.  
**Python / Google Colab** → deterministic generation and local validation.  
**CSV Files** → portable raw artifacts; not committed if large or containing generated data by default.  
**BigQuery Raw Layer** → explicit-schema ingestion and low-cost scalable storage.  
**Data Quality Validation** → key, category, timestamp, range, and referential checks.  
**BigQuery Transformation Layer** → standardization, deduplication, valid-event filtering.  
**Feature Engineering** → user-level pre-treatment covariates and fixed-window outcomes.  
**Analytical Dataset / Views** → one row per user for statistical analysis.  
**Google Colab Statistical Analysis** → experiment estimates, diagnostics, uncertainty, and sensitivity.  
**Statistical Results** → persisted CSV/Parquet/BigQuery result artifacts.  
**Business Insights** → evidence, interpretation, recommendation, limitation.  
**BigQuery Dashboard Views** → clean KPI and methodology views.  
**Looker Studio** → executive-facing charts and filters.  
**Executive Decision Support** → launch, iterate, or stop decision with documented uncertainty.

## 15. Looker Studio Dashboard Specification

**Dashboard title:** `Synthetic Snapchat Growth Experiment — Executive Decision Support`

### Page 1 — Executive Decision
- Audience: product and business leadership.
- Source: `executive_summary`.
- KPIs: eligible users, treatment share, activation, D28 retention, subscription conversion, guardrail status.
- Charts: KPI cards; treatment/control dot-and-interval chart; decision banner; methodology note.
- Filters: date/cohort, market, device, acquisition channel.
- Question: Is the treatment decision-ready?

### Page 2 — Funnel and Retention
- Source: `user_experiment_metrics` or an aggregated view.
- Charts: activation funnel, retention by treatment, cohort trend.
- Question: Where does treatment change user behavior?

### Page 3 — Segments and Guardrails
- Source: `segment_results` and `guardrail_results`.
- Charts: segment forest plot/table, opt-out/report rates, sample sizes.
- Question: Is the result consistent and safe across important pre-treatment groups?

### Page 4 — Data Quality and Methodology
- Source: `data_quality_summary` and `experiment_metadata`.
- Charts: pass/fail table, data freshness, metric definitions, experiment assumptions.
- Question: Can stakeholders trust the analysis?

**Wireframe:** header → decision banner → primary KPI cards → CI chart → funnel/retention visuals → segment and guardrail table → methodology and limitations panel.

### Component mapping

| Component | BigQuery view | Dimension | Metric | Calculation | Question |
|---|---|---|---|---|---|
| Retention card | `executive_summary` | treatment | D28 retention | retained/users | Did retention change? |
| Funnel | `funnel_summary` | treatment, stage | users | distinct users by stage | Where is lift? |
| Segment chart | `segment_results` | market/device/channel | risk difference, CI | treatment-control | Is effect heterogeneous? |
| Quality table | `data_quality_summary` | check | failures/status | validation output | Is data trustworthy? |

Use BigQuery views rather than raw tables. Document refresh policy, owner, source lineage, metric definitions, and limitations in the dashboard itself.

## 16. Reproduction Instructions

1. Confirm access to Google Cloud project `driiiportfolio` or create/use a permitted project; enable BigQuery.
2. Create datasets with `sql/01_create_datasets.sql` in a chosen location.
3. Open Colab, install pinned packages from `requirements.txt`, and run the generator.
4. Run Python validation and save the data-quality report.
5. Upload CSV files through the BigQuery console or Cloud Storage; specify schema and skip the header row. Follow [official CSV loading guidance](https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-csv).
6. Execute SQL scripts in order 02 through 08.
7. Export the analytical view to Colab or query it with the BigQuery client.
8. Run the statistical notebook from a fresh runtime.
9. Persist result tables and figures under `outputs/`.
10. Connect Looker Studio's native BigQuery connector to dashboard views.
11. Add dashboard notes for refresh, ownership, source lineage, and synthetic-data limitations.
12. Run the final QA checklist and reproduce from scratch.

**Dependencies:** Python 3.x, `numpy`, `pandas`, `scipy`, `statsmodels`, `matplotlib`, `seaborn`, `google-cloud-bigquery`, and `pyarrow` as needed. Pin tested versions after execution; do not claim a version has been tested until it has been run.

## 17. BigQuery and Colab Cost Controls

Current pricing, quotas, and free-tier terms can change. Verify before execution using official [BigQuery pricing](https://cloud.google.com/bigquery/pricing), [cost controls](https://docs.cloud.google.com/bigquery/docs/best-practices-costs), and [quotas](https://cloud.google.com/bigquery/quotas). Do not treat third-party summaries as authoritative.

Checklist:
- Use small synthetic data by default.
- Avoid `SELECT *`.
- Partition events and filter partition columns.
- Cluster by common join/filter fields.
- Use dry runs or query byte estimates before expensive queries.
- Set maximum bytes billed where appropriate.
- Prefer materialized analytical views/tables for repeated dashboard work.
- Retrieve only the user-level analytical subset into Colab.
- Delete or expire temporary tables.
- Monitor billing and quota dashboards.
- Do not assume free-tier amounts or Colab runtime limits; verify at execution time.

Colab's official FAQ states that resources and availability are dynamic and not guaranteed; this project intentionally avoids GPU dependence and large model training. [Colab FAQ](https://research.google.com/colaboratory/faq.html)

## 18. Insights, Recommendations, and Limitations

### Findings

Before execution: **EXPECTED OUTPUT — MUST BE GENERATED AFTER EXECUTION**. The repository must separate:
- Descriptive: what happened in the generated sample.
- Diagnostic: plausible mechanisms, labeled **INTERPRETATION**.
- Statistical: estimates, CI, p-values, and effect sizes from executed code.
- Business: decision implications, with assumptions.

### Recommendation template

| Evidence | Recommendation | Rationale | Expected impact | Measurement | Risk |
|---|---|---|---|---|---|
| EXECUTION-DEPENDENT RESULT | Expand, iterate, or stop | Tied to primary estimand and guardrails | Formula only; no invented dollars | Follow-up experiment/monitoring | Generalization, novelty, instrumentation |

### Limitations

- All user and event data are synthetic.
- Simulated treatment effects are not real Snap effects.
- The generator cannot reproduce Snap's user behavior, scale, privacy controls, economics, or infrastructure.
- Synthetic distributions and missingness assumptions may be wrong.
- Randomization removes confounding only in the simulated experiment; it does not establish external validity.
- The observation window may be too short for durable retention.
- No real ad revenue, pricing, costs, or lifetime value are included.
- Segment analysis can be underpowered and exploratory.
- Event definitions are portfolio abstractions.
- Dashboard results are illustrative until executed.

## 19. AI Use Protocol

AI may assist with drafting SQL, explaining errors, generating test cases, or suggesting visualizations. The analyst remains responsible for:

1. Reviewing every generated query.
2. Running key queries independently.
3. Checking join grain and denominator logic.
4. Verifying statistical formulas against authoritative references.
5. Preventing leakage and fabricated results.
6. Documenting material AI assistance without entering confidential data.

## 20. End-to-End Execution Order

| Step | Objective | Tool/output | Validation | Dependency/completion |
|---|---|---|---|---|
| 01 | Review job description | Requirements matrix | Every requirement classified | None; matrix complete |
| 02 | Define scenario | Business problem doc | Measurable decision exists | 01 |
| 03 | Define estimands | Hypothesis table | Primary metric pre-specified | 02 |
| 04 | Design schema | Architecture/data dictionary | Grain/keys documented | 03 |
| 05 | Generate data | CSVs | Seed, ranges, keys pass | 04 |
| 06 | Validate locally | Quality report | No unexplained failures | 05 |
| 07 | Create BigQuery resources | Datasets/tables | Correct location/schema | 06 |
| 08 | Load raw data | Raw tables | Row counts and schema | 07 |
| 09 | Run DQ SQL | Check results | Failures remediated | 08 |
| 10 | Transform | Clean events | No invalid events | 09 |
| 11 | Engineer features | User analytical table | One row/user, no leakage | 10 |
| 12 | Analyze | Statistical outputs | Assumptions/CI/effects | 11 |
| 13 | Sensitivity test | Robustness outputs | Differences explained | 12 |
| 14 | Create dashboard views | Clean views | Metric lineage documented | 12 |
| 15 | Build dashboard | Looker Studio report | Filters and sources work | 14 |
| 16 | Write findings | Reports | No fabricated numbers | 12,15 |
| 17 | Final QA | Checklist | All critical checks pass | 16 |
| 18 | Fresh reproduction | Re-run project | Independent reproduction succeeds | 17 |

## 21. Final QA Audit

- [ ] Scenario is explicitly hypothetical and aligned to the job description.
- [ ] No Snap confidential data or internal systems are implied.
- [ ] Synthetic data is labeled everywhere.
- [ ] Primary estimand and metric were defined before analysis.
- [ ] Every table has documented grain and keys.
- [ ] SQL is BigQuery-compatible and avoids unnecessary scans.
- [ ] Python has imports, seed, validation, and output paths.
- [ ] Data-quality checks include completeness, uniqueness, validity, consistency, timeliness, outliers, and leakage.
- [ ] Joins are tested for multiplication.
- [ ] Treatment assignment and sample-ratio checks are run.
- [ ] No post-treatment variables enter adjustment features.
- [ ] Confidence intervals, effect sizes, and practical thresholds are reported.
- [ ] Statistical and business significance are separated.
- [ ] No result is stated before execution.
- [ ] Dashboard uses curated views, not raw tables.
- [ ] Dashboard documents source, refresh, owner, definitions, and limitations.
- [ ] BigQuery pricing and quotas are verified from official documentation at execution time.
- [ ] Colab resources are not assumed to be guaranteed.
- [ ] Repository reproduces from a fresh environment.

## 22. Deliverable Manifest

| Deliverable | File/location | Purpose | Generated by | Status |
|---|---|---|---|---|
| Project blueprint | `docs/portfolio_project_blueprint.md` | Complete design and execution specification | Markdown | This file |
| README | `README.md` | Public project orientation and reproduction | Markdown | To create |
| Executive summary | `Executive_Summary.md` | C-suite narrative after execution | Markdown | Template required |
| Dashboard summary | `Dashboard_Executive_Summary.md` | Dashboard use and interpretation | Markdown | Template required |
| Disclaimer | `Project_Disclaimer.md` | Non-affiliation and synthetic-data disclosure | Markdown | Required |
| Business problem | `docs/business_problem.md` | Scenario and analytical questions | Markdown | Required |
| Data dictionary | `docs/data_dictionary.md` | Schemas, grains, keys, definitions | Markdown | Required |
| Architecture | `docs/data_architecture.md` | BigQuery layers and lineage | Markdown/SQL | Required |
| Data flow | `docs/data_flow.md` | End-to-end flow | Markdown | Required |
| Methodology | `docs/statistical_methodology.md` | Estimands, tests, assumptions | Markdown | Required |
| Alignment matrix | `docs/job_description_alignment.md` | Requirement-to-evidence mapping | Markdown | Required |
| Python generator | `src/data_generation/generate_synthetic_data.py` | Deterministic synthetic data | Python | Code included above |
| Python validation | `src/validation/validate_data.py` | Quality checks | Python | Required |
| SQL scripts | `sql/*.sql` | BigQuery ingestion/transformation/analysis | SQL | Plan and core code above |
| Colab notebooks | `notebooks/*.ipynb` | Generation, validation, analysis | Colab | Required |
| CSV files | `data/synthetic/*.csv` | Generated raw inputs | Python | Generated after execution; do not invent now |
| Analytical tables | `driiiportfolio.snap_growth_analytics.*` | User metrics and results | BigQuery SQL | Created after execution |
| Dashboard views | `driiiportfolio.snap_growth_dashboard.*` | Looker Studio sources | BigQuery SQL | Created after execution |
| Figures | `outputs/figures/` | Executed plots | Python | Generated after execution |
| Reports | `outputs/reports/` | DQ and statistical reports | Python/Markdown | Generated after execution |
| Looker Studio report | External report URL | Executive dashboard | Looker Studio | Build after views exist |

## Sources and verification notes

- Snap careers/job description: `https://careers.snap.com/jobs` and the source job-description file in this repository.
- Snap SEC filings: `https://investor.snap.com/financials/sec-filings/default.aspx` and `https://www.sec.gov/edgar/browse/?CIK=0001564408`.
- BigQuery datasets: `https://docs.cloud.google.com/bigquery/docs/datasets`.
- BigQuery CSV loading: `https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-csv`.
- BigQuery cost controls: `https://docs.cloud.google.com/bigquery/docs/best-practices-costs`.
- BigQuery quotas: `https://cloud.google.com/bigquery/quotas`.
- BigQuery pricing: `https://cloud.google.com/bigquery/pricing`.
- Google Colab FAQ: `https://research.google.com/colaboratory/faq.html`.
- Looker/BigQuery documentation: `https://docs.cloud.google.com/looker/docs/db-config-google-bigquery`.

Changing cloud prices, quotas, connector behavior, and runtime policies are **UNKNOWN — REQUIRES VALIDATION** at the time of execution. 
