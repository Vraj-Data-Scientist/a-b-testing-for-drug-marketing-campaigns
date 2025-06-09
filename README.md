
# A/B Testing for Drug Marketing Campaigns

## Project Overview
This project focuses on evaluating the effectiveness of marketing campaigns targeting elderly patients (65+ years) in therapeutic areas such as cardiovascular, neurology, and endocrinology. By leveraging A/B testing, the project compares a new campaign (e.g., video ads emphasizing ease of use) against a standard campaign (e.g., flyers), using prescription uptake as the primary metric. The analysis utilizes a Kaggle Marketing A/B Testing dataset, adapted to simulate healthcare-specific scenarios, and employs Python libraries like Pandas, NumPy, Matplotlib, Seaborn, and SciPy for data processing, statistical testing, and visualization. Additionally, pseudo-code for Snowflake integration demonstrates scalability for production environments.

## Why It’s Helpful in the Domain
In the pharmaceutical and healthcare marketing domain, optimizing campaigns for underserved populations, such as elderly patients, is critical for improving patient engagement and commercial outcomes. This project provides actionable insights to:
- **Enhance ROI**: Identifies which campaign drives higher prescription uptake, enabling cost-effective marketing strategies.
- **Target Specific Populations**: Focuses on elderly patients, addressing their unique needs in therapeutic areas like cardiovascular, neurology, and endocrinology.
- **Support Data-Driven Decisions**: Uses rigorous statistical methods (e.g., t-tests, ANOVA) to ensure reliable conclusions, aligning with industry needs for evidence-based strategies.
- **Scalability**: Incorporates Snowflake integration for handling large-scale healthcare datasets, a key requirement in modern pharmaceutical analytics.

This aligns with roles requiring expertise in data analysis, A/B testing, and statistical modeling to drive commercial strategies, as seen in data science positions within the pharmaceutical industry.

## What It Provides
- **Data Preprocessing**: Cleans and adapts a marketing dataset to simulate healthcare scenarios, including outlier removal and time slot categorization.
- **Statistical Analysis**: Performs A/B testing with t-tests, odds ratios, and ANOVA to compare campaign performance across groups and health conditions.
- **Visualizations**: Generates bar plots to visualize prescription uptake by campaign type, health condition, and time slot.
- **Sample Size Calculation**: Ensures statistical validity by calculating the required sample size for reliable A/B test results.
- **Snowflake Integration**: Provides pseudo-code for loading and sampling data in Snowflake, enabling scalability in production environments.
- **Actionable Insights**: Identifies whether the new campaign significantly improves prescription uptake and explores variations by health condition and time of day.

## Explanation of Results
1. **Dataset Overview (Chunk 16)**:
   - The adapted dataset contains 588,101 records with no missing values, covering columns like `test group`, `converted`, `total ads`, `most ads day`, `most ads hour`, `age`, `health_condition`, and `time_slot`.
   - The `converted` column (0 or 1) indicates prescription uptake, with a mean uptake rate of 2.52%.
   - `total ads` has a mean of 24.82, with a maximum of 61 after outlier removal.
   - The dataset is balanced across health conditions (~33% each for Cardiovascular, Neurology, Endocrinology).

2. **Frequency Tables (Chunk 17)**:
   - `test group`: 96% of users saw the new campaign (`ad`), 4% saw the control (`psa`), reflecting the dataset's imbalance.
   - `most ads day`: Ad exposure is fairly evenly distributed across days, with Friday (15.75%) and Tuesday (13.17%) as the most and least frequent.
   - `health_condition`: Nearly equal distribution across Cardiovascular (33.40%), Endocrinology (33.33%), and Neurology (33.27%), ensuring unbiased analysis across therapeutic areas.

3. **Sample Size Calculation (Chunk 27)**:
   - Required sample size: 5,631 per group, calculated using conversion rates (`p1 = 0.017854` for `psa`, `p2 = 0.025547` for `ad`), significance level (α = 0.05), and power (0.8).
   - Ensures the test can detect a meaningful difference in uptake rates with high confidence.

4. **Group Size Adjustment (Chunk 33)**:
   - The `psa` group (21,328) is smaller than the `ad` group (514,716), so the sample size is adjusted to 5,631 per group to ensure balanced testing.
   - Random sampling with a fixed seed (42) ensures reproducibility.

5. **T-Test (Chunk 28)**:
   - T-statistic: 2.60, P-value: 0.0092 (< 0.05), rejecting the null hypothesis.
   - Indicates a statistically significant difference in prescription uptake between the `ad` and `psa` groups, suggesting the new campaign is more effective.

6. **Odds Ratio (Chunk 49)**:
   - Odds Ratio: 1.52 (95% CI: [1.11, 2.08]), indicating the `ad` group has 1.52 times higher odds of prescription uptake than the `psa` group.
   - The confidence interval excludes 1, reinforcing the significance of the result.

7. **ANOVA for Health Condition (Chunk 50)**:
   - F-statistic: 1.27, P-value: 0.2811 (> 0.05), failing to reject the null hypothesis.
   - Suggests no significant difference in prescription uptake across Cardiovascular, Neurology, and Endocrinology groups, indicating the campaign's effect is consistent across therapeutic areas.

8. **Visualizations (Chunks 42–44)**:
   - **Health Condition Uptake**: Bar plot shows similar uptake rates across health conditions, consistent with the ANOVA result.
   - **Ad vs. PSA Uptake**: The `ad` group has a higher uptake rate than `psa`, visually confirming the t-test result.
   - **Time Slot Uptake**: Uptake rates vary slightly by time slot (Morning, Afternoon, Evening, Night), suggesting potential optimization opportunities for ad scheduling.

## Column Conversions and Additions
- **Converted Columns**:
  - `converted`: Changed from boolean (True/False) to integer (1/0) for numerical analysis and compatibility with statistical tests like t-tests and ANOVA.
  - **Why**: Integer format simplifies calculations (e.g., mean uptake rate) and ensures compatibility with statistical libraries.

- **Added Columns**:
  - `age`: Randomly generated integers (65–90) to simulate elderly patients.
    - **Why**: Aligns the dataset with the target population (elderly patients), enabling healthcare-specific analysis.
  - `health_condition`: Randomly assigned values (Cardiovascular, Neurology, Endocrinology).
    - **Why**: Reflects key therapeutic areas in pharmaceutical marketing, allowing analysis of campaign effectiveness across different patient needs.
  - `time_slot`: Derived from `most ads hour` (categorized into Morning, Afternoon, Evening, Night).
    - **Why**: Enables exploration of ad effectiveness by time of day, critical for optimizing campaign scheduling for elderly patients.

- **Dropped Columns**:
  - `Unnamed: 0`, `user id`: Removed as they were irrelevant identifiers not needed for analysis.
    - **Why**: Reduces noise and focuses on relevant features for A/B testing.

## Why This Project Is Unique
- **Healthcare Focus**: Tailors A/B testing to pharmaceutical marketing for elderly patients, addressing an underserved population with specific needs.
- **Realistic Simulation**: Adapts a general marketing dataset to include healthcare-specific features (age, health condition), making it relevant to the industry.
- **Comprehensive Analysis**: Combines EDA, statistical testing (t-test, ANOVA, odds ratio), and visualizations to provide a holistic evaluation of campaign performance.
- **Scalability**: Includes Snowflake integration pseudo-code, demonstrating how to handle large-scale healthcare data in production environments, aligning with industry tools like Snowflake and Azure.
- **Actionable Insights**: Provides clear, data-driven recommendations for optimizing marketing campaigns, directly applicable to commercial strategies.

## Industry Standards
This project adheres to industry standards in pharmaceutical data science and analytics:
- **Statistical Rigor**: Uses established methods (t-test, ANOVA, odds ratio) with appropriate significance levels (α = 0.05) and power (0.8), ensuring reliable results.
- **Data Cleaning**: Applies standard techniques like outlier removal (IQR method) and categorical encoding (time slots) to ensure data quality.
- **Reproducibility**: Employs random sampling with a fixed seed and saves processed data (`healthcare_marketing_AB.csv`) for transparency.
- **Visualization**: Uses Seaborn and Matplotlib for clear, publication-quality plots, standard in data science communication.
- **Scalability**: Incorporates Snowflake for handling large datasets, aligning with tools used in pharmaceutical analytics (e.g., Snowflake, Azure).
- **Documentation**: Provides detailed explanations of methodology and results, meeting expectations for reproducibility and collaboration in data science roles.

This project is ideal for showcasing skills in data analysis, statistical modeling, and A/B testing, directly relevant to roles requiring data-driven insights in pharmaceutical marketing.

