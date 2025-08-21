# A/B Landing Page Testing: Conversion Analysis & Insights

[![Releases](https://img.shields.io/badge/Releases-Download-blue?logo=github)](https://github.com/annonymous855/AB-Testing/releases)

📊 🔬 🎯

Table of contents
- About
- Dataset
- Analysis plan
- Key metrics
- Statistical methods
- Results at a glance
- Visuals
- Reproduce the analysis
- Project files
- Requirements
- Tips for extension
- Topics & links
- License & contact

About
This repository holds a full analysis of an A/B test for a landing page. The test compares a control page (old) and a treatment page (new). The goal is to check whether the new page changes user conversion. The work covers data checks, exploratory plots, statistical tests, and bootstrap checks for robustness.

Dataset
The dataset records visits and conversions. Each row is one user session. Core fields:
- user_id — unique user identifier
- timestamp — visit date and time
- group — experiment group: control or treatment
- landing_page — old_page or new_page
- converted — 0 for no, 1 for yes

The data lets us measure conversion per group and test the difference between groups. We also inspect data quality and alignment between group assignment and page shown.

Analysis plan
1. Data audit
   - Confirm unique user IDs
   - Find missing fields and timestamps
   - Check if group and landing_page match expected mapping
2. Descriptive metrics
   - Count users per group
   - Count conversions per group
   - Compute conversion rates
3. Visual exploration
   - Time series of conversions
   - Conversion rate bar chart
   - Distribution of session times
4. Statistical tests
   - Two-proportion z-test for difference in conversion rates
   - Bootstrap confidence intervals for rate difference
   - Logistic regression for adjusted effect (optional)
5. Robustness
   - Check for duplicate users
   - Run sensitivity with and without borderline entries
6. Report
   - Present p-value, effect size, and confidence interval
   - Provide plots and code to reproduce

Key metrics
- Users per group: sample size matters for power
- Conversions: raw counts
- Conversion rate: conversions / users
- Lift: (rate_treatment - rate_control) / rate_control
- Absolute difference: rate_treatment - rate_control
- p-value: test whether difference can be due to chance
- 95% CI: plausible range for the difference

Statistical methods
- Two-proportion z-test
  - Tests if the conversion rates differ
  - Works with large samples
  - Reports p-value and z-statistic
- Bootstrap
  - Resamples sessions with replacement
  - Computes distribution of rate differences
  - Gives non-parametric confidence interval
- Logistic regression
  - Models conversion ~ group (+ covariates)
  - Provides odds ratio and p-value
- Multiple testing
  - If you run many tests, adjust p-values
  - Use Bonferroni or Benjamini-Hochberg as needed

Results at a glance
- Sample sizes: control = ~N_control, treatment = ~N_treatment
- Conversion rates: control ≈ X%, treatment ≈ Y%
- Absolute lift: ≈ (Y - X) percentage points
- Relative lift: ≈ ((Y - X) / X) * 100%
- p-value: see statistical section below
- Bootstrap 95% CI: lower → upper

The exact numbers appear in the results notebook and the release artifact. Download the release package to view the final report and code.

Visuals
Images help to see patterns. The repo includes:
- Conversion rate bar charts
- Time trends of conversions
- Bootstrap distribution plots
- Heatmaps for hourly/daily patterns

Example image from Unsplash (for visual header):
![Landing Page A/B Test](https://images.unsplash.com/photo-1515377905703-c4788e51af15?ixlib=rb-4.0.3&w=1200&q=80)

Sample plots are in the visuals folder in the release asset.

Reproduce the analysis
Use the release to run the full analysis on your machine.

[Download the release and run the analysis](https://github.com/annonymous855/AB-Testing/releases)  
The releases page contains the analysis bundle. Download the file named ab_testing_release.zip and extract it. Then run the main script:

1. Extract
   - unzip ab_testing_release.zip
2. Install environment
   - pip install -r requirements.txt
3. Run
   - python run_analysis.py --data data/ab_test_data.csv --out results/

run_analysis.py will:
- Load the CSV
- Run data checks and EDA
- Produce plots in results/plots
- Run z-test, bootstrap, and logistic regression
- Save a report results/report.md and figures

If the link does not load, check the Releases section of this repository for the package.

Project files
- data/
  - sample dataset used for tests (CSV)
- notebooks/
  - 01_EDA.ipynb — exploratory analysis and plots
  - 02_stats.ipynb — hypothesis tests and bootstrap
- scripts/
  - run_analysis.py — orchestrates the full pipeline
  - utils.py — helper functions for tests and plots
- results/
  - report.md — human-readable report
  - plots/ — PNG figures
- README.md — this file

How the code flows
- run_analysis.py reads the CSV into pandas
- It validates group assignments and removes duplicates
- It computes conversion counts and rates
- It runs a z-test using statsmodels or scipy
- It runs bootstrap sampling with numpy
- It fits a logistic regression with statsmodels for an adjusted check
- It writes outputs to results/

Command examples
- quick view of conversion rates (Python REPL)
  - from scripts.utils import summary_rates
  - summary_rates('data/ab_test_data.csv')
- run full pipeline
  - python scripts/run_analysis.py --data data/ab_test_data.csv --out results/

Requirements
- Python 3.8+
- pandas
- numpy
- scipy
- statsmodels
- seaborn
- matplotlib
- jupyter (if you want to open notebooks)

Install
- pip install -r requirements.txt

Best practices applied
- Check randomization: confirm groups balance on size
- Check alignment: group assignment vs. landing_page value
- Remove duplicates: ensure unique user_id per test window
- Use both parametric and non-parametric tests
- Report effect size and CI, not only p-value
- Save raw outputs and plots for audit

Extensions and experiments
- Add covariates (country, device, traffic source) to regression
- Run sequential analysis with corrected thresholds
- Apply Bayesian A/B test for posterior probability of improvement
- Use multi-armed bandit for adaptive allocation
- Test different metrics (time on page, revenue per user)

Badging and topics
Badges:
[![Releases](https://img.shields.io/badge/Releases-Download-blue?logo=github)](https://github.com/annonymous855/AB-Testing/releases)

Topics:
ab-testing, analysis, bootstrap, eda, matplotlib, numpy, p-value, pandas, python, scipy, seaborn, statsmodels, z-test

License
This project uses the MIT License. See LICENSE for details.

Contact
If you found an issue or want to suggest an analysis, open an issue or submit a pull request. The notebooks show step-by-step calculations to make review simple.

Image credits
- Unsplash photo used under the Unsplash license: https://unsplash.com/

Releases
Visit the Releases page to download the analysis package. The release contains the code, data sample, and final report. Download ab_testing_release.zip and run the included script to reproduce all figures and tables.

[Get the release here](https://github.com/annonymous855/AB-Testing/releases)