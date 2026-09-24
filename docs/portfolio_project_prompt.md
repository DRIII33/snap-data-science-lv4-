https://github.com/DRIII33/snap-data-science-lv4-/tree/main/docsENGINEERED PROMPT: END-TO-END SNAP INC. DATA SCIENTIST (LEVEL 4) PORTFOLIO PROJECT
ROLE AND PRIMARY OBJECTIVE
Act as a senior Data Science Portfolio Architect, Data Scientist, Analytics Engineer, Data Engineer, Statistical Analyst, and Technical Project Manager.
Your task is to design and provide complete, meticulous, executable, end-to-end instructions for building a professional Data Science portfolio project specifically aligned to the Snap Inc. Data Scientist (Level 4) job description provided in this conversation.
The finished project must be suitable for:

GitHub publication
Technical portfolio review
Data Scientist interview discussion
Executive-level portfolio review
Statistical methodology discussion
SQL/data-wrangling demonstration
Data visualization/dashboard demonstration
Business-case discussion
Technical storytelling
Demonstration of production-oriented analytical thinking
The objective is not merely to describe a project.
You must engineer the complete project from:
Business Scenario → Business Problem → Data Requirements → Data Architecture → Synthetic/External Data → Data Generation/Acquisition → Data Validation → BigQuery → SQL Transformation → Statistical Analysis → Modeling/Inference where appropriate → Insights → Looker Studio Dashboard → Executive Summary → Recommendations → GitHub Repository → Reproducibility Documentation
There must be NO PROCESS GAPS.
1. FIRST: REVIEW AND REFRESH THE ENTIRE CONVERSATION
Before designing the project:

Review the entire available chat transcript.
Identify all relevant:
portfolio-project frameworks
analytical frameworks
data-science methodologies
SQL conventions
BigQuery conventions
Python conventions
dashboard conventions
GitHub documentation conventions
synthetic-data conventions
statistical-analysis expectations
validation requirements
portfolio presentation requirements
Reconcile the current project with those previously established standards.
Refresh the project design so that it is fully aligned with the Snap Inc. Data Scientist (Level 4) job description.
Do not silently discard useful requirements from the conversation.
If two prior instructions conflict, explicitly identify the conflict and select the approach that best preserves:
factual accuracy
reproducibility
technical credibility
portfolio usefulness
alignment with the job description.
Do not invent prior conversation content that is unavailable to you.
2. JOB DESCRIPTION ALIGNMENT
Use the Snap Inc. Data Scientist (Level 4) job description as the primary requirements source.
Create a detailed Job Description → Portfolio Evidence Matrix.
For every significant requirement, responsibility, qualification, technical skill, analytical competency, or business competency in the job description, identify:
Job Description RequirementPortfolio ComponentEvidence ProducedTool/TechnologyGitHub DeliverableInterview Talking Point
Do not claim that the portfolio project demonstrates a competency unless the project actually produces evidence for it.
Clearly distinguish:

Explicitly demonstrated skills
Supporting skills
Skills that are not demonstrated by this project
Do not artificially force technologies or methodologies into the project merely to make the project appear more sophisticated.
3. PROJECT CONCEPT
Design one cohesive, realistic, end-to-end Snap Inc.-relevant Data Science project.
The project must resemble a legitimate business/data-science problem that a Data Scientist at approximately Level 4 could reasonably encounter.
The project should demonstrate the ability to:

Translate an ambiguous business problem into analytical questions
Define measurable outcomes
Design appropriate data requirements
Work with structured analytical data
Perform data quality assessment
Use SQL for data preparation and transformation
Use Python for statistical analysis and/or modeling
Select appropriate statistical methods
Explain why those methods were selected
Validate analytical assumptions
Quantify uncertainty where appropriate
Generate actionable insights
Communicate findings to technical and nontechnical stakeholders
Build an executive-facing dashboard
Document the work professionally
Produce reproducible artifacts
Do not manufacture access to Snap's internal data.
If Snap-specific internal data is unavailable, explicitly use synthetic or appropriately sourced public data and clearly disclose that limitation.
4. BUSINESS SCENARIO
Create a detailed business scenario aligned with:

Snap Inc.
The relevant department/function associated with the job description
A plausible current business challenge
The reason a Data Scientist at this level would be hired
A measurable business outcome
The scenario must answer:

Who?
Identify the hypothetical stakeholder(s).
Examples may include, if appropriate:

Product
Engineering
Ads
Marketing Science
User Growth
Monetization
Trust & Safety
Content
Business Operations
Product Analytics
Machine Learning
Data Engineering
Do not assume a department unless the job description supports that connection.

What?
What business problem exists?

Why?
Why does the problem matter?

Where?
What product, platform, workflow, funnel, or business process is affected?

When?
What analytical period is being studied?

How?
How can data science help?

Business impact
Define measurable outcomes such as:

engagement
retention
conversion
revenue
advertiser performance
user experience
operational efficiency
experiment performance
risk reduction
recommendation quality
Only use metrics that logically fit the selected scenario.
5. BUSINESS PROBLEM / CHALLENGES / BOTTLENECKS
Create a detailed section identifying:

Primary Business Problem
State the problem in one precise sentence.

Secondary Problems
Identify supporting problems.

Analytical Questions
Translate the business problem into specific analytical questions.

Hypotheses
Define testable hypotheses where appropriate.
For every hypothesis specify:

Null hypothesis
Alternative hypothesis
Metric
Population
Unit of analysis
Statistical test/model
Significance threshold if appropriate
Effect-size measure
Confidence interval approach
Interpretation criteria
Do not use statistical testing merely for appearance.
6. DATA STRATEGY
Determine whether the project should use:

Option A — Synthetic Data
Use synthetic data if:

appropriate public data does not adequately represent the business problem
privacy considerations make synthetic data preferable
synthetic data allows controlled experimentation
the portfolio objective requires demonstrating data generation
OR:

Option B — Public Data
Use public data if it provides a materially better foundation.
If public data is selected:
Explain:

Where the data comes from
Why it is appropriate
How it is legally/publicly accessible
How it should be downloaded
File formats
Data dictionary
Storage structure
Data-refresh considerations
Transformation requirements
Attribution/licensing requirements
Limitations
Potential mismatch with Snap's real internal data
Never imply public data is Snap internal data.
If synthetic data is selected, explicitly label it as synthetic throughout the project.
7. SYNTHETIC DATA DESIGN
If synthetic data is required, design a realistic data-generating process rather than randomly generating arbitrary numbers.
Explain:

Entities
Relationships
Primary keys
Foreign keys
Event structure
Time dimensions
Categorical variables
Numerical variables
Behavioral variables
Outcome variables
Missingness
Outliers
Noise
Correlations
Potential confounders
Treatment/control variables if experimentation is involved
Data leakage risks
The synthetic dataset should contain realistic relationships that allow the proposed statistical analysis to produce meaningful findings.
However:
DO NOT fabricate an outcome and then reverse-engineer the analysis to guarantee that outcome.
If the data-generating process intentionally includes known simulated effects for validation purposes, explicitly document that fact.
8. GOOGLE CLOUD / BIGQUERY ARCHITECTURE
Use the following Google Cloud project:
BigQuery Project ID: driiiportfolio
Design the complete BigQuery architecture.
Specify:

Dataset name(s)
Table names
View names
Table types
Partitioning
Clustering
Data types
Primary/business keys
Relationships
Grain of each table
Expected row counts
Loading method
Transformation layer
Analytical layer
Dashboard layer
Provide a complete schema table:
DatasetTable/ViewGrainColumnData TypeDescriptionKeyNullableSource
Use BigQuery-compatible SQL.
9. BIGQUERY FREE-TIER CONSIDERATIONS
The project must be designed with the 2026 BigQuery free-tier limitations and current Google Cloud pricing structure in mind.
Because pricing and quotas can change:

Verify current information using authoritative Google Cloud documentation where possible.
Do not state outdated limits as current facts.
Explain which operations could generate costs.
Design the project to minimize unnecessary bytes processed.
Use:
partitioning where appropriate
clustering where appropriate
column selection instead of SELECT *
limited development queries
appropriately sized synthetic datasets
dry runs/query estimates when useful
Explain how the user can monitor usage.
Include a cost-control checklist.
Do not deliberately create an enormous dataset merely to make the project appear sophisticated.
10. GOOGLE COLAB — DATA GENERATION
If synthetic data is used, provide the complete Python code required to generate it.
The code must:

Be complete
Be executable
Use deterministic random seeds where appropriate
Include imports
Define configuration variables
Generate all required tables
Preserve relational integrity
Validate generated data
Detect unexpected nulls
Detect duplicate keys
Validate ranges
Validate categorical values
Validate date/time fields
Validate foreign-key relationships
Produce summary statistics
Save CSV files automatically
Clearly identify output paths
Prepare the files for BigQuery ingestion
Do not provide pseudocode where executable Python is required.
The code should be optimized for the Google Colab free tier in 2026.
Avoid unnecessary memory-intensive operations.
Explain expected:

RAM usage
approximate dataset size
execution time considerations
scaling limitations
Where appropriate, provide configurable parameters such as:

N_USERS = ...
N_EVENTS = ...
RANDOM_SEED = ...
This should allow the user to scale the project without rewriting the entire program.
11. DATA VALIDATION
Create a formal data-quality framework.
At minimum evaluate:

Completeness
Uniqueness
Referential integrity
Validity
Consistency
Timeliness
Range violations
Duplicate records
Missing values
Impossible values
Outliers
Distribution anomalies
Leakage
Unexpected category values
Provide Python validation code where appropriate.
Provide BigQuery SQL validation queries where appropriate.
Document expected results.
Create a:
Data Quality Report
containing:
CheckExpected ResultActual ResultStatusRemediation
Do not simply state that the data is "clean."
Demonstrate that it was validated.
12. BIGQUERY SQL DEVELOPMENT
Provide all necessary SQL in full.
Organize SQL logically, for example:

sql/
├── 01_create_datasets.sql
├── 02_create_raw_tables.sql
├── 03_data_quality_checks.sql
├── 04_clean_transform.sql
├── 05_feature_engineering.sql
├── 06_statistical_inputs.sql
├── 07_dashboard_views.sql
└── 08_final_validation.sql
Adjust this structure if another architecture is more appropriate.
For every SQL script explain:

Purpose
Input tables
Output tables/views
Grain
Transformations
Business logic
Why the transformation exists
Do not leave undocumented SQL.
13. DATA NORMALIZATION / STANDARDIZATION
Where appropriate, address:

Naming conventions
Data types
Date/time standardization
Categorical standardization
Unit standardization
Null handling
Deduplication
Key normalization
String normalization
Boolean normalization
Numeric precision
Derived fields
Explain whether the final analytical model is:

normalized
denormalized
star-schema-oriented
analytical wide-table-oriented
Explain why.
Do not normalize data merely because normalization is theoretically possible.
14. FEATURE ENGINEERING
Identify all features required for the analysis.
For each feature provide:
FeatureDefinitionSourceSQL/Python LogicBusiness MeaningLeakage Risk
Explicitly identify:

Pre-treatment variables
Post-treatment variables
Outcome variables
Potential confounders
Variables that must not be used because they create leakage
15. STATISTICAL ANALYSIS
Use Google Colab for statistical analysis where appropriate.
Determine the correct statistical methodology based on the actual business question and data structure.
Do not automatically use:

t-tests
regression
ANOVA
chi-square
correlation
machine learning
unless justified.
For every statistical method explain:

Why this method?
Why is it appropriate?

Why not the alternatives?
Briefly explain why other plausible methods were not selected.

Assumptions
Identify assumptions.

Diagnostics
Provide appropriate diagnostic tests/plots.

Effect size
Report practical effect size where appropriate.

Statistical significance
If hypothesis testing is appropriate, define:

α
p-value
confidence interval
Practical significance
Distinguish statistical significance from business significance.

Uncertainty
Quantify uncertainty where appropriate.
16. EXPERIMENTATION / CAUSAL INFERENCE
If the business problem involves treatment, experimentation, product changes, advertising interventions, or similar causal questions, determine whether a causal methodology is appropriate.
Potential methods may include:

A/B testing
Difference-in-Differences
Regression adjustment
Propensity methods
CUPED or related variance-reduction techniques
Interrupted time series
Causal inference frameworks
Only use a method when justified.
Explicitly discuss:

Treatment
Control
Unit of randomization
Unit of analysis
Pre-period
Post-period
Confounders
Parallel trends where relevant
Selection bias
Spillover/interference
Statistical power where relevant
Multiple testing where relevant
If synthetic data is used, clearly explain which causal relationships are simulated rather than observed from real-world experimentation.
17. MACHINE LEARNING — ONLY IF JUSTIFIED
Determine whether machine learning is actually necessary.
If it is not necessary:
Do not add machine learning simply to make the project look more advanced.
If machine learning is appropriate, provide:

Problem formulation
Target variable
Feature set
Train/validation/test strategy
Baseline
Model selection rationale
Evaluation metrics
Cross-validation
Hyperparameter approach
Class imbalance strategy if relevant
Leakage prevention
Interpretability
Error analysis
Business implications
Compare model performance against a meaningful baseline.
18. ANALYTICAL VALIDATION
Before interpreting results:
Validate:

Dataset grain
Sample size
Missingness
Distribution
Statistical assumptions
Feature construction
Treatment assignment if applicable
Outcome construction
Query logic
Aggregation logic
Duplicate counting
Join explosions
Leakage
Sensitivity to assumptions
Include a formal:

Analytical Validation Checklist
with PASS / FAIL / INVESTIGATE statuses.
Do not declare a result valid merely because the code executes successfully.
19. UNDERSTANDING THE DATA FLOW: FROM SYNTHETIC DATA TO STATISTICAL INSIGHTS
Create a dedicated, easy-to-understand section titled exactly:

Understanding the Data Flow: From Synthetic Data to Statistical Insights
Explain the entire flow step by step:

Synthetic/Public Source Data
        ↓
Python / Google Colab
        ↓
CSV Files
        ↓
BigQuery Raw Layer
        ↓
Data Quality Validation
        ↓
BigQuery Transformation Layer
        ↓
Feature Engineering
        ↓
Analytical Dataset / Views
        ↓
Google Colab Statistical Analysis
        ↓
Statistical Results
        ↓
Business Insights
        ↓
BigQuery Dashboard Views
        ↓
Looker Studio
        ↓
Executive Decision Support
For each stage explain:

What enters the stage
What happens
What leaves the stage
Why the stage exists
Which tool performs it
Which artifact is produced
How the next stage uses that artifact
The explanation must be understandable to someone who knows basic data analytics but is not an expert in every component.
20. GOOGLE COLAB STATISTICAL ANALYSIS NOTEBOOK
Provide the complete notebook structure.
For each section provide:

Markdown explanation
Python code
Expected output
Validation
Interpretation
Recommended structure:

01_Project_Setup
02_Load_Data
03_Data_Validation
04_Exploratory_Data_Analysis
05_Feature_Engineering
06_Methodology
07_Assumption_Checks
08_Statistical_Analysis
09_Effect_Size
10_Confidence_Intervals
11_Sensitivity_Analysis
12_Visualization
13_Insights
14_Business_Recommendations
15_Final_Validation
Modify as needed based on the actual project.
The notebook must be reproducible from a fresh Google Colab session.
21. GOOGLE COLAB FREE-TIER DESIGN
Design the notebook for the current free Colab environment.
Avoid unnecessary:

memory consumption
giant intermediate objects
redundant dataframe copies
repeated downloads
unnecessary model training
expensive computation
Where useful:

process data in chunks
use efficient data types
push large transformations into BigQuery
retrieve only analytical subsets into Colab
Explain which computations belong in BigQuery versus Python and why.
22. LOOKER STUDIO DASHBOARD
Design the complete Looker Studio dashboard.
Provide:

Dashboard Title
Specify the exact title.
If multiple pages are required, provide exact page titles.
For example:

Page 1 — Executive Overview
Page 2 — Business Performance
Page 3 — User/Product Behavior
Page 4 — Statistical Findings
Page 5 — Data Quality & Methodology
Do not use these pages automatically; design the actual pages based on the project.
For every dashboard page specify:

Purpose
Target audience
Data source
BigQuery table/view
KPIs
Charts
Filters
Dimensions
Metrics
Date controls
Calculated fields
Required interactions
Business question answered
Provide a dashboard wireframe in text.
23. LOOKER STUDIO DATA MODEL
Identify exactly which BigQuery views/tables feed each dashboard component.
Create a mapping:
Dashboard ComponentBigQuery ViewDimensionMetricCalculationBusiness Question
Do not connect Looker Studio directly to messy raw tables if an analytical view is more appropriate.
24. INSIGHTS
Generate insights only after the analytical process is defined.
Separate:

Descriptive Findings
What happened?

Diagnostic Findings
Why might it have happened?

Statistical Findings
What evidence supports the observed relationship/difference?

Business Findings
Why does it matter?

Limitations
What cannot be concluded?
Never claim causality from observational data without appropriate causal methodology.
Never manufacture numerical results.
If actual analysis cannot be executed during prompt generation, clearly identify:
EXPECTED OUTPUT — MUST BE GENERATED AFTER EXECUTION
rather than inventing results.
25. RECOMMENDATIONS / NEXT STEPS
Create recommendations only from validated findings.
For each recommendation specify:
FindingRecommended ActionRationaleExpected Business ImpactMeasurement PlanRisk/Constraint
Do not invent financial impact.
If financial impact must be estimated, provide the formula and clearly identify assumptions.
Distinguish:

Evidence
Interpretation
Recommendation
Assumption
26. PROJECT LIMITATIONS
Create a comprehensive limitations section covering:

Synthetic data
Public-data limitations if applicable
Sample-size limitations
Data-generating assumptions
Causal limitations
Statistical limitations
Measurement limitations
Missing variables
Potential confounding
Generalizability
Difference between portfolio simulation and production Snap environment
27. PROJECT DISCLAIMER
Create a dedicated:
Project_Disclaimer.md
It must clearly state:

This is a portfolio project.
It is not an official Snap Inc. project.
It does not use confidential Snap data.
Synthetic data must be identified as synthetic.
Public data must be identified as public.
Results are illustrative unless supported by actual public data.
Any simulated relationships must be disclosed.
The project does not claim access to Snap's internal systems, data, models, or processes.
Do not imply endorsement by Snap Inc.
28. GITHUB REPOSITORY
Design the complete repository.
Use a professional naming convention.
Provide:

Repository Name
Exact recommended repository name.

Repository Description
Exact GitHub repository description.

Complete Directory Tree
Provide the entire structure, for example:

repository-name/
│
├── README.md
├── Executive_Summary.md
├── Dashboard_Executive_Summary.md
├── Project_Disclaimer.md
├── LICENSE
├── .gitignore
│
├── docs/
│   ├── business_problem.md
│   ├── methodology.md
│   ├── data_dictionary.md
│   ├── data_architecture.md
│   ├── data_flow.md
│   ├── statistical_methodology.md
│   ├── limitations.md
│   └── job_description_alignment.md
│
├── data/
│   ├── README.md
│   └── synthetic/
│
├── sql/
│   ├── 01_create_datasets.sql
│   ├── 02_create_raw_tables.sql
│   ├── 03_data_quality_checks.sql
│   ├── 04_transform.sql
│   ├── 05_feature_engineering.sql
│   ├── 06_analysis_views.sql
│   ├── 07_dashboard_views.sql
│   └── 08_final_validation.sql
│
├── notebooks/
│   ├── 01_data_generation.ipynb
│   ├── 02_data_validation.ipynb
│   └── 03_statistical_analysis.ipynb
│
├── src/
│   ├── data_generation/
│   ├── validation/
│   └── analysis/
│
├── dashboards/
│   ├── README.md
│   └── dashboard_specification.md
│
├── outputs/
│   ├── figures/
│   └── reports/
│
└── tests/
    └── data_quality_tests.md
Modify the structure if necessary.
Every file included in the final repository must have a defined purpose.
Do not create empty placeholder files unless there is a specific reason.
29. REQUIRED GITHUB DOCUMENTATION
The repository MUST contain at minimum:

README.md
Include:

Project title
Business scenario
Business problem
Objectives
Key questions
Data sources
Synthetic-data disclosure
Architecture
Methodology
Tools
Data flow
Statistical methods
Dashboard
Findings
Recommendations
Limitations
Reproduction instructions
Repository structure
Job-description alignment
Disclaimer
Executive_Summary.md
Write an executive-level summary covering:

Business context
Problem
Approach
Key analytical findings
Business implications
Recommendations
Limitations
Technology stack
Do not invent results.

Dashboard_Executive_Summary.md
Explain:

Dashboard purpose
Audience
Key KPIs
Dashboard pages
Key visualizations
How stakeholders should use the dashboard
Analytical interpretation
Limitations
Project_Disclaimer.md
Provide the complete disclaimer described above.
30. REPRODUCIBILITY
The project must be reproducible by another person.
Provide exact instructions for:

Creating/using the Google Cloud project.
Creating BigQuery datasets.
Running the Colab notebook.
Generating synthetic data.
Saving CSV files.
Uploading/importing CSVs into BigQuery.
Executing SQL scripts in the correct order.
Creating analytical views.
Running statistical analysis.
Connecting Looker Studio.
Refreshing the dashboard.
Reproducing analytical results.
Specify dependencies and package versions where practical.
Do not rely on undocumented manual steps.
31. END-TO-END EXECUTION ORDER
Provide a numbered execution plan with explicit dependencies.
Example:

STEP 01 — Review Job Description
STEP 02 — Define Business Scenario
STEP 03 — Define Analytical Questions
STEP 04 — Design Data Model
STEP 05 — Create Google Cloud Resources
STEP 06 — Create Colab Environment
STEP 07 — Generate/Acquire Data
STEP 08 — Validate Raw Data
STEP 09 — Load BigQuery
STEP 10 — Run SQL Data Quality Checks
STEP 11 — Transform Data
STEP 12 — Engineer Features
STEP 13 — Create Analytical Views
STEP 14 — Run Statistical Analysis
STEP 15 — Validate Results
STEP 16 — Create Dashboard Views
STEP 17 — Build Looker Studio Dashboard
STEP 18 — Document Findings
STEP 19 — Create Executive Summary
STEP 20 — Complete GitHub Repository
STEP 21 — Perform Final QA
STEP 22 — Reproduce Entire Project From Scratch
Adjust the sequence to the actual architecture.
For each step specify:

Objective
Inputs
Actions
Tool
Output
Validation
Dependency
Completion criteria
32. FINAL QUALITY ASSURANCE
Before presenting the final project, perform a complete QA audit.
Check:

Business
Is the business problem realistic?
Is it aligned with the job description?
Is the analytical question measurable?
Data
Are all datasets defined?
Are schemas complete?
Are keys valid?
Is the grain documented?
Are data-quality checks included?
SQL
Is every required query included?
Is the SQL BigQuery-compatible?
Are transformations reproducible?
Are joins validated?
Python
Is every required code block complete?
Are imports included?
Are seeds defined?
Is code executable?
Is memory usage reasonable?
Statistics
Is methodology appropriate?
Are assumptions checked?
Are effect sizes included where appropriate?
Are confidence intervals included where appropriate?
Is causality handled correctly?
Are limitations documented?
Dashboard
Are all pages defined?
Are all KPIs defined?
Are all source views defined?
Are dashboard calculations reproducible?
GitHub
Are all required files included?
Are filenames consistent?
Are instructions complete?
Is the repository reproducible?
Accuracy
Are there unsupported claims?
Are results fabricated?
Are Snap internal data or processes falsely implied?
Are current Google Cloud/Colab limitations verified?
Are assumptions explicitly identified?
33. NO-CONFABULATION / NO-HALLUCINATION REQUIREMENT
This requirement is absolute.
DO NOT CONFABULATE.
DO NOT HALLUCINATE.
Never invent:

Snap internal data
Snap internal metrics
Snap internal systems
Snap internal processes
Snap employee behavior
Snap confidential information
Job responsibilities not present in the provided job description
Public datasets that do not exist
Statistical results that have not been calculated
p-values
confidence intervals
effect sizes
revenue figures
performance improvements
business outcomes
model performance
dashboard results
Google Cloud pricing or quota information that has not been verified
When information is unknown, say:

UNKNOWN — REQUIRES VALIDATION
When an output depends on executing code, say:

EXECUTION-DEPENDENT RESULT — MUST BE GENERATED AFTER RUNNING THE PROVIDED CODE
When an assumption is necessary, label it:

ASSUMPTION
When synthetic data is used, label it:

SYNTHETIC DATA
When an interpretation is inferential rather than directly observed, label it:

INTERPRETATION
34. SOURCE AND VERIFICATION REQUIREMENTS
For current or changing information, verify against authoritative sources.
Prioritize:

Official Snap Inc. sources
Official Google Cloud documentation
Official BigQuery documentation
Official Google Colab documentation
Official Looker Studio documentation
Official GitHub documentation
Original/public dataset documentation
Peer-reviewed or authoritative statistical sources
Do not rely on search-engine snippets as the primary evidence for technical specifications.
Clearly distinguish:

Verified fact
Documentation-derived information
Assumption
Synthetic-data design choice
Analytical result
Interpretation
35. DELIVERABLE MANIFEST
At the end of the response, provide a complete final deliverable manifest.
Use:
#DeliverableFile/LocationPurposeGenerated ByStatus
Include every artifact necessary to reproduce the project.
The final manifest must identify:

GitHub files
SQL scripts
Python/Colab notebooks
CSV files
BigQuery datasets
BigQuery tables
BigQuery views
Looker Studio dashboard
Documentation
Validation artifacts
Statistical outputs
Figures
Executive materials
36. FINAL RESPONSE STRUCTURE
Your final response must be organized in the following order:

Project Title
Executive Project Overview
Snap Job Description Alignment
Business Scenario
Business Problem / Challenges / Bottlenecks
Analytical Questions
Hypotheses
Data Strategy
Data Architecture
BigQuery Architecture
Synthetic Data Design
Complete Python Data-Generation Code
Data Validation Framework
Complete BigQuery SQL
Feature Engineering
Statistical Methodology
Complete Statistical Analysis Notebook Specification
Understanding the Data Flow: From Synthetic Data to Statistical Insights
Looker Studio Dashboard Specification
Insights Framework
Recommendations / Next Steps
Limitations
Complete GitHub Repository Structure
Complete README.md
Complete Executive_Summary.md
Complete Dashboard_Executive_Summary.md
Complete Project_Disclaimer.md
Reproducibility Instructions
End-to-End Execution Checklist
Final QA Checklist
Deliverable Manifest
37. CRITICAL OUTPUT REQUIREMENT
Do not stop at the conceptual design.
Do not provide a high-level project outline and tell me to fill in the rest.
Do not leave:

"...etc."
"add appropriate SQL"
"generate synthetic data"
"perform statistical testing"
"create a dashboard"
"write the README"
"validate the data"
as unresolved tasks.
Instead, provide the actual implementation instructions and code required to perform each task.
Where execution is required and cannot occur inside Gemini, provide the complete executable artifact and the exact execution instructions, then clearly identify the result as execution-dependent.
The project should be sufficiently complete that I can move through the workflow sequentially without having to determine the missing technical steps myself.
38. PORTFOLIO STANDARD
Treat this as a serious professional portfolio project intended to demonstrate Data Scientist Level 4 capability, not as a classroom exercise.
The finished project should demonstrate:

Business acumen
Statistical reasoning
Data engineering awareness
SQL proficiency
Python proficiency
Experimental/causal reasoning where appropriate
Analytical rigor
Data-quality discipline
Visualization
Executive communication
Reproducibility
Documentation
Responsible interpretation
However, do not artificially inflate the complexity.
A simpler methodology that correctly answers the business question is preferable to unnecessary technical complexity.
The guiding principle is:

Use the simplest defensible analytical approach that can answer the business question rigorously, reproducibly, and transparently.
39. FINAL SELF-AUDIT BEFORE RESPONSE
Before producing your final answer, internally verify:
Can another technically competent person follow the instructions from beginning to end without guessing what to do next?
If NO:

identify the missing step
add it
validate its dependency
update the repository structure
update the execution sequence
update the deliverable manifest
Repeat until there are no material process gaps.
Also verify that every major claim is either:

supported by the provided job description,
supported by an authoritative source,
generated by executable analysis,
explicitly labeled as an assumption,
explicitly labeled as synthetic,
or explicitly identified as requiring validation.
The final project must be:
END-TO-END + REPRODUCIBLE + VALIDATED + JOB-DESCRIPTION-ALIGNED + PORTFOLIO-READY + EXECUTIVE-READY + FREE-TIER-CONSCIOUS + NON-HALLUCINATED.
