# eda-amazon-sales-dataset
# Amazon Sales Dataset EDA  Exploratory Data Analysis project using Python, Pandas, Matplotlib, and Seaborn.
# 📦 Amazon Sales — Exploratory Data Analysis

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jupyter-Notebook-orange?style=for-the-badge&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C72B0?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge"/>
</p>

---

## 📌 Project Overview

This project performs a comprehensive **Exploratory Data Analysis (EDA)** on an Amazon Sales Dataset sourced from Kaggle. The goal is to uncover meaningful patterns in pricing, discounts, customer ratings, and product categories — providing actionable insights into how Amazon's product ecosystem is structured and how customers respond to it.

The dataset contains **1,465 rows** and **16 columns**, covering product metadata, pricing, discount information, ratings, and customer reviews from Amazon India (amazon.in).

---

## 🎯 Objectives

- 🔍 Understand the structure and quality of the Amazon sales dataset
- 🧹 Clean and preprocess raw data (handle currency symbols, missing values, type conversions)
- 📊 Visualize the distribution of prices, discounts, and ratings
- 🔗 Identify correlations between key numeric variables
- 🏷️ Analyse product performance across different categories
- 💡 Extract actionable insights that could inform business decisions

---
## Project Presentation

View the full project presentation here:

https://gamma.app/docs/Amazon-India-Sales-Exploratory-Data-Analysis-cngxvwl95u9x8ui

---

## 🛠️ Technologies Used

| Tool | Purpose |
|---|---|
| 🐍 Python 3.10+ | Core programming language |
| 📓 Jupyter Notebook | Interactive development environment |
| 🐼 Pandas | Data manipulation and analysis |
| 🔢 NumPy | Numerical computations |
| 📈 Matplotlib | Static data visualizations |
| 🎨 Seaborn | Statistical data visualizations |

---

## 📁 Dataset Information

| Attribute | Details |
|---|---|
| **Source** | Kaggle — Amazon Sales Dataset |
| **File** | `archive/amazon.csv` |
| **Rows** | 1,465 products |
| **Columns** | 16 features |
| **Data Types** | Mixed (object → cleaned to float/category) |

### 📋 Key Columns

| Column | Description |
|---|---|
| `product_id` | Unique product identifier |
| `product_name` | Name of the product |
| `category` | Product category hierarchy |
| `actual_price` | Original listed price (₹) |
| `discounted_price` | Price after discount (₹) |
| `discount_percentage` | Percentage discount applied |
| `rating` | Average customer rating (0–5) |
| `rating_count` | Number of customer ratings |
| `about_product` | Product description |
| `review_title / review_content` | Customer reviews |

---

## 🔧 Data Cleaning Steps

The raw dataset required significant preprocessing before analysis:

1. **Currency Conversion** — Stripped `₹` symbols and commas from `actual_price` and `discounted_price`, then cast to `float`
2. **Discount Parsing** — Removed `%` from `discount_percentage` and converted to `float`
3. **Rating Fix** — Identified a corrupt `|` rating value; replaced it with `3.9` (verified on Amazon.in)
4. **Missing Values** — Filled missing `rating_count` values using the **median** (chosen over mean due to right-skewed distribution)
5. **Duplicate Check** — Verified and handled any duplicate rows
6. **Type Encoding** — Encoded categorical columns using `.cat.codes` for correlation analysis

---

## 📊 Analysis & Visualizations

### 1. 💰 Price Distribution
A histogram of `actual_price` reveals the distribution is **highly right-skewed** — the vast majority of products are priced in the lower range, while a small number of premium products push the tail rightward.

### 2. ⚡ Actual Price vs. Rating (Scatter Plot)
A scatter plot on a log-scale x-axis shows that products across all price ranges receive similarly distributed ratings — there is **no strong linear relationship** between price and customer satisfaction.

### 3. 🔥 Correlation Heatmap
A Seaborn heatmap across `discounted_price`, `actual_price`, `discount_percentage`, `rating`, and `rating_count` reveals:
- **Very strong positive correlation (0.96)** between `actual_price` and `discounted_price`
- **Weak negative relationship** between `discount_percentage` and prices
- **Negligible correlation** between ratings and pricing variables

### 4. 🏷️ Category-wise Rating Analysis
Products are grouped by category, and the mean rating per category is computed to identify which product segments consistently earn higher or lower customer satisfaction.

### 5. 📉 Missing Value Analysis
A bar chart visualises the count of null values per column, confirming that `rating_count` was the only column with meaningful missing data.

---

## 💡 Key Insights

> **1.** 🛒 Most Amazon products are budget-friendly — the price distribution is heavily skewed toward lower price points, with very few luxury/premium listings.

> **2.** 🔗 Actual price and discounted price move almost in lockstep (r = 0.96), suggesting that higher-priced products receive proportionally similar discounts.

> **3.** ⭐ Customer ratings are largely independent of price — buyers rate cheap and expensive products with similar satisfaction levels.

> **4.** 📉 Higher discount percentages are not strongly associated with higher ratings — discounting alone may not be driving purchase satisfaction.

> **5.** 🏷️ Category plays a significant role in determining average ratings, pointing to category-specific customer expectations.

---

## 🚀 Getting Started

### Prerequisites

Make sure you have Python 3.10+ installed and the required libraries.

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/amazon-sales-eda.git
cd amazon-sales-eda
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

Or install manually:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### 3. Add the Dataset

Download the Amazon Sales Dataset from [Kaggle](https://www.kaggle.com/) and place it at:

```
archive/amazon.csv
```

### 4. Run the Notebook

```bash
jupyter notebook sales.ipynb
```

---

## 📂 Project Structure

```
amazon-sales-eda/
│
├── archive/
│   └── amazon.csv          # Raw dataset (download from Kaggle)
│
├── sales.ipynb             # Main EDA notebook
├── requirements.txt        # Python dependencies
└── README.md               # Project documentation
```

---

## 📈 Future Improvements

- [ ] 🤖 Build a **price prediction model** using regression (e.g., Linear Regression, XGBoost)




## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/new-analysis`)
3. Commit your changes (`git commit -m 'Add sentiment analysis'`)
4. Push to the branch (`git push origin feature/new-analysis`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- Dataset sourced from [Kaggle — Amazon Sales Dataset](https://www.kaggle.com/)
- Inspired by the open-source data science community
- Built with ❤️ using Python and Jupyter Notebook

---

<p align="center">
  ⭐ If you found this project helpful, please consider giving it a star!
</p>
