# Data-Driven Growth Analytics: Optimizing User Cohorts and Marketing ROI for Entertainment Ticketing

## Project Overview
This project performs a comprehensive data analysis for an entertainment ticketing company to understand user behavior and optimize marketing efficiency. The analysis is divided into two operational streams: 
1. **Product & User Behavior Analysis:** Mapping traffic profiles (DAU, WAU, MAU), session dynamics, and time-to-conversion using custom user cohorts.
2. **Marketing Performance Optimization:** Evaluation of customer acquisition costs (CAC) and return on marketing investment (ROMI) across multiple acquisition channels to optimize budget allocation.

The primary goal is to determine how users interact with the platform, identify when and why they convert, and establish which marketing sources yield the highest structural return.

## Dataset Architecture
The analysis relies on three interconnected datasets covering the period from **June 2017 to May 2018**:

* **`visits_log_us.csv` (Server Logs):** Website interaction records.
  * `uid`: Unique user identifier.
  * `device`: User device type (desktop/touch).
  * `start_ts` / `end_ts`: Session start and end timestamps.
  * `source_id`: Marketing channel id from which the session originated.
* **`orders_log_us.csv` (Transactional Data):** Platform purchases.
  * `uid`: Unique user identifier.
  * `buy_ts`: Transaction timestamp.
  * `revenue`: Order value in fiat currency.
* **`costs_us.csv` (Marketing Costs):** Ad spend statistics.
  * `source_id`: Marketing channel identifier.
  * `dt`: Date of the expenditure.
  * `costs`: Total amount spent on that day for the specific channel.

## Tech Stack & Libraries
* **Language:** Python 3.x
* **Data Manipulation:** Pandas, NumPy
* **Data Visualization:** Matplotlib, Seaborn

## Data Pipeline & Preprocessing
To ensure analytical integrity, the raw data underwent rigorous preprocessing:
* **Case Standardization:** Standardized all column headers across datasets to `lower_snake_case`.
* **Type Casting:** Converted object/string representations of timestamps (`start_ts`, `end_ts`, `buy_ts`, `dt`) into explicit `datetime64[ns]` formats.
* **Feature Engineering:** Calculated explicit `session_duration` metrics in minutes and derived categorical time-based flags for cohorts.

---

## Key Metrics & Analytical Findings

### 1. Exploratory Data Analysis & Product Dynamics
* **User Traffic Volumes:**
  * **Daily Active Users (DAU):** Average of **908** unique users (Peaking at 3,319).
  * **Weekly Active Users (WAU):** Average of **5,716** unique users (Peaking at 10,586).
* **Session Frequencies & Engagement:**
  * On average, users generate **1.58 sessions** within the active lifecycle. 
  * Only **22.8%** of the user base constitutes returning users (52,128 out of 228,169 unique IDs), pointing toward an activation or retention barrier.
  * **Session Duration Distribution:** Heavily right-skewed. While anomalous multi-hour sessions exist, filtering out extreme outliers (sessions $\le$ 99 minutes) shows that the vast majority of interactions are brief and highly intent-driven.
* **Seasonality Trends:**
  * Strong cyclical performance tied to seasonal demand. Traffic peaks sharply during the late Q4 holiday season (October–December), with November recording the highest historical volume of unique monthly interactions. 
  * Conversely, late summer (August) and mid-spring (April) experience dramatic traffic contractions.

### 2. Time-to-Conversion & Cohort Analysis
Users were grouped into discrete cohorts based on their velocity to purchase, defined as the lag between their first platform touchpoint (`start_ts`) and their first completed transaction (`buy_ts`):

| Cohort Name | Conversion Velocity Window | Unique Users | % Share | Orders / User | Avg. Ticket ($) | Total Revenue ($) | User LTV ($) |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **C0** | Immediate (Day 0) | 26,363 | 72.2% | 1.30 | 4.56 | 156,075.98 | **5.92** |
| **C1** | 1 Day Delay | 1,011 | 2.8% | 1.79 | 5.90 | 10,684.87 | **10.57** |
| **C2-7** | 2 to 7 Days | 2,069 | 5.7% | 1.67 | 4.79 | 16,534.65 | **7.99** |
| **C8-30** | 8 to 30 Days | 2,178 | 6.0% | 1.72 | 7.82 | 29,330.54 | **13.47** |
| **C30+** | Greater than 30 Days | 4,902 | 13.4% | 1.46 | 5.50 | 39,431.16 | **8.04** |

**Cohort Takeaways:**
* **High Frictionless Intent:** **72.2%** of converting users make a purchase *immediately on Day 0* (`C0`). While they represent the core volume, their LTV ($5.92) is the lowest across all groups.
* **The High-Value Lurkers:** Users who convert between 8 to 30 days (`C8-30`) demonstrate outstanding transactional health, yielding the highest average ticket ($7.82) and an LTV of **$13.47**. This indicates a high-intent research phase that pays off in larger basket sizes.

### 3. Marketing Performance & Multichannel ROI
By mapping cross-dataset interactions, customer acquisition costs (CAC) and Return on Marketing Investment (ROMI) were isolated per acquisition channel (`source_id`):

| Source ID | Total Spend ($) | Unique Users Generated | Unit CAC ($) | Total Revenue Attributed ($) | ROMI (%) | Operational Tier |
| :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **1** | 20,833.27 | 18,999 | 1.10 | 2,298,200.17 | **10,931.4%** | Highly Recommended (High Efficiency) |
| **2** | 42,806.04 | 26,245 | 1.63 | 2,638,189.21 | **6,063.1%** | Highly Recommended (Maximum Scale) |
| **5** | 51,757.10 | 56,974 | 0.91 | 1,181,477.14 | **2,182.7%** | Highly Recommended (Balanced Growth) |
| **4** | 61,073.60 | 83,525 | 0.73 | 496,690.17 | **713.3%** | Moderate Performance (Niche Scale) |
| **9** | 5,517.49 | 9,264 | 0.60 | 36,342.25 | **558.7%** | Moderate Performance (Low Cost/Vol) |
| **10** | 5,822.49 | 8,067 | 0.72 | 14,619.23 | **151.1%** | Moderate Performance (Low Return) |
| **3** | 141,321.63 | 74,756 | 1.89 | 296,687.96 | **109.9%** | Weak Performance (Highly Inefficient) |
| **6 / 7** | *No Spend Data* | 40 | N/A | 1.22 | N/A | Non-evaluable / Organic |

---

## Strategic Business Recommendations

1. **Reallocate Capital from Source 3 to Sources 1, 2, and 5:** * **Source 3** commands the highest total budget allocation ($141.3K) but operates at a near-break-even ROMI of just **109.9%**, dragging down overall corporate margins. 
   * Defunding Source 3 and shifting budget to **Sources 1, 2, and 5** will maximize revenue velocity, as these three channels combine vast market scale, low-to-moderate unit CAC, and exceptional exponential returns (exceeding 2,000% ROMI).
2. **Implement Off-Season Counter-Cyclical Promotions:**
   * To mitigate severe structural revenue dips in August and April, the marketing team should roll out early-bird seasonal passes or bundle promotions during these months to artificially stabilize cash flow.
3. **Nurture and Upsell the Immediate Conversion Funnel (`C0`):**
   * Since 72.2% of your converted user base purchases instantly but exits with a low individual average ticket ($4.56), look into introducing cross-selling mechanisms, checkout add-ons (e.g., event insurance, VIP upgrades), or post-purchase trigger emails within 24 hours to drive secondary transactions and expand their structural LTV.
4. **Deploy Retargeting Campaigns for the Mid-Funnel (`C8-30`):**
   * Given that users who take 8 to 30 days to convert spend the most money per ticket ($7.82), dedicate a slice of the low-cost acquisition budget (via Source 4 or 9) to retarget users who visited the site 7 days ago but haven't checked out yet. Their high basket values justify targeted email and display-ad retargeting workflows.

## Project Structure

├── datasets/
│   ├── visits_log_us.csv       # Platform interaction logs
│   ├── orders_log_us.csv       # Purchase transactional logs
│   └── costs_us.csv            # Multi-channel marketing costs
├── notebook.ipynb              # Full Jupyter Notebook analysis (Spanish text/code)
└── README.md                   # Executive English summary for portfolio display