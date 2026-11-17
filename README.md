# Marketing Attribution & A/B Test Analysis

This repository contains solutions for two Data Analyst tasks: estimating unattributed user registrations across ad channels and evaluating an A/B test on email notification frequency for a digital comics platform.

## Repository Structure

* `registration_attribution.ipynb` — Linear regression modeling and diagnostics to estimate unattributed registrations per marketing channel.
* `evaluating_ab_test.ipynb` — Statistical evaluation, CUPED variance reduction, bootstrap confidence intervals, and risk assessment for an email frequency A/B test.

---

## Task 1: Marketing Registration Attribution

### Problem
Due to browser privacy settings and anti-trackers, a portion of user registrations cannot be directly attributed to a specific ad source. The goal is to estimate what percentage of total registrations from each channel (**Google, Facebook, TikTok, Snapchat**) end up as "unattributed."

### Approach & Diagnostics
* **Modeling:** Built an Ordinary Least Squares (OLS) linear regression model without an intercept (`fit_intercept=False`, since zero traffic means zero unattributed users) and non-negative constraints.
* **Diagnostics:** Checked statistical significance ($p$-values), model fit ($R^2$), multicollinearity (VIF), and coefficient stability over time using a 30-day rolling window.

### Key Findings
* **TikTok:** **20.77%** unattributed (p < 0.05) — highest attribution gap among all channels.
* **Google:** **12.74%** unattributed (p < 0.05) — stable and consistent over time.
* **Facebook:** **6.42%** unattributed (p < 0.05) — most reliable tracking among channels.
* **Snapchat:** Statistically insignificant (p = 0.866) and unstable over time; excluded from attribution conclusions.
* **Recommendation:** Implement server-side tracking or enhanced conversions for TikTok to close the attribution gap.

---

## Task 2: Email Frequency A/B Test Evaluation

### Problem
An online comics platform ran an A/B test from **August 1 to August 25** where the test group (**Group B**) received **2x more email notifications** (updates, recommendations, promos) than the control group (**Group A**). The goal is to evaluate the impact on revenue and engagement and provide a business recommendation.

### Approach & Diagnostics
* **Pre-Test & Sample Checks:** Compared historical pre-test revenue and conversion rates between groups.
* **Statistical Testing:** Evaluated ARPU (Average Revenue Per User), conversion rate, visits, and episodes read using t-test and Z-test for proportions.
* **Variance Reduction & Risk Checks:** Applied **CUPED** using pre-test revenue, calculated 95% confidence intervals via **Bootstrap** (due to heavy zero-inflation and "whale" outliers), and checked **ARPPU** (average check of paying users) to assess monetization risks.

### Key Findings
* **Engagement vs. Sales:** Doubling email frequency successfully boosted user engagement (visits and episodes read), **but did not lead to a statistically significant increase in sales or ARPU**.
* **Confidence & Risk:** The 95% bootstrap confidence interval for revenue difference (`[-0.47, 0.59]`) spans across zero, and ARPPU showed no uplift (p = 0.278).
* **Recommendation:** Continue scaling email outreach to drive content engagement, but shift focus toward optimizing **in-app monetization and promotional offers** so that higher reading activity converts into actual purchases.

---

## Tools Used
* **Python**
* `pandas`, `numpy` — data cleaning and aggregation
* `statsmodels`, `scipy` — OLS regression, hypothesis testing
* `scikit-learn` — constrained linear regression & rolling window checks
* `matplotlib`, `seaborn` — visualizations


**Contributor**: Yelyzaveta Tretiak
