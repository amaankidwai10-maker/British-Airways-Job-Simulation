# British-Airways-Job-Simulation
# British Airways Customer Review Analysis

> **Analyzing 3,926 customer reviews to uncover what makes passengers recommend — or avoid — British Airways.**

![Wordcloud](wordcloud.png)

---

## 📌 Project Overview

British Airways (BA) is the flag carrier airline of the United Kingdom and one of the largest airlines in Europe. With thousands of flights operating daily, customer satisfaction plays a critical role in the airline's reputation and revenue.

In this project, I analyzed **3,926 real customer reviews** collected from [Skytrax](https://www.airlinequality.com/airline-reviews/british-airways) — one of the most trusted airline review platforms in the world. The dataset contains detailed ratings across multiple service dimensions including seat comfort, food, cabin staff, entertainment, and overall value for money.

The project is divided into two parts:
- **Part 1 — Exploratory Data Analysis (EDA):** Understanding the data through visualizations and statistics
- **Part 2 — Machine Learning:** Building a model to predict whether a customer will recommend British Airways

---

## 📂 Dataset

| Column | Description |
|---|---|
| Name | Reviewer name |
| Date | Date of review |
| Location | Country of reviewer |
| Full Review | Complete review text |
| Rating | Overall rating (1–10) |
| Seat Comfort | Seat comfort rating |
| Cabin Staff Service | Staff service rating |
| Food & Beverages | Food quality rating |
| Inflight Entertainment | Entertainment rating |
| Ground Service | Ground service rating |
| Value For Money | Value for money rating |
| Recommended | Whether customer recommends BA (yes/no) |
| Type Of Traveller | Business / Leisure / Solo / Family |
| Seat Type | Economy / Premium Economy / Business / First |

**Dataset shape after cleaning: 1,878 rows × 18 columns**

---

## 🧹 Data Cleaning

Before analysis, the dataset required significant cleaning:

- **Wifi & Connectivity** column was dropped — 82% of values were missing (3,237 out of 3,926)
- **Aircraft** column was dropped — 1,880 missing values (too sparse to be useful)
- Missing values in numerical rating columns were filled with their **median values**
- Remaining rows with missing values were dropped
- Final clean dataset: **1,878 rows** (down from 3,926)

---

## 📊 Exploratory Data Analysis (EDA)

### 1. Ratings Distribution
![Ratings Chart](ratings_chart.png)

The overall ratings are heavily skewed toward the extremes — customers either love BA or hate it. The average rating is just **4.67 out of 10**, which is well below average for a major international carrier. This suggests a deeply divided customer base with very few neutral experiences.

---

### 2. Top 10 Countries Reviewing BA
![Top Countries](top_countries.png)

The **United Kingdom** dominates the reviews by a large margin, followed by the United States and Australia. This makes sense as BA primarily serves routes to and from London Heathrow. The high volume of UK reviews also suggests that domestic and frequent flyers are the most vocal about their experiences.

---

### 3. Type of Traveller Breakdown
![Traveller Type](traveller_type.png)

**Couple Leisure** travellers make up the largest group at **33.7%**, followed by Solo Leisure and Business travellers. Family leisure travellers are the smallest group. This breakdown is important because different traveller types have very different expectations and priorities.

---

### 4. Ratings by Type of Traveller
![Ratings by Traveller](ratings_by_traveller.png)

This boxplot reveals a critical insight:
- **Business travellers** are the **most dissatisfied** — with a median rating of just 3/10
- **Solo Leisure** travellers are the **most satisfied** — with a median rating of 5/10
- Couple and Family Leisure travellers fall in between

This suggests BA is significantly underdelivering for its highest-paying customer segment — business travellers.

---

### 5. Ratings by Seat Type
![Ratings by Seat](ratings_by_seat.png)

As expected, **First Class** passengers give the highest ratings, followed by Business, Premium Economy, and Economy. However, even First Class passengers only give a median rating of around 6–7/10, which indicates that BA is underperforming **across all cabin classes** — not just economy.

---

### 6. Word Cloud of Customer Reviews
![Wordcloud](wordcloud.png)

The word cloud generated from 3,926 full review texts reveals the most frequently mentioned topics. The dominant words are **seat, flight, BA, service, food, business class, cabin crew** and **Heathrow**. Words like **delayed, bag** and **hour** also appear prominently, pointing to operational issues around baggage and delays as recurring pain points.

---

### 7. Correlation Heatmap
![Correlation Heatmap](correlation_heatmap.png)

The heatmap shows how strongly each service dimension correlates with the overall rating:

| Factor | Correlation with Rating |
|---|---|
| Value For Money | **0.87** — strongest |
| Food & Beverages | 0.75 |
| Seat Comfort | 0.73 |
| Cabin Staff Service | 0.70 |
| Ground Service | 0.71 |
| Inflight Entertainment | 0.61 — weakest |

**Key takeaway:** If British Airways wants to improve its overall ratings, the biggest return on investment would come from improving **Value For Money** and **Food Quality** — not inflight entertainment screens.

---

## 🤖 Machine Learning Model

### Goal
Predict whether a customer will **recommend British Airways** (yes/no) based on their service ratings.

### Model Used
**Random Forest Classifier** — an ensemble model that builds multiple decision trees and combines their outputs for a more accurate and stable prediction.

### Features Used
- Seat Comfort
- Cabin Staff Service
- Food & Beverages
- Inflight Entertainment
- Ground Service
- Value For Money

### Results
| Metric | Score |
|---|---|
| **Accuracy** | **93.35%** |
| Training Split | 80% |
| Testing Split | 20% |

### Feature Importance
![Feature Importance](feature_importance.png)

The ML model confirms what the correlation heatmap suggested — **Value For Money is the single most important factor** in predicting whether a customer will recommend BA. This is a powerful and consistent finding across both the statistical analysis and the machine learning model.

### Confusion Matrix
![Confusion Matrix](confusion_matrix.png)

| | Predicted: Not Recommended | Predicted: Recommended |
|---|---|---|
| **Actual: Not Recommended** | 226 ✅ | 16 ❌ |
| **Actual: Recommended** | 9 ❌ | 125 ✅ |

The model made only **25 mistakes out of 376 predictions** on unseen test data — demonstrating strong real-world predictive performance.

---

## 💡 Final Recommendations for British Airways

Based on this analysis, here are data-driven recommendations:

1. **Prioritize Value For Money** — It is the #1 driver of recommendations. Pricing strategy and perceived value must be addressed urgently.
2. **Fix the Business Class experience** — Business travellers are the most dissatisfied despite paying premium prices. This is a serious revenue risk.
3. **Improve Food Quality** — Second highest correlation with overall rating. A simple menu upgrade could significantly move the needle.
4. **Address operational delays** — The word cloud clearly shows "delayed" and "hour" as pain points. Punctuality improvements would directly improve reviews.
5. **Inflight Entertainment is least critical** — Investing heavily in screens and content will have the lowest ROI compared to the factors above.

---

## 🛠️ Technologies Used

- **Python 3**
- **Pandas** — data manipulation and cleaning
- **Matplotlib & Seaborn** — data visualization
- **Scikit-learn** — Random Forest ML model
- **WordCloud** — text visualization
- **Jupyter Notebook** — development environment

---

## 📁 Project Structure

```
British-Airways-Job-Simulation/
├── British_Airways_EDA.ipynb
├── British_Airways_Data.csv
├── ratings_chart.png
├── top_countries.png
├── traveller_type.png
├── ratings_by_traveller.png
├── ratings_by_seat.png
├── wordcloud.png
├── correlation_heatmap.png
├── feature_importance.png
└── confusion_matrix.png
```

---

*This project was built as part of a data science portfolio to demonstrate skills in EDA, data cleaning, visualization and machine learning.*
