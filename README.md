# Customer Shopping Behavior Analysis

End-to-end retail analytics project: cleaning and modeling a 3,900-row consumer shopping dataset in Python, answering fourteen business questions in SQL, visualizing the results in an interactive Power BI dashboard, and turning the findings into a stakeholder-ready report and presentation.

## Business Problem

A retail company wants to understand shifting purchasing patterns across demographics, product categories, and sales channels, and to know which factors actually drive purchase decisions and repeat purchases — discounts, reviews, seasons, or payment preferences.

> How can the company leverage consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?

## Dataset

- **3,900** purchase records, **18** columns of customer demographics and shopping behavior
- Only one column had missing data: `Review Rating` (37 nulls)
- Source: `customer_shopping_behavior.csv`

## Repository Contents

| File | Description |
|---|---|
| `customer_shopping_behavior.csv` | Raw dataset |
| `customer_shopping_behavior_analysis.ipynb` | Python data cleaning & feature engineering |
| `customer_shopping_behavior_queries.sql` | 14 business-question SQL queries |
| `customer_shopping_behavior_dashboard.pbix` | Interactive Power BI dashboard |
| `customer_shopping_behavior_report.pdf` | Full written project report |
| `customer_shopping_behavior_presentation.pptx` | Stakeholder presentation |

## Tools Used

Python (pandas), MySQL, Power BI, Word/PowerPoint for the report and slides.

## Data Preparation (Python)

Full pipeline in [`customer_shopping_behavior_analysis.ipynb`](customer_shopping_behavior_analysis.ipynb):

1. **Load & explore** — structure check, summary statistics, null audit
2. **Handle missing data** — imputed `Review Rating` with the category-wise median, rather than a single global fill, so imputed values stay consistent with how each product category tends to be rated
3. **Standardize columns** — lowercase, snake_case
4. **Feature engineering** — `age_group` (quartile-based bands) and `purchase_frequency_days` (numeric interval derived from the categorical purchase-frequency field)
5. **Drop redundant data** — `promo_code_used` was identical to `discount_applied` in every row, so it was dropped
6. **Load to MySQL** — cleaned data written to a `customer_behavior` database via SQLAlchemy, ready for the SQL analysis

> The notebook's database connection cell uses placeholder credentials (`your_username` / `your_password`) — swap in your own local MySQL credentials (or load them from environment variables) before running it.

## SQL Analysis

Fourteen business questions answered in [`customer_shopping_behavior_queries.sql`](customer_shopping_behavior_queries.sql): revenue by gender, discount behavior vs. spend, top-rated and top-selling products, shipping method comparisons, subscription impact, customer segmentation (New/Returning/Loyal), revenue by age group, review rating vs. loyalty, discounts vs. repeat purchases, seasonal patterns, and payment method vs. spend/loyalty.

## Power BI Dashboard

Interactive dashboard in [`customer_shopping_behavior_dashboard.pbix`](customer_shopping_behavior_dashboard.pbix), covering revenue trends, category and seasonal performance, customer segments, and the discount/gender pattern below. Requires Power BI Desktop to open.

## Key Findings

**The business, in five numbers**
- 3.9K customers · $233K total revenue · $59.76 average purchase · 3.75 average review rating · 97.9% of customers have more than one recorded purchase

**Clothing leads by a wide margin.** Clothing generated $104,000 in revenue — nearly half of all category revenue combined (Accessories $74,000, Footwear $36,000, Outerwear $19,000). Top-rated products cluster tightly between 3.78–3.86, with no single standout favorite.

**Of four commonly assumed spend drivers, three show no measurable effect:**
| Factor | Result |
|---|---|
| Review rating | No effect — $58.51 (rating < 3) vs. $60.52 (rating 4+) |
| Discount usage | No positive effect — $59.28 (used) vs. $60.13 (not used) |
| Payment method | No effect — $58.95–$60.92 across 6 methods |
| Subscription status | No effect — $59.49 (subscribed) vs. $59.87 (not) |
| **Season** | **Real effect** — Fall $60,018 vs. Summer $55,777 (~8% gap) |

**The sharpest finding: 100% of discounts went to male customers, 0% to female customers** (Male: 975 no-discount / 1,677 discounted; Female: 1,248 no-discount / 0 discounted). Male customers already generate more than double the revenue of female customers ($157,890 vs. $75,191) — meaning the entire discount budget is concentrated on the segment that needs it least, despite discounts showing no measurable lift in spend or loyalty.

**Fall and Clothing are the real seasonal levers.** Fall ($60,018) outperforms every other season, with Summer ($55,777) the weakest — the only season-over-season gap in the data with a real, defensible size (~8%).

## Recommendations

1. **Audit the discount program.** Discounts show no return and go 100% to male customers — test extending them to female customers, or cut spend where it isn't earning one.
2. **Redesign loyalty around actual behavior.** Subscription status doesn't predict spend or repeat purchases; build tiers on purchase history instead.
3. **Lean into Fall and Clothing.** The one combination in the data with a proven revenue lift — concentrate seasonal marketing and inventory here.
4. **Target Young Adults and Express shippers.** Both segments already show above-average value, making them the clearest place to focus acquisition spend.

## Full Report & Presentation

- [`customer_shopping_behavior_report.pdf`](customer_shopping_behavior_report.pdf) — full written analysis
- [`customer_shopping_behavior_presentation.pptx`](customer_shopping_behavior_presentation.pptx) — stakeholder-facing summary

## How to Run

1. Open `customer_shopping_behavior_analysis.ipynb` and run all cells (installs `pymysql`/`sqlalchemy` if needed) to clean the data and load it into a local MySQL database named `customer_behavior`.
2. Run the queries in `customer_shopping_behavior_queries.sql` against that database.
3. Open `customer_shopping_behavior_dashboard.pbix` in Power BI Desktop to explore the dashboard, or refresh it against your own MySQL connection.

---

## Author

**Simerpreet Kaur**

Data Analyst | Excel • SQL • Power BI • Python

[LinkedIn](https://www.linkedin.com/in/simer-preet-kaur/) · [GitHub](https://github.com/Simer45)
