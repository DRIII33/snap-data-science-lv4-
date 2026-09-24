# End-to-End Processing Manual
## Synthetic Snapchat Growth Experiment Analytics

**Repository:** `DRIII33/snap-data-science-lv4-`  
**Primary blueprint:** [`docs/portfolio_project_blueprint.md`](./portfolio_project_blueprint.md)  
**BigQuery project:** `driiiportfolio`  
**Dashboard:** `Synthetic Snapchat Growth Experiment — Executive Decision Support`  
**Last reviewed:** 2026-09-24

---

## 1. Purpose and Operating Rules

This manual converts the portfolio blueprint into an executable process. Follow it from business framing through data generation, BigQuery, statistical analysis, Looker Studio, documentation, and final quality assurance.

This is a **portfolio simulation**. It is not an official Snap Inc. project and does not use confidential Snap data. Every generated record is **SYNTHETIC DATA**. Any simulated treatment effect is a data-generating assumption, not an observed Snap result.

Use these labels throughout the project:

- **VERIFIED FACT:** Directly documented by the job description or an official technical source.
- **ASSUMPTION:** A deliberate project-design choice that is not known to be true of Snap.
- **SYNTHETIC DATA:** Generated portfolio records.
- **EXECUTION-DEPENDENT RESULT — MUST BE GENERATED AFTER RUNNING THE PROVIDED CODE:** Any count, p-value, confidence interval, effect size, chart result, or recommendation that depends on execution.
- **INTERPRETATION:** An inference from executed evidence, not a directly observed fact.
- **UNKNOWN — REQUIRES VALIDATION:** Information that cannot be established from the repository or authoritative documentation.

Do not publish numerical findings before executing the notebooks and validating the output.

---

## 2. Required Software and Access

### 2.1 Accounts and permissions

You need:

1. A GitHub account with write access to `DRIII33/snap-data-science-lv4-`.
2. A Google account for Google Colab and Looker Studio.
3. Access to Google Cloud project `driiiportfolio`, or permission to use another project if the specified project is unavailable.
4. BigQuery permissions sufficient to create datasets and tables, run queries, and connect Looker Studio.

If the project or permissions are unavailable, record **UNKNOWN — REQUIRES VALIDATION** in the run log rather than assuming access.

### 2.2 Local Python environment

The project can be run in Colab. A local environment is optional. Use Python 3.x and install:

```bash
pip install numpy pandas scipy statsmodels matplotlib seaborn pyarrow google-cloud-bigquery
```

Pin versions only after testing them. Record the actual versions in `outputs/reports/run_metadata.json`.

### 2.3 Source documentation

Verify changing product terms before execution using official documentation:

- [BigQuery datasets](https://docs.cloud.google.com/bigquery/docs/datasets)
- [BigQuery CSV loading](https://docs.cloud.google.com/bigquery/docs/loading-data-cloud-storage-csv)
- [BigQuery cost controls](https://docs.cloud.google.com/bigquery/docs/best-practices-costs)
- [BigQuery pricing](https://cloud.google.com/bigquery/pricing)
- [BigQuery quotas](https://cloud.google.com/bigquery/quotas)
- [Google Colab FAQ](https://research.google.com/colaboratory/faq.html)
- [Looker Studio documentation](https://docs.cloud.google.com/data-studio)
- [Looker Studio quick start](https://docs.cloud.google.com/data-studio/quick-start-guide)

Prices, quotas, free-tier terms, connector behavior, and runtime availability are changeable. Do not hard-code them into the project as permanent facts.

---

## 3. Repository Preparation

### Step 1 — Review the source materials

1. Open `docs/job_description.md`.
2. Open `docs/portfolio_project_blueprint.md`.
3. Confirm that the project remains a hypothetical Snapchat growth experiment.
4. Confirm that no Snap-internal data, systems, or results are claimed.
5. Create a working branch if your repository workflow requires one.

### Step 2 — Create the implementation structure

Use the structure specified by the blueprint:

```text
README.md
Executive_Summary.md
Dashboard_Executive_Summary.md
Project_Disclaimer.md
requirements.txt
docs/
sql/
notebooks/
src/data_generation/generate_synthetic_data.py
src/validation/validate_data.py
src/analysis/experiment_analysis.py
data/synthetic/
dashboards/
outputs/figures/
outputs/reports/
tests/
```

Do not add empty files merely to fill a tree. Every committed file must have a defined purpose.

### Step 3 — Establish a run log

Create `outputs/reports/run_metadata.json` after the first run. Record:

- Git commit SHA
- Execution timestamp and timezone
- Python version
- Package versions
- Random seed
- User/event configuration
- BigQuery project and dataset locations
- Query job IDs if available
- Dashboard data-refresh timestamp
- Validation status

Never include credentials or service-account keys in the repository.

---

## 4. Business Framing Before Coding

Complete this work before generating data.

### 4.1 Write the decision statement

Use this exact decision framing:

> Should the hypothetical onboarding and feature-discovery treatment be expanded, iterated, or stopped based on its effect on day-28 retention, activation, subscription conversion, and guardrail metrics?

### 4.2 Define the primary estimand

The primary estimand is the intention-to-treat difference in day-28 retention:

```text
Risk difference = retention_rate(treatment) - retention_rate(control)
```

Define the unit as one eligible randomized user. Do not use events as the denominator for user-level outcomes.

### 4.3 Freeze hypotheses before looking at results

Document:

- Primary metric: D28 retention.
- Secondary metrics: D7 activation and D28 subscription conversion.
- Guardrails: notification opt-out, report events, and other explicitly defined experience proxies.
- Two-sided alpha: 0.05, unless a different value is justified and documented.
- Practical thresholds: project assumptions, not Snap standards.
- Segment analyses: exploratory unless separately powered and pre-specified.

Commit the hypothesis document before running the final analysis. This prevents post-hoc metric selection.

---

## 5. Generate the Synthetic Data

### Step 1 — Open Colab

1. Open a new Google Colab notebook.
2. Select a standard CPU runtime; GPU is not required.
3. Clone or download the repository, or upload the generator file.
4. Run the dependency installation cell.
5. Set the random seed and configuration variables.

### Step 2 — Run the generator

Run `src/data_generation/generate_synthetic_data.py`, or copy its code into the generation notebook. The default configuration should create:

- `users.csv`
- `experiment_assignments.csv`
- `events.csv`
- `subscriptions.csv`

The generator must:

1. Use a deterministic seed.
2. Preserve primary and foreign keys.
3. Create treatment and control groups.
4. Create fixed observation windows.
5. Generate events with timestamps and event types.
6. Generate subscription records separately from event records.
7. Save all files under `data/synthetic/`.
8. Print row counts and null summaries.
9. Run uniqueness, range, category, timestamp, and referential-integrity assertions.

### Step 3 — Record generated-data metadata

Record actual:

- Number of users
- Number of assignments
- Number of events
- Number of subscriptions
- File sizes
- Date ranges
- Treatment/control counts
- Seed
- Runtime
- Memory observations if available

These are **EXECUTION-DEPENDENT RESULT — MUST BE GENERATED AFTER RUNNING THE PROVIDED CODE**.

### Step 4 — Inspect the generated files

For every CSV:

```python
import pandas as pd
from pathlib import Path

for path in Path("data/synthetic").glob("*.csv"):
    df = pd.read_csv(path)
    print(path.name, df.shape)
    display(df.head())
    display(df.isna().sum())
```

Check that IDs are strings, dates/timestamps parse correctly, categories match the data dictionary, and no generated file contains credentials or real personal data.

---

## 6. Run Local Data Validation

Run `src/validation/validate_data.py` or the validation notebook.

### 6.1 Required checks

The validation report must contain these columns:

| Check | Expected result | Actual result | Status | Remediation |
|---|---|---|---|---|
| User primary-key uniqueness | Zero duplicates | Execution-dependent | PASS/FAIL | Remove or investigate duplicates |
| Assignment uniqueness | One assignment per user | Execution-dependent | PASS/FAIL | Investigate reassignment |
| Event primary-key uniqueness | Zero duplicate event IDs | Execution-dependent | PASS/FAIL | Deduplicate or quarantine |
| User foreign keys | Every event user exists | Execution-dependent | PASS/FAIL | Quarantine orphan events |
| Treatment categories | Only control/treatment | Execution-dependent | PASS/FAIL | Standardize or reject |
| Event categories | Approved event names | Execution-dependent | PASS/FAIL | Reject unexpected values |
| Timestamp validity | Non-null and within study bounds | Execution-dependent | PASS/FAIL | Quarantine invalid rows |
| Subscription keys | Existing users only | Execution-dependent | PASS/FAIL | Reject orphan subscriptions |
| Missingness | Required fields complete | Execution-dependent | PASS/FAIL | Document and remediate |
| Outliers | Investigated, not silently deleted | Execution-dependent | INVESTIGATE | Explain treatment |
| Leakage | No post-treatment adjustment variables | Zero violations | PASS/FAIL | Remove leaked features |

### 6.2 Defect testing

To demonstrate that tests work, make a temporary copy and inject one defect at a time:

- Duplicate an event ID.
- Replace a treatment value with `unknown`.
- Add an orphan user ID.
- Add an impossible timestamp.
- Add a negative count if counts are present.

The validator must fail the relevant check. Do not commit intentionally corrupted production inputs.

### 6.3 Validation exit criteria

Do not load data into BigQuery until:

- Required-key checks pass.
- Category checks pass.
- Foreign-key checks pass.
- Date checks pass.
- Any intentional test defects are removed.
- The report is saved under `outputs/reports/data_quality_report.csv`.

---

## 7. Create BigQuery Resources

### Step 1 — Select the project and location

Use project `driiiportfolio`. Select one BigQuery location and use it consistently for all datasets and connected resources. Dataset location mismatches can prevent queries or dashboard connections.

### Step 2 — Create datasets

Run `sql/01_create_datasets.sql` in the BigQuery SQL editor. Verify that these datasets exist:

```text
snap_growth_raw
snap_growth_transform
snap_growth_analytics
snap_growth_dashboard
```

If the SQL location is not accepted in your environment, create the datasets in the console and record the selected location in the run metadata.

### Step 3 — Create raw tables

Run `sql/02_create_raw_tables.sql` after editing the table definitions if necessary. Prefer explicit schemas. Confirm:

- `events` is partitioned by event date.
- Common filter/join fields are clustered where supported.
- Date, timestamp, boolean, integer, and string fields have deliberate types.
- Raw tables preserve source records; cleaning belongs in later layers.

### Step 4 — Load CSVs

Use either the BigQuery console or a documented `bq`/Python load process.

Console process:

1. Open BigQuery Explorer.
2. Select `driiiportfolio.snap_growth_raw`.
3. Select **Create table**.
4. Choose **Upload** or Cloud Storage as the source.
5. Select CSV format.
6. Specify the target table name.
7. Skip one leading header row.
8. Use the explicit schema from the data dictionary.
9. Confirm the correct partition configuration for events.
10. Create the table.

After every load, run:

```sql
SELECT COUNT(*) AS row_count FROM `driiiportfolio.snap_growth_raw.users`;
SELECT COUNT(*) AS row_count FROM `driiiportfolio.snap_growth_raw.experiment_assignments`;
SELECT COUNT(*) AS row_count FROM `driiiportfolio.snap_growth_raw.events`;
SELECT COUNT(*) AS row_count FROM `driiiportfolio.snap_growth_raw.subscriptions`;
```

Compare the results to the local CSV counts. A mismatch is a blocking issue until explained.

---

## 8. Run BigQuery Data Quality Checks

Run `sql/03_data_quality_checks.sql`.

Add checks for:

```sql
-- Required user columns
SELECT COUNT(*) AS failures
FROM `driiiportfolio.snap_growth_raw.users`
WHERE user_id IS NULL OR signup_date IS NULL;

-- One assignment per user
SELECT COUNT(*) AS duplicate_users
FROM (
  SELECT user_id
  FROM `driiiportfolio.snap_growth_raw.experiment_assignments`
  GROUP BY user_id
  HAVING COUNT(*) != 1
);

-- Orphan subscriptions
SELECT COUNT(*) AS orphan_subscriptions
FROM `driiiportfolio.snap_growth_raw.subscriptions` s
LEFT JOIN `driiiportfolio.snap_growth_raw.users` u USING (user_id)
WHERE u.user_id IS NULL;

-- Date validity
SELECT COUNT(*) AS invalid_dates
FROM `driiiportfolio.snap_growth_raw.events`
WHERE event_ts IS NULL OR DATE(event_ts) < DATE '2026-01-01';
```

Save query results, screenshots, or exported tables as validation artifacts. Do not only state that checks passed.

---

## 9. Transform and Standardize Data

Run `sql/04_transform.sql`.

The transformation layer must:

1. Normalize event names with `LOWER(TRIM(...))`.
2. Remove exact duplicate event records.
3. Reject null IDs and timestamps.
4. Retain an auditable relationship to raw data.
5. Create a clean event date for partition filtering.
6. Restrict event names to the documented event taxonomy.
7. Avoid silently converting invalid values into valid values.

Run a post-transform comparison:

```sql
SELECT COUNT(*) FROM `driiiportfolio.snap_growth_raw.events`;
SELECT COUNT(*) FROM `driiiportfolio.snap_growth_transform.clean_events`;
```

Explain every difference in the data-quality report.

---

## 10. Engineer User-Level Features

Run `sql/05_feature_engineering.sql`.

The output must have exactly one row per user. Validate that grain:

```sql
SELECT COUNT(*) AS rows, COUNT(DISTINCT user_id) AS users
FROM `driiiportfolio.snap_growth_analytics.user_experiment_metrics`;
```

These values must be equal. If they are not, investigate join multiplication before proceeding.

### Feature rules

- Pre-treatment variables: market, device type, acquisition channel, signup date, and any valid pre-treatment activity.
- Primary outcome: D28 retention.
- Secondary outcomes: D7 activation and D28 subscription conversion.
- Count outcomes: messages and app opens in fixed windows.
- Never use treatment-exposed events as pre-treatment adjustment variables.
- Do not use the simulated latent propensity in the final analysis; it exists only to create realistic synthetic relationships.
- Do not use hidden generator labels as observed analytical features.

Create a feature dictionary with definition, source, window, business meaning, and leakage risk.

---

## 11. Statistical Analysis in Colab

### Step 1 — Retrieve only the analytical dataset

Do not download raw event data into Colab for analysis if BigQuery has already aggregated it. Retrieve the one-row-per-user analytical table with only required columns.

### Step 2 — Verify assignment and grain

Run:

```python
assert df["user_id"].is_unique
assert set(df["treatment_group"].dropna()) <= {"control", "treatment"}
assert df["treatment_group"].notna().all()
```

Calculate treatment share and assess sample-ratio mismatch against the pre-specified assignment ratio.

### Step 3 — Run the primary analysis

For D28 retention:

1. Calculate user counts by treatment.
2. Calculate retention rates.
3. Calculate treatment minus control risk difference.
4. Calculate a 95% confidence interval.
5. Calculate a p-value using a suitable two-sample proportion method.
6. Report practical significance against the pre-specified threshold.
7. Keep the analysis intention-to-treat.

### Step 4 — Run secondary and guardrail analyses

Repeat the same structured process for activation, subscription conversion, and guardrails. Clearly label them secondary or exploratory.

### Step 5 — Run sensitivity analysis

Use a regression-adjusted model only with pre-treatment variables. Compare its estimate with the unadjusted ITT estimate. Explain any material difference.

### Step 6 — Check assumptions and diagnostics

Create outputs for:

- Treatment balance.
- Missingness.
- Outcome-window completeness.
- Distribution of count outcomes.
- Confidence intervals.
- Segment sample sizes.
- Multiple-testing treatment.
- Sensitivity to exclusions.
- Leakage audit.

### Step 7 — Export results

Save:

```text
outputs/reports/experiment_results.csv
outputs/reports/assumption_checks.csv
outputs/reports/analytical_validation_checklist.csv
outputs/figures/primary_effect.png
outputs/figures/retention_by_treatment.png
outputs/figures/segment_effects.png
```

Every numerical result is an **EXECUTION-DEPENDENT RESULT** until produced by the executed notebook.

---

## 12. Analytical Validation Checklist

Before writing findings, mark each item `PASS`, `FAIL`, or `INVESTIGATE`:

| Area | Check |
|---|---|
| Grain | One row per user in the analytical dataset |
| Keys | No duplicate user IDs or orphan foreign keys |
| Assignment | One assignment per user and valid treatment categories |
| SRM | Treatment allocation consistent with pre-specified design |
| Missingness | Required outcomes and assignment complete |
| Windows | Outcomes use fixed, non-overlapping, documented windows |
| Leakage | No post-treatment variable used as pre-treatment adjustment |
| Joins | No join explosion or duplicate counting |
| Statistics | Method matches binary/count outcome and randomized design |
| Uncertainty | Confidence intervals and effect sizes are included |
| Practicality | Statistical significance separated from business significance |
| Sensitivity | Alternative reasonable specifications evaluated |
| Reproducibility | Fresh runtime reproduces outputs using the same seed |
| Limitations | Synthetic-data and external-validity limits documented |

Any `FAIL` in grain, assignment, leakage, join logic, or outcome construction blocks publication.

---

# 13. Looker Studio Dashboard Build Manual

## 13.1 Dashboard identity and design system

**Report name:** `Synthetic Snapchat Growth Experiment — Executive Decision Support`

**Page names:**

1. `01 Executive Decision`
2. `02 Funnel and Retention`
3. `03 Segments and Guardrails`
4. `04 Data Quality and Methodology`

**Audience:** Hypothetical product, growth, analytics, engineering, and executive stakeholders.

**Design goals:** One decision per page, curated BigQuery views, explicit metric definitions, no raw-table joins inside charts, clear distinction between observed results and interpretation, and visible synthetic-data disclosure.

**Recommended visual style:**

- Canvas: 16:9 landscape.
- Background: white or very light gray.
- Header: dark charcoal/navy.
- Primary accent: Snap-inspired yellow used sparingly; this is a portfolio design choice and is not an official Snap brand asset.
- Positive: green only for favorable, validated direction.
- Negative/guardrail: red/orange.
- Neutral/unknown: gray.
- Use one consistent font and avoid decorative effects.
- Display rates as percentages with one decimal place unless small counts require more precision.
- Display counts with comma separators.
- Include a footer on every page: `Synthetic portfolio data | Not an official Snap Inc. report | Refresh: [timestamp]`.

## 13.2 Prepare BigQuery dashboard views

Connect Looker Studio to curated views in `driiiportfolio.snap_growth_dashboard`, not raw event tables.

Recommended views:

- `executive_summary`
- `funnel_summary`
- `retention_daily`
- `segment_results`
- `guardrail_results`
- `data_quality_summary`
- `experiment_metadata`

If a view does not yet exist, create it in `sql/07_dashboard_views.sql`. Prefer BigQuery views over Looker Studio blends because BigQuery provides centralized join logic, stable denominators, easier testing, and lower risk of inconsistent calculations.

### Suggested `executive_summary` fields

```text
metric_name STRING
metric_group STRING
treatment_group STRING
users INT64
metric_value FLOAT64
control_value FLOAT64
risk_difference FLOAT64
relative_difference FLOAT64
ci_lower FLOAT64
ci_upper FLOAT64
p_value FLOAT64
practical_threshold FLOAT64
result_status STRING
run_timestamp TIMESTAMP
```

### Suggested `funnel_summary` fields

```text
funnel_stage STRING
treatment_group STRING
users INT64
stage_rate FLOAT64
stage_order INT64
```

### Suggested `retention_daily` fields

```text
metric_date DATE
treatment_group STRING
users INT64
activated_users INT64
retained_users INT64
subscription_users INT64
activation_rate FLOAT64
d28_retention_rate FLOAT64
subscription_rate FLOAT64
```

### Suggested `segment_results` fields

```text
segment_name STRING
segment_value STRING
treatment_group STRING
users INT64
metric_name STRING
metric_value FLOAT64
risk_difference FLOAT64
ci_lower FLOAT64
ci_upper FLOAT64
sample_size_flag STRING
```

### Suggested `data_quality_summary` fields

```text
check_name STRING
check_group STRING
expected_result STRING
actual_result STRING
status STRING
remediation STRING
run_timestamp TIMESTAMP
```

## 13.3 Create the report and connect data

1. Sign in to Looker Studio.
2. Select **Create → Report**.
3. Name the report exactly `Synthetic Snapchat Growth Experiment — Executive Decision Support`.
4. Select the BigQuery connector.
5. Choose project `driiiportfolio`.
6. Choose the appropriate `snap_growth_dashboard` dataset.
7. Add each curated view as a data source only when required.
8. Confirm the field types: dates are Date, timestamps are Date & Time, rates are Percent/Number, IDs are Text, and counts are Number.
9. Rename confusing display labels in the data-source field configuration, but preserve source-field lineage in the documentation.
10. Set the report data credentials and sharing permissions deliberately. Do not make the report public if the connected data is not intended for public access.
11. Add the four pages and name them exactly as specified.

If the connector cannot see the project or dataset, verify Google Cloud permissions, dataset location, connector credentials, and that the authorized account is the intended account.

## 13.4 Add global controls

Add these controls to pages where they are meaningful:

- Date range control using `metric_date` or the documented study date.
- Drop-down filter for `market` when the underlying source contains market.
- Drop-down filter for `device_type` when available.
- Drop-down filter for `acquisition_channel` when available.
- Treatment-group selector only on diagnostic pages; the executive page should show control and treatment together.
- Reset/filter-clear affordance if supported.

Configure controls to affect the intended page or report. Avoid placing a control on a page when its field is absent or semantically incompatible with the source.

---

## PAGE TITLE: 01 Executive Decision

**Purpose:** Give leadership a decision-ready summary of the primary experiment result, secondary outcomes, guardrails, and analysis trustworthiness.

**Page-level controls:** Date range if applicable; market/device/channel filters only if the executive view was designed to support those dimensions. Default to all users.

### CHART 1: Eligible Users

**Chart Type:** Scorecard  
**Data Source:** `driiiportfolio.snap_growth_dashboard.executive_summary`  
**Dimensions:** None  
**Metrics:** `users`, aggregation `SUM`  
**Filter:** `metric_group = 'primary'` or use a dedicated one-row metric view.  
**Date Range Settings:** Use the report default study period; do not use an arbitrary rolling period.

**Calculated Field(s):** None if `users` is already a validated aggregate. If sourced from a one-row-per-user table, use a BigQuery view with `COUNT(DISTINCT user_id)` rather than a chart-level count.

**Visualization Notes:**

- Title: `Eligible Users`.
- Compact notation off if exact counts are important.
- Show comparison only if comparison semantics are meaningful.
- Add a subtitle or text note: `Synthetic randomized users in the analysis population`.

### CHART 2: Treatment Allocation

**Chart Type:** Scorecard  
**Data Source:** `executive_summary`  
**Dimensions:** None  
**Metrics:** `treatment_share`, aggregation `AVG` only if the view has one row; otherwise calculate in BigQuery.  
**Filter:** `metric_name = 'treatment_share'`.

**Calculated Field:** Prefer BigQuery. If required at chart level and the source contains aggregated fields:

```text
SUM(treatment_users) / SUM(users)
```

**Data type:** Percent. **Aggregation:** Aggregated.

**Visualization Notes:** Title `Treatment Allocation`; add a note with the expected assignment ratio. Do not label the allocation as balanced until the executed SRM check passes.

### CHART 3: Primary D28 Retention by Group

**Chart Type:** Bar chart, horizontal  
**Data Source:** `executive_summary`  
**Dimension:** `treatment_group`  
**Metric:** `metric_value`, aggregation `AVG` if one row per group/metric; preferably `SAFE_DIVIDE(SUM(retained_users), SUM(users))` in BigQuery.  
**Filter:** `metric_name = 'd28_retention'`.  
**Sort:** `treatment_group` ascending with control first.

**Calculated Field:** If using row-level counts, create in BigQuery:

```sql
SAFE_DIVIDE(SUM(retained_users), SUM(users)) AS retention_rate
```

Do not average precomputed percentages across unequal groups.

**Visualization Notes:**

- Title: `D28 Retention by Experiment Group`.
- Data labels on, one decimal place.
- Control color gray; treatment color yellow or blue.
- Add a reference line only for the control value if the chart supports a fixed/metric reference line; otherwise use the effect chart below.
- Enable cross-filtering only if clicking a group should filter the other page components.

### CHART 4: Primary Effect with Confidence Interval

**Chart Type:** Horizontal bar chart or table with metric and CI; use a table if the connector cannot render an interval cleanly.  
**Data Source:** `executive_summary`  
**Dimension:** `metric_name`  
**Metrics:** `risk_difference`, `ci_lower`, `ci_upper`, `p_value`; aggregation `AVG` only when one row exists per metric.  
**Filter:** `metric_name = 'd28_retention'`.

**Calculated Field:**

```text
CASE
  WHEN risk_difference >= practical_threshold THEN 'Positive practical signal'
  WHEN risk_difference <= -practical_threshold THEN 'Negative practical signal'
  ELSE 'Below practical threshold'
END
```

**Data type:** Text. **Aggregation:** Record-level.

**Visualization Notes:**

- Title: `Primary Effect: Treatment − Control`.
- Display the effect in percentage points, not only percent relative change.
- Show `ci_lower` and `ci_upper` in a table or tooltip.
- Add a zero reference line.
- Add a second reference line only if the practical threshold is documented.
- Use explicit text: `Causal interpretation applies only to the simulated randomized assignment; external validity is not established.`

### CHART 5: Outcome Scorecards Row

Create three scorecards:

1. `D7 Activation Rate` — metric `activation_rate`, filtered to `metric_name = 'activation'`.
2. `D28 Subscription Conversion` — metric `subscription_rate`, filtered to `metric_name = 'subscription_conversion'`.
3. `Guardrail Status` — metric or text from `guardrail_results`; use a table if a text scorecard is unsupported.

For each rate, use a BigQuery-calculated numerator/denominator rate. Do not average segment rates.

### CHART 6: Decision Status

**Chart Type:** Table with one row  
**Data Source:** `executive_summary`  
**Dimension:** `result_status`  
**Metrics:** `risk_difference`, `ci_lower`, `ci_upper`, `p_value`, `users`  
**Filter:** `metric_name = 'd28_retention'`.

**Calculated Field:** Do not make an irreversible launch recommendation in Looker Studio. Display a status generated by the statistical notebook, such as `EXECUTION-DEPENDENT RESULT` until populated.

**Visualization Notes:** Conditional formatting:

- Green only for a validated positive recommendation.
- Orange for investigate/iterate.
- Red for validated negative or guardrail-harm status.
- Gray for not run or insufficient data.

---

## PAGE TITLE: 02 Funnel and Retention

**Purpose:** Explain where user behavior differs across the onboarding and early product funnel.

**Page-level controls:** Date range, market, device, acquisition channel, treatment group.

### CHART 7: Onboarding Funnel

**Chart Type:** Funnel chart if available; otherwise horizontal bar chart with stage ordering.  
**Data Source:** `funnel_summary`  
**Dimension:** `funnel_stage`  
**Metric:** `users`, aggregation `SUM`  
**Sort:** `stage_order` ascending.  
**Filter:** Optional treatment group and page controls.

**Calculated Field:**

```text
SAFE_DIVIDE(SUM(users), SUM(eligible_users))
```

Use a BigQuery view if `eligible_users` is not at the same grain. Name the field `stage_rate` and format as Percent.

**Visualization Notes:**

- Title: `User Funnel by Experiment Stage`.
- Show absolute users and rate where the chart supports both.
- Do not use a pie chart for sequential funnel stages.
- Apply consistent treatment colors.
- Enable cross-filtering by treatment group or market if appropriate.

### CHART 8: Daily Activation Trend

**Chart Type:** Time series  
**Data Source:** `retention_daily`  
**Dimension:** `metric_date`  
**Metric:** `activation_rate`, aggregation `AVG` only if one row per date/group; otherwise calculate from counts.  
**Breakdown:** `treatment_group`  
**Date Range Dimension:** `metric_date`  
**Default Date Range:** Full synthetic study period.

**Calculated Field:** Prefer:

```sql
SAFE_DIVIDE(SUM(activated_users), SUM(users)) AS activation_rate
```

**Visualization Notes:**

- Title: `Activation Rate Over Time`.
- Lines: control and treatment.
- Points on only when the number of dates is manageable.
- Use a zero-to-one percent axis where possible.
- Add a trendline only as descriptive context; do not interpret it causally.
- Show missing dates explicitly or document why they are absent.

### CHART 9: D28 Retention Comparison

**Chart Type:** Grouped bar chart  
**Data Source:** `retention_daily` or a cohort view  
**Dimension:** cohort date or cohort week  
**Metric:** `d28_retention_rate`, aggregation based on validated numerator/denominator fields  
**Breakdown:** `treatment_group`  
**Sort:** cohort date ascending.

**Visualization Notes:**

- Title: `D28 Retention by Cohort and Group`.
- Use a consistent cohort window.
- Do not show incomplete cohorts as if they have complete D28 observation.
- Filter out cohorts without a full 28-day follow-up using a documented field.

### CHART 10: Engagement Distribution

**Chart Type:** Box plot if supported; otherwise table or histogram alternative.  
**Data Source:** `user_experiment_metrics`  
**Dimension:** `treatment_group`  
**Metrics:** `opens_28d`, `messages_28d`; aggregation `AVG`, `MEDIAN`, or percentile fields supplied by BigQuery/Python.  
**Filter:** Eligible users with complete windows.

**Visualization Notes:**

- Title: `Engagement Distribution — 28-Day Window`.
- Prefer median and percentile outputs for heavy-tailed counts.
- Do not use a mean-only scorecard to imply that a skewed distribution is symmetric.
- Add a methodology note that engagement counts are secondary outcomes.

### CHART 11: Retention Metric Table

**Chart Type:** Table  
**Data Source:** `executive_summary`  
**Dimensions:** `metric_name`, `treatment_group`  
**Metrics:** `users`, `metric_value`, `risk_difference`, `ci_lower`, `ci_upper`, `p_value`  
**Rows:** Limit to documented primary and secondary metrics.

**Visualization Notes:**

- Title: `Experiment Metric Detail`.
- Sort primary metric first using a BigQuery `metric_order` field.
- Format rates as percentages and p-values consistently.
- Add conditional formatting only to effect direction/status, not raw p-values alone.

---

## PAGE TITLE: 03 Segments and Guardrails

**Purpose:** Identify whether effects differ across pre-treatment segments and whether the treatment creates potential user-experience harm.

**Page-level controls:** Segment name, market, device type, acquisition channel, treatment group, date range where supported.

### CHART 12: Segment Effect Forest Table

**Chart Type:** Table; use a horizontal bar chart if an interval-capable chart is available.  
**Data Source:** `segment_results`  
**Dimensions:** `segment_name`, `segment_value`, `metric_name`  
**Metrics:** `users`, `risk_difference`, `ci_lower`, `ci_upper`, `p_value`, `sample_size_flag`  
**Filter:** `metric_name = 'd28_retention'`.

**Calculated Field:**

```text
CASE
  WHEN sample_size_flag != 'OK' THEN 'Small sample — investigate'
  WHEN ci_lower > 0 THEN 'Positive interval'
  WHEN ci_upper < 0 THEN 'Negative interval'
  ELSE 'Interval crosses zero'
END
```

**Visualization Notes:**

- Title: `D28 Retention Effect by Pre-Treatment Segment`.
- Sort by segment name and value, not by favorable effect unless explicitly selected.
- Display sample sizes beside effects.
- Do not claim subgroup causality when cells are underpowered.
- Include a note that segment findings are exploratory unless pre-specified and powered.

### CHART 13: Guardrail Rate Comparison

**Chart Type:** Grouped bar chart  
**Data Source:** `guardrail_results`  
**Dimension:** `guardrail_name`  
**Metric:** `metric_value`  
**Breakdown:** `treatment_group`  
**Filter:** only documented guardrails.

**Visualization Notes:**

- Title: `Guardrail Rates by Experiment Group`.
- Use neutral colors for control/treatment and warning colors only when a validated threshold is crossed.
- Add reference lines for pre-specified maximum acceptable rates.
- Do not infer user harm from a proxy without documenting its limitation.

### CHART 14: Guardrail Status Table

**Chart Type:** Table  
**Data Source:** `guardrail_results`  
**Dimensions:** `guardrail_name`, `result_status`  
**Metrics:** `risk_difference`, `ci_lower`, `ci_upper`, `p_value`, `users`.

**Calculated Field:**

```text
CASE
  WHEN risk_difference <= -guardrail_threshold THEN 'Potential harm — investigate'
  WHEN ABS(risk_difference) < guardrail_threshold THEN 'Within threshold'
  ELSE 'Potential change — investigate'
END
```

**Visualization Notes:**

- Title: `Guardrail Review`.
- Use conditional formatting on `result_status`.
- Include an explicit `Not evaluated` status.
- Do not automatically convert a statistical result into a safety conclusion.

### CHART 15: Segment Sample Sizes

**Chart Type:** Bar chart  
**Data Source:** `segment_results`  
**Dimension:** `segment_value`  
**Metric:** `users`, aggregation `SUM`  
**Breakdown:** `segment_name`.

**Visualization Notes:**

- Title: `Segment Sample Sizes`.
- Sort descending by users.
- Add a minimum sample-size reference line if documented.
- This chart exists to prevent overinterpreting unstable subgroup estimates.

---

## PAGE TITLE: 04 Data Quality and Methodology

**Purpose:** Make the analysis auditable and show stakeholders whether the dashboard is fit for decision support.

**Page-level controls:** Run timestamp, check group, status.

### CHART 16: Data-Quality Status Scorecard

**Chart Type:** Scorecard  
**Data Source:** `data_quality_summary`  
**Metric:** count of checks where `status = 'PASS'`; aggregation `COUNT` or a BigQuery-produced `passed_checks` value.  
**Filter:** latest `run_timestamp`.

**Calculated Field:** If using row-level checks:

```text
CASE WHEN status = 'PASS' THEN 1 ELSE 0 END
```

Use `SUM` as the aggregate. A BigQuery summary field is preferable.

**Visualization Notes:** Title `Passed Data-Quality Checks`; show a comparison with total checks only if both values are available.

### CHART 17: Data-Quality Check Table

**Chart Type:** Table  
**Data Source:** `data_quality_summary`  
**Dimensions:** `check_group`, `check_name`, `status`, `actual_result`  
**Metrics:** None or `failure_count`  
**Sort:** status severity, then check group.

**Visualization Notes:**

- Title: `Data-Quality Validation Results`.
- Apply red/orange/green conditional formatting to status.
- Show remediation text.
- Filter to latest run timestamp.

### CHART 18: Experiment Metadata Table

**Chart Type:** Table  
**Data Source:** `experiment_metadata`  
**Dimensions:** `metadata_key`, `metadata_value`  
**Metrics:** None.

Include:

- Experiment name
- Primary estimand
- Primary metric
- Study period
- Random seed
- Run timestamp
- Data version
- Synthetic-data disclosure
- Analysis status

### CHART 19: Methodology Scorecard/Notice

**Chart Type:** Text box, not a data chart.  
**Data Source:** None.  
**Content:**

```text
Primary analysis: intention-to-treat randomized comparison.
Primary outcome: day-28 retention.
Uncertainty: 95% confidence intervals.
Secondary outcomes and segments: exploratory unless otherwise documented.
Data: synthetic portfolio data; not Snap internal data.
Numerical findings: execution-dependent.
```

**Visualization Notes:** Use a shaded methodology card. Do not use a fake numeric score for methodological quality.

---

## 13.5 Calculated-field policy

Use BigQuery for any calculation that requires reliable denominators, joins, deduplication, or statistical output. Use Looker Studio calculated fields only for display logic, labels, simple ratios over already-compatible aggregates, and conditional formatting.

Avoid:

- Averaging percentages across unequal groups.
- Counting events where the metric requires users.
- Joining raw users and events in separate chart sources.
- Recomputing p-values or confidence intervals in Looker Studio.
- Hiding metric definitions inside undocumented chart formulas.
- Using a post-treatment field in a control or filter that is presented as pre-treatment.

## 13.6 Blended data policy

Default: **Do not blend data** for the core report. Use BigQuery views instead.

If a blend is unavoidable for a small display-only element:

- Source A: `executive_summary`, key `metric_name`, metrics `risk_difference`, `ci_lower`, `ci_upper`.
- Source B: `experiment_metadata`, key `metric_name` or a single constant key, metrics/fields for methodology context.
- Join: `LEFT JOIN` from Source A to Source B.
- Justification: preserve all experiment metrics even when metadata is incomplete.
- Validate row counts before and after the blend.

Do not blend two independently aggregated sources on a non-unique key. If the join key is not unique, create a BigQuery view with the correct grain.

## 13.7 BigQuery view alternative

If a chart needs a calculated metric, create it in BigQuery. Example:

```sql
CREATE OR REPLACE VIEW `driiiportfolio.snap_growth_dashboard.funnel_summary` AS
WITH stage_counts AS (
  SELECT
    treatment_group,
    COUNT(*) AS eligible_users,
    COUNTIF(activated) AS activated_users,
    COUNTIF(d28_retained) AS retained_users,
    COUNTIF(subscribed_28d) AS subscribed_users
  FROM `driiiportfolio.snap_growth_analytics.user_experiment_metrics`
  GROUP BY treatment_group
)
SELECT treatment_group, 'Eligible' AS funnel_stage, eligible_users AS users, 1 AS stage_order
FROM stage_counts
UNION ALL
SELECT treatment_group, 'Activated', activated_users, 2 FROM stage_counts
UNION ALL
SELECT treatment_group, 'D28 Retained', retained_users, 3 FROM stage_counts
UNION ALL
SELECT treatment_group, 'Subscribed', subscribed_users, 4 FROM stage_counts;
```

Connect the resulting view using **Add data → BigQuery → project → dataset → view**. Document the view SQL and grain in `docs/data_architecture.md`.

## 13.8 Dashboard sharing and refresh

1. Click **Share**.
2. Assign viewer/editor permissions deliberately.
3. Keep the report restricted unless public access is intentional.
4. Confirm that the data-source credentials are appropriate for viewers.
5. Document the refresh behavior and last successful run.
6. If scheduled delivery is used, verify the recipient list and report access.
7. Never send confidential credentials, raw data, or service-account keys through the dashboard.

## 13.9 Dashboard QA checklist

- [ ] Report name is exact.
- [ ] Page names are exact.
- [ ] Every chart uses the documented source view.
- [ ] Every chart has a title.
- [ ] Every metric has a definition and correct aggregation.
- [ ] User rates use user denominators, not event denominators.
- [ ] Date controls filter the intended charts.
- [ ] Treatment colors are consistent.
- [ ] Control is shown before treatment where applicable.
- [ ] Zero and practical-threshold reference lines are documented.
- [ ] Confidence intervals are not fabricated or recomputed incorrectly.
- [ ] Small segments are flagged.
- [ ] Data-quality page shows actual validation results.
- [ ] Synthetic-data disclaimer appears on every page or in a persistent footer.
- [ ] No raw table is connected directly unless explicitly justified.
- [ ] Dashboard totals reconcile to BigQuery query results.
- [ ] Filters do not cause denominator drift without a visible explanation.
- [ ] Report sharing and credentials are tested.
- [ ] Screenshot or PDF export matches the intended layout.

---

## 14. Document Findings and Recommendations

Only after the statistical notebook and dashboard are executed, write:

### Descriptive findings
What happened in the generated sample?

### Diagnostic findings
What mechanisms are plausible? Label these **INTERPRETATION**.

### Statistical findings
What are the executed estimates, confidence intervals, p-values, and effect sizes?

### Business findings
What decision follows, subject to assumptions and limitations?

### Recommendation format

| Evidence | Interpretation | Recommendation | Expected impact | Measurement plan | Risk/constraint |
|---|---|---|---|---|---|
| Executed result | Clearly labeled inference | Expand, iterate, or stop | Formula or qualitative only unless measured | Follow-up experiment/monitoring | Synthetic-data and external-validity limits |

Never invent revenue, user growth, or financial impact. If an estimate is useful, provide a formula and label every assumption.

---

## 15. Final End-to-End Run Order

1. Review job description and blueprint.
2. Freeze business decision, estimand, metrics, and thresholds.
3. Prepare repository and run metadata.
4. Run synthetic-data generator.
5. Run local validation.
6. Create BigQuery datasets.
7. Load raw CSV tables.
8. Reconcile BigQuery and local row counts.
9. Run BigQuery data-quality checks.
10. Transform and standardize events.
11. Engineer one-row-per-user analytical features.
12. Validate grain, keys, windows, and leakage.
13. Run statistical notebook.
14. Export results, figures, and validation reports.
15. Create or refresh dashboard views.
16. Build the Looker Studio report using this manual.
17. Reconcile dashboard values to SQL results.
18. Write findings and recommendations.
19. Complete README, executive summary, dashboard summary, disclaimer, and limitations.
20. Run final QA.
21. Reproduce the project from a fresh runtime.
22. Commit only reviewed artifacts and documentation.

---

## 16. Final Deliverable Manifest

| Deliverable | Location | Purpose | Generated by | Status |
|---|---|---|---|---|
| Processing manual | `docs/portfolio_project_process_manual.md` | End-to-end execution instructions | Markdown | This file |
| Blueprint | `docs/portfolio_project_blueprint.md` | Project architecture and rationale | Markdown | Existing |
| Synthetic generator | `src/data_generation/generate_synthetic_data.py` | Creates reproducible CSV inputs | Python | Required |
| Validation code | `src/validation/validate_data.py` | Local data-quality checks | Python | Required |
| Analysis code | `src/analysis/experiment_analysis.py` | Statistical analysis | Python | Required |
| Raw CSVs | `data/synthetic/*.csv` | Generated inputs | Python | Generated after execution |
| BigQuery datasets | `driiiportfolio.snap_growth_*` | Raw, transform, analytics, dashboard layers | BigQuery | Create during execution |
| BigQuery tables/views | `driiiportfolio.snap_growth_dashboard.*` | Curated dashboard sources | BigQuery SQL | Create during execution |
| Statistical outputs | `outputs/reports/` | Results, assumptions, validation | Colab/Python | Generated after execution |
| Figures | `outputs/figures/` | Dashboard/report visual evidence | Colab/Python | Generated after execution |
| Looker Studio report | External Looker Studio URL | Executive decision dashboard | Looker Studio | Build after views exist |
| Dashboard documentation | `dashboards/dashboard_specification.md` | Chart inventory and metric definitions | Markdown | Required |
| Executive materials | `Executive_Summary.md`, `Dashboard_Executive_Summary.md` | Stakeholder communication | Markdown | Complete after execution |
| Disclaimer | `Project_Disclaimer.md` | Non-affiliation and data disclosure | Markdown | Required |

**Completion criterion:** The project is complete only when a second person can follow this manual from a fresh environment, reproduce the synthetic inputs and analytical outputs, connect the curated BigQuery views to Looker Studio, and understand which findings are executed results versus assumptions or interpretations.
