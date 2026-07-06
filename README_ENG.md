# Growth Analytics & Marketing ROI for Ticketing (Showz)

This project analyzes user behavior and marketing channel efficiency for an entertainment ticketing platform (*Showz*). The primary goal is to optimize advertising spend, identify high-value customer cohorts, and generate actionable, data-driven recommendations.

## Project Context

The company wants to understand how customers use the service, when they decide to purchase, how much lifetime value (LTV) they bring, and whether marketing expenses generate a positive return (ROMI). Data spanning visits, orders, and marketing costs from June 2017 to May 2018 was analyzed.

## Methodology and Key Findings

The analysis was structured in four integrated phases, connecting user behavior with the financial performance of marketing channels.

### 1. Exploratory Data Analysis (EDA)
- **Data Cleaning & Structuring:** Corrected data types and removed duplicates.
- **Sessions & Retention:** Identified that most users only visit the platform on a single day (median of 1 active day). Only 19.7% return on distinct days.
- **Intensive Single-Day Users:** Users with multiple sessions on the same day (but who do not return the next day) have a purchase rate of **40.60%**, compared to **10.47%** for single-session users (Z-test, p=0). This is a clear signal of high purchase intent.
- **Session Duration:** Buyers spend significantly more time on the platform than non-buyers (Mann-Whitney U, p<0.0001).
- **Seasonality:** Peaks were detected in November (Black Friday) and troughs in August. The November peak was primarily driven by returning users, who purchased at 44.86% vs. the annual 33.77%.

### 2. Conversion Cohorts
Buyers were segmented by the time elapsed between their first visit and first purchase.
- **C0 (Immediate purchase):** 72.2% of buyers. LTV of $5.92. Strategy: Immediate upselling.
- **C8-30 (8 to 30 days):** Only 6% of buyers, but the most valuable cohort. LTV of $13.47 and average ticket of $7.82. Strategy: Retargeting and reminder campaigns.
- **C30+ (over 30 days):** 13.4% of buyers. Intermediate LTV of $8.04. Strategy: Long-term campaigns and monitoring.

### 3. Marketing Efficiency (CAC and ROMI)
**First-touch attribution** was used to assign revenue to the marketing source that originally brought the user, preventing revenue inflation from multiple sessions.
- **Source 1:** The most profitable channel (ROMI 49%). High retention (2.08 days) and session duration (12.18 min).
- **Source 3:** The most inefficient channel (ROMI -61%). High volume (66k users), but 84% do not purchase, retention is low (1.41 days), and it generates almost no long-term value (C8-30 = 1%).

### 4. Integrated Analysis (Behavioral + Financial)
Behavioral metrics (retention, duration, cohort quality) were cross-referenced with ROMI and CAC for each source to diagnose the root causes of inefficiencies.

## Strategic Recommendations (Prioritized)

| Priority | Channel | Recommendation |
| :--- | :--- | :--- |
| **1 (Eliminate)** | **Source 10** | Eliminate investment (low volume, ROMI -24%). Reallocate budget to Source 1. |
| **1 (Reduce)** | **Source 3** | Reduce investment by 80%. Use the remaining 20% to test new targeting with a success threshold of retention > 1.6 days. Concentrate remaining budget on high-season periods (Black Friday). |
| **2 (Optimize)** | **Source 4** | Optimize landing page to increase immediate conversion (C0) from 10% to 12% to turn ROMI positive. |
| **2 (Investigate)** | **Source 5** | Investigate time-of-day and device distribution. If low-quality traffic, reduce budget by 50%. |
| **3 (Scale)** | **Source 1** | Increase investment. Focus on upselling and cross-selling at checkout. |
| **3 (Maintain)** | **Source 2** | Maintain and apply nurturing (email at days 5 and 15) to push users towards the high-value C8-30 cohort. |
| **3 (Monitor)** | **Source 9** | Maintain minimum budget. This is a late-buyer channel (C30+). Monitor LTV over time. |

## Project Structure

```text
├── datasets/
│   ├── processed/
│   │   ├── cohort_metrics_powerbi.csv
│   │   ├── marketing_analysis_powerbi.csv
│   │   └── user_profile_powerbi.csv
│   ├── costs_us.csv
│   ├── orders_log_us.csv
│   └── visits_log_us.csv
├── growth_analytics_v2.ipynb
├── README_ENG.md
└── README_ESP.md