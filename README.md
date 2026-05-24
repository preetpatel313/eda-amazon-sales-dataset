<div align="center">

# 🛒 Amazon Sales — Exploratory Data Analysis

<p>
  <img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/NumPy-Numerical-013243?style=for-the-badge&logo=numpy&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C72B0?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/TextBlob-NLP-blueviolet?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge"/>
</p>

<p>
  <strong>A full end-to-end Exploratory Data Analysis on 1,465 Amazon India product listings —<br/>
  uncovering pricing patterns, discount behaviour, customer ratings, and NLP-based review sentiment.</strong>
</p>

[📓 View Notebook](./sales.ipynb) · [🌐 View Presentation](https://gamma.app/docs/Amazon-India-Sales-Exploratory-Data-Analysis-cngxvwl95u9x8ui) · [📊 Dataset on Kaggle](https://www.kaggle.com/code/mehakiftikhar/amazon-sales-dataset-eda)

</div>

---

## 📌 Project Overview

This project performs a comprehensive **Exploratory Data Analysis (EDA)** on a real-world Amazon India sales dataset sourced from Kaggle. Raw data was cleaned, transformed, and interrogated across **10 research questions** — covering price distributions, discount strategies, rating patterns, category performance, and TextBlob sentiment classification on customer reviews.

The dataset contains **1,465 products** and **16 features** from Amazon India (`amazon.in`), spanning electronics, accessories, computers, and more.

---

## 🎯 Objectives

| # | Objective |
|---|-----------|
| 1 | 🔍 Profile the dataset — structure, dtypes, missing values, duplicates |
| 2 | 🧹 Clean and preprocess raw data (currency symbols, corrupt values, type conversions) |
| 3 | 💰 Analyse price distributions and the relationship between actual vs. discounted prices |
| 4 | ⭐ Investigate how ratings relate to price, discount, and review count |
| 5 | 🔗 Build a correlation heatmap across all key numeric features |
| 6 | 🏷️ Rank product categories by average customer rating |
| 7 | 💬 Classify customer reviews as Positive / Negative / Neutral using TextBlob NLP |

---

## 🛠️ Technologies Used

| Tool | Version | Purpose |
|------|---------|---------|
| 🐍 Python | 3.10+ | Core language |
| 📓 Jupyter Notebook | Latest | Interactive development environment |
| 🐼 Pandas | 2.x | Data loading, cleaning & manipulation |
| 🔢 NumPy | 1.26+ | Numerical computations |
| 📈 Matplotlib | 3.x | Static charts and visualizations |
| 🎨 Seaborn | 0.13+ | Statistical plots and heatmaps |
| 💬 TextBlob | 0.18+ | NLP-based sentiment analysis |

---

## 📁 Dataset Information

| Attribute | Details |
|-----------|---------|
| **Source** | [Kaggle — Amazon Sales Dataset](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset) |
| **File** | `archive/amazon.csv` |
| **Rows** | 1,465 products |
| **Columns** | 16 features |
| **Region** | Amazon India (₹ INR pricing) |
| **Data Types** | Mixed — cleaned to `float64`, `int64`, and `category` |

### 📋 Key Columns

| Column | Type | Description |
|--------|------|-------------|
| `product_id` | object | Unique Amazon product identifier |
| `product_name` | object | Full product name / title |
| `category` | object | Hierarchical category (pipe-separated levels) |
| `actual_price` | float64 | Original MRP in ₹ (after cleaning) |
| `discounted_price` | float64 | Sale price in ₹ (after cleaning) |
| `discount_percentage` | float64 | Percentage discount applied |
| `rating` | float64 | Average customer rating (0–5) |
| `rating_count` | int64 | Number of customer ratings |
| `about_product` | object | Product description text |
| `review_content` | object | Full customer review text (used for NLP) |

---

## 🔧 Data Cleaning Pipeline

The raw dataset required significant preprocessing before any analysis could begin:

| Step | Issue | Fix Applied |
|------|-------|-------------|
| **1. Currency Formatting** | `actual_price` and `discounted_price` stored as strings with `₹` and `,` | Stripped symbols, cast to `float64` |
| **2. Discount Parsing** | `discount_percentage` stored as `"47%"` strings | Removed `%`, cast to `float64` |
| **3. Corrupt Rating** | One row had `rating = "\|"` (pipe character) | Replaced with `3.9` — verified manually on Amazon.in |
| **4. Missing Values** | `rating_count` had null entries | Filled with **median** (chosen over mean due to right-skewed distribution) |
| **5. Duplicate Check** | Potential duplicate product rows | Verified and removed duplicates |
| **6. Type Encoding** | Categorical columns needed numeric form for correlation | Applied `.cat.codes` encoding |
| **7. Safe Copy** | Avoid mutating the original DataFrame | Created `copydf` as a deep copy for all transformations |

---

## 📊 Analysis & Visualizations

### 1. 💰 Price Distribution
A histogram of `actual_price` reveals the distribution is **highly right-skewed** — the vast majority of products sit in the budget range (₹100–₹500), while a small number of premium products create a long right tail.

### 2. ⚡ Actual Price vs. Rating (Scatter Plot — Log Scale)
Plotting price on a log-scale x-axis against rating shows that products across **all price points receive similarly distributed ratings** — there is no meaningful linear relationship between price and customer satisfaction.

### 3. 🔥 Correlation Heatmap
A Seaborn heatmap across `discounted_price`, `actual_price`, `discount_percentage`, `rating`, and `rating_count` reveals:
- **r = 0.96** — near-perfect positive correlation between `actual_price` and `discounted_price`
- **Weak negative** relationship between `discount_percentage` and prices
- **Negligible correlation** between `rating` and any pricing variable

### 4. 📉 Missing Value Profile
A bar chart of null counts per column confirms that `rating_count` was the **only column with meaningful missing data**, keeping the dataset largely complete.

### 5. 🏷️ Category-wise Rating Analysis
Products are grouped by top-level category and the mean rating per group is computed. **Top 5 highest-rated categories:**

| Rank | Category | Avg. Rating |
|------|----------|-------------|
| 🥇 1 | Tablets | 4.6 ★ |
| 🥈 2 | Network Adapters (LAN) | 4.5 ★ |
| 🥈 2 | Camera Accessories (Film) | 4.5 ★ |
| 🥈 2 | Memory Components | 4.5 ★ |
| 🥈 2 | Streaming Devices | 4.5 ★ |

### 6. 💬 Sentiment Analysis (TextBlob NLP)
TextBlob polarity scores classify each of the 1,465 reviews:

| Sentiment | Count | Share |
|-----------|-------|-------|
| 😊 Positive | 1,438 | 98.2% |
| 😞 Negative | 26 | 1.8% |
| 😐 Neutral | 1 | < 0.1% |

---

## 💡 Key Insights

> 💡 **Insight 1 — Budget-First Market**
> Most Amazon India products are priced in the ₹100–₹500 range. The price distribution is heavily right-skewed, reflecting a price-sensitive consumer base.

> 💡 **Insight 2 — Prices Move Together (r = 0.96)**
> Actual price and discounted price are almost perfectly correlated — higher-priced products receive proportionally similar absolute discounts, not deeper percentage cuts.

> 💡 **Insight 3 — Rating is Price-Independent**
> Customer ratings are largely independent of price. Buyers rate cheap and expensive products with similar satisfaction — quality perception does not scale with cost on this platform.

> 💡 **Insight 4 — Discounts Don't Drive Satisfaction**
> Higher discount percentages show no strong correlation with higher ratings — discounting alone does not appear to improve perceived product quality.

> 💡 **Insight 5 — Category is the Strongest Rating Predictor**
> Category plays the most significant role in determining average ratings, pointing to category-specific customer expectations and product standards.

> 💡 **Insight 6 — Overwhelmingly Positive Sentiment**
> 98.2% of reviews carried positive sentiment — a powerful trust signal reflecting strong overall satisfaction with Amazon India's product ecosystem.

---

## 🚀 Getting Started

### Prerequisites
- Python 3.10 or higher
- `pip` package manager

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/amazon-sales-eda.git
cd amazon-sales-eda
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

Or install manually:

```bash
pip install pandas numpy matplotlib seaborn jupyter textblob
```

### 3. Add the Dataset

Download `amazon.csv` from [Kaggle](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset) and place it at:

```
archive/amazon.csv
```

### 4. Launch the Notebook

```bash
jupyter notebook sales.ipynb
```

Then run all cells: **Kernel → Restart & Run All**

---

## 📂 Project Structure

```
amazon-sales-eda/
│
├── 📓 sales.ipynb             # Main EDA notebook (all analysis + visualizations)
├── 📂 archive/
│   └── amazon.csv             # Raw dataset (download from Kaggle)
├── 📄 requirements.txt        # Python dependencies
└── 📄 README.md               # Project documentation
```

---

## 📈 Sample Visualizations

The notebook produces the following charts:

| # | Chart Type | What It Shows |
|---|-----------|---------------|
| 1 | 📊 Bar chart | Missing value count per column |
| 2 | 📉 Histogram | Distribution of actual & discounted prices |
| 3 | 🔵 Scatter plot (log scale) | Actual price vs. customer rating |
| 4 | 🟥 Correlation heatmap | Relationships between all numeric features |
| 5 | 📦 Horizontal bar | Top categories by average rating |
| 6 | 🥧 Bar chart | Sentiment breakdown (Positive / Negative / Neutral) |

---

## 🔭 Future Improvements

- [ ] 🤖 **Price Prediction Model** — Linear Regression / XGBoost on product features
- [ ] 🌐 **Interactive Dashboard** — Plotly or Dash for dynamic exploration
- [ ] 🔤 **Word Cloud** — Most frequent terms across positive vs. negative reviews
- [ ] 📅 **Time-Series Analysis** — Price and rating trends over time (if date column added)
- [ ] 🏷️ **Sub-category Deep Dive** — Drill into the full hierarchical category tree
- [ ] 🧪 **A/B Simulation** — Discount threshold vs. rating impact analysis

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/your-analysis`
3. Commit your changes: `git commit -m 'Add: sentiment word cloud'`
4. Push to the branch: `git push origin feature/your-analysis`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---


---
### Project Presentation

View the full project presentation here:

https://gamma.app/docs/Amazon-India-Sales-Exploratory-Data-Analysis-cngxvwl95u9x8ui

---

## 🙏 Acknowledgements

- Dataset by [Karkavelraja J on Kaggle](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset)
- Built with ❤️ using Python, Jupyter, and the open-source data science ecosystem

---

<div align="center">

**👤 Author**

**Preet Patel** · [📧 Email](preet313313@gmail.com) · [🔗 LinkedIn](https://www.linkedin.com/in/preet-patel-109559348
) · [💻 GitHub](https://github.com/preetpatel313
)

---

⭐ **If this project helped you, please give it a star — it means a lot!** ⭐

</div>
