# Online Sports Store Revenue Analysis – Data-Driven Business Insights

##  Project Overview
The **global sports apparel industry** is a multi-billion-dollar market with rapid growth potential. To remain competitive, **data-driven decision-making** is critical for online sports retailers.

This project was conducted for an **online sportswear retailer**, focusing on **revenue optimization, pricing strategy, and customer engagement analysis**. Using **real-world data**, we analyzed **product sales, pricing impact, and customer sentiment**.

### 🎯 Business Goals:
- **📊 Revenue Optimization** – Identify the best pricing strategy for maximizing revenue.
- **📈 Customer Engagement** – Understand how product descriptions impact ratings and reviews.
- **🏆 Competitive Benchmarking** – Compare sales performance between Adidas and Nike.
- **📣 Marketing Insights** – Provide actionable strategies for boosting conversions.

---

## 📂 Datasets Used
This analysis was performed using **four datasets**, each providing unique business insights.

| **Dataset**  | **Description** |
|-------------|----------------|
| `brands.csv` | Contains **product_id** and **brand name** (Nike, Adidas, etc.). |
| `finance.csv` | Includes **listing price, discount, sale price, and revenue** per product. |
| `info.csv` | Stores **product names and descriptions**. |
| `reviews.csv` | Contains **average ratings and the number of reviews** per product. |

**Merging Strategy:**  
All datasets were merged using **`product_id`** to create a **unified dataset** for analysis.

---

## 🛠 Tools & Technologies Used

| **Category** | **Tools & Methods** |
|-------------|--------------------|
| **Data Processing** | `pandas` for data merging and cleaning |
| **Exploratory Data Analysis (EDA)** | `matplotlib`, `seaborn` for visualization |
| **Feature Engineering** | `pd.qcut()` for price segmentation |
| **Statistical Analysis** | `groupby()`, `agg()` for revenue and rating calculations |
| **Data Binning** | `pd.cut()` for categorizing descriptions into length intervals |

---

## 🔀 Methodology & Business Impact

### 1️⃣ Data Preparation
- **Loaded datasets** using `pandas`.
- **Merged data** with **inner joins** on `product_id` for completeness.
- **Removed null values** to maintain data quality.

📌 **Impact:** Ensured **high data integrity** for reliable business insights.

---

### 2️⃣ Sales Performance Analysis (Adidas vs. Nike)
- **Segmented products** into **pricing quartiles**:
  - **Budget**
  - **Average**
  - **Expensive**
  - **Elite**
- **Grouped by brand** (`Nike`, `Adidas`) and **price category**.
- **Calculated**:
  - 📦 **Number of Products Sold**
  - 💰 **Mean Revenue Per Category**

📌 **Impact:** Identified **optimal pricing strategies** that maximize sales.

---

### 3️⃣ Product Description Length vs. Customer Sentiment
- **Measured description length** using `.str.len()`.
- **Created bins** for descriptions at **100-character intervals**.
- **Grouped by description length** to analyze:
  - ⭐ **Average Rating**
  - 💬 **Total Reviews**

📌 **Impact:** Revealed how **content length affects customer perception and purchase decisions**.

---

## 📊 Key Findings & Business Recommendations

### 🔥 Key Takeaways:
1. **💲 Pricing Impacts Sales Volume**
   - **Budget-priced** products drive **higher sales**.
   - **Elite** products generate **higher revenue per unit** but have **lower sales volume**.
   - **Optimal price range** for Adidas & Nike lies in the **Average** category.

2. **✍️ Product Descriptions Affect Ratings**
   - **Short descriptions (100-200 characters)** receive **higher ratings**.
   - **Long descriptions (400+ characters)** tend to get more reviews but **lower ratings**.
   - **Actionable:** Use **concise** and **bullet-pointed descriptions** to boost conversions.

3. **📣 Strategic Discounting & Bundling**
   - Discounts **boost conversions**, but deep discounts **hurt profit margins**.
   - **Bundling** (e.g., shoes + socks) increases order value.

---

## 🎯 Business Recommendations

✔ **Reposition Pricing Strategy**  
- Focus on **"Average" price category** for **Nike & Adidas** to maximize sales.
- **Reduce deep discounts** on **Elite** products to maintain exclusivity.

✔ **Optimize Product Descriptions**  
- Keep descriptions **concise (100-200 characters)** for **higher ratings**.
- Use **bullet points** instead of long paragraphs.

✔ **Leverage Customer Reviews for Trust**  
- **Encourage reviews** via **email follow-ups** and **loyalty incentives**.
- Prioritize **top-rated products** in **advertising campaigns**.

✔ **Personalized Marketing for High-Value Shoppers**  
- Offer **Elite-tier customers** early access to premium collections.
- **AI-driven recommendations** to improve customer retention.

---

## 🔢 Key Code Snippets
### **Merging Data (Inner Join on `product_id`)**
```python
import pandas as pd

# Load datasets
brands = pd.read_csv("brands.csv")
finance = pd.read_csv("finance.csv")
info = pd.read_csv("info.csv")
reviews = pd.read_csv("reviews.csv")

# Merge datasets using INNER JOIN on 'product_id'
merged_df = info.merge(finance, on="product_id", how="inner")
merged_df = merged_df.merge(reviews, on="product_id", how="inner")
merged_df = merged_df.merge(brands, on="product_id", how="inner")

# Drop missing values
merged_df.dropna(inplace=True)
```
```
Analyzing Sales Performance

# Categorize products into price quartiles
merged_df["price_label"] = pd.qcut(
    merged_df["listing_price"], q=4, labels=["Budget", "Average", "Expensive", "Elite"]
)

# Group by brand and price category
adidas_vs_nike = merged_df.groupby(["brand", "price_label"], as_index=False).agg(
    num_products=("price_label", "count"),
    mean_revenue=("revenue", "mean")
).round(2)

print(adidas_vs_nike)
```
```
Product Description Length vs. Ratings

# Compute description length
merged_df["description_length"] = merged_df["description"].str.len()

# Create bins for description length
bins = list(range(0, 800, 100))  # Bins of 100-character intervals
labels = [str(x) for x in bins[1:]]

# Assign labels based on bins
merged_df["description_length"] = pd.cut(
    merged_df["description_length"], bins=bins, labels=labels
)

# Group by description length
description_lengths = merged_df.groupby("description_length", as_index=False).agg(
    mean_rating=("rating", "mean"),
    total_reviews=("reviews", "sum")
).round(2)

print(description_lengths)
```
📎 References

    Source: https://www.statista.com/statistics/254489/total-revenue-of-the-global-sports-apparel-market/
    Python Libraries Used: pandas, matplotlib, seaborn
    Business Intelligence Insights: Data-driven pricing & marketing strategies

🏁 Conclusion

This project provided real-world insights into pricing, customer behavior, and marketing strategies for an online sports retailer. The findings empower business teams to make data-backed decisions, optimizing sales strategies and customer engagement.

The next step involves building a machine learning model for dynamic pricing recommendations and real-time revenue forecasting.

📢 Interested in the full dataset and code?
Check out the full project on GitHub: 
