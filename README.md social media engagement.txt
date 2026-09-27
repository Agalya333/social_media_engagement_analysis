# Social Media Engagement Data Analysis Pipeline

An end-to-end Python data science project demonstrating data cleaning, feature engineering, exploratory data analysis (EDA), data wrangling, statistical analysis, and data visualization on a 5,000-row social media dataset using Pandas, NumPy, Matplotlib, and Seaborn.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset Description](#dataset-description)
- [Project Architecture & Methodology](#project-architecture--methodology)
- [Key Features & Engineered Metrics](#key-features--engineered-metrics)
- [Statistical & Analytical Highlights](#statistical--analytical-highlights)
- [Tech Stack](#tech-stack)
- [How to Run](#how-to-run)
- [Author & Acknowledgments](#author--acknowledgments)

---

## Project Overview
The objective of this project is to build an automated and robust data pipeline to clean, explore, wrangle, and statistically analyze social media engagement metrics. By handling real-world data issues (missing values, inconsistent formatting, negative values, and text normalization), the pipeline extracts actionable insights regarding content formats, audience sentiments, and geographic performance.

---

## Dataset Description
The dataset contains **5,000 rows** representing individual social media posts across various platforms.

| Attribute | Type | Description |
| :--- | :--- | :--- |
| `posted_at` | Datetime | Timestamp when the post was published |
| `post_type` | Categorical | Content format (e.g., Image, Video, Reel) |
| `country` | Categorical | Geographic region of the post audience |
| `sentiment` | Categorical | Audience reaction (Positive, Neutral, Negative) |
| `hashtags` | Text | Raw string of hashtags included in the post |
| `likes` | Numerical | Count of likes received |
| `comments` | Numerical | Count of comments received |
| `shares` | Numerical | Count of shares received |
| `impressions` | Numerical | Total number of views/impressions |
| `followers` | Numerical | Total follower count of the publisher |

---

## Project Architecture & Methodology

The analytical pipeline is divided into **6 sequential tasks**:

### Task 1: Data Acquisition & Preprocessing
* Loaded raw CSV dataset directly into Python via Google Colab.
* Handled missing numerical values (`likes`, `comments`, `shares`) using median and mode imputation.
* Standardized date parameters (`posted_at`) into Pandas Datetime format (`dayfirst=True`).
* Corrected unrealistically negative metric values using non-negative constraints (`max(0, x)`).

### Task 2: Feature Engineering & Text Cleaning
* **Hashtag Extraction**: Parsed raw hashtag strings to count total hashtags per post (`hashtag_count`).
* **Text Normalization**: Stripped whitespace and standardized text case for categorical columns (`sentiment`, `post_type`).

### Task 3: Data Exploration (EDA)
* Inspected structural parameters using `head()`, `tail()`, `shape`, `dtypes`, and `info()`.
* Evaluated distributions of categorical fields using `value_counts()`, `unique()`, and `nunique()`.
* Generated a full Pearson Correlation Matrix across all numeric attributes.

### Task 4: Data Wrangling
* Merged category mapping tables using `pd.merge()` on relational keys.
* Created engineered domain metrics:
  $$\text{engagement\_score} = \text{likes} + (\text{comments} \times 2) + (\text{shares} \times 3)$$
* Applied log-transformation (`log_likes = np.log1p(likes)`) to reduce skewness in metric distributions.
* Aggregated metrics across `post_type`, `country`, and `sentiment` using `groupby()`.

### Task 5: Statistical Analysis
Computed full descriptive statistical suites across engagement metrics:
* **Central Tendency**: Mean, Median, Mode
* **Dispersion**: Standard Deviation, Variance, Percentiles (25%, 50%, 75%)
* **Distribution Shape**: Skewness and Kurtosis

### Task 6: Visualizations & Insights
* Built visual diagnostics using Seaborn & Matplotlib (Histograms, Bar Charts, Box Plots, Heatmaps).
* Derived business recommendations based on high-performing post categories and demographic engagement trends.

---

## Key Features & Engineered Metrics
1. **`hashtag_count`**: Quantifies hashtag density per post to measure correlation with total reach.
2. **`engagement_score`**: Weighted composite metric prioritizing comments ($2\times$) and shares ($3\times$) over passive likes ($1\times$).
3. **`log_likes`**: Logarithmic transformation allowing stable statistical modeling on highly skewed data.

---

## Tech Stack
* **Language**: Python 3.x
* **Environment**: Google Colab / Jupyter Notebook
* **Libraries**: 
  * `pandas` - Data manipulation & structure analysis
  * `numpy` - Vectorized calculations & transformations
  * `matplotlib` & `seaborn` - Static data visualization

---

## How to Run

1. **Clone or Download Notebook**: Open the `.ipynb` file in Google Colab or Jupyter Notebook.
2. **Install Dependencies** (if running locally):
   ```bash
   pip install pandas numpy matplotlib seaborn