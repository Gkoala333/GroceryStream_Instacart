# GroceryStream

End-to-end Instacart-style ETL → Warehouse → ML → Dashboard pipeline

A production-grade data analytics platform demonstrating enterprise data engineering, machine learning, and business intelligence capabilities using the Instacart Market Basket dataset.

---

## 📌 Table of Contents

- [Overview](#overview)
- [Features](#features)
  - [Data Engineering](#data-engineering)
  - [Machine Learning](#machine-learning)
  - [Dashboard](#dashboard)
- [Quick Start](#quick-start)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Load Data & Train Model](#load-data--train-model)
  - [Run Dashboard](#run-dashboard)
- [Project Structure](#project-structure)
- [Data Pipeline](#data-pipeline)

---

## Overview

GroceryStream is a comprehensive data platform that showcases:

- **ETL Orchestration:** Python-based scripts for automated data ingestion and processing.
- **Data Warehouse:** Staging and feature storage in CSV / SQLite (`grocerystream.db`).
- **ML Systems:** Purchase prediction using Random Forest; product recommendation engine.
- **Analytics Dashboard:** Real-time insights with Streamlit.
- **A/B Testing:** Basic experimentation framework.

**Business Value**

- 📈 Increased basket size through personalized recommendations
- 🎯 High prediction accuracy for next purchase items
- 🔄 Enhanced reorder rate through ML-powered suggestions
- ⚡ Real-time inference for thousands of users

---

**Workflow:**

DATA SOURCES
• Instacart CSV files (orders, products, aisles, departments, order_products_prior, order_products_train)

   │
   ▼


INGESTION LAYER (Python ETL)
• Scripts load CSVs → create features → save processed data & db

   │
   ▼


DATA WAREHOUSE / FEATURES
• SQLite or staged CSVs
• user_features, product_features, user_product_features
• Saved as features.csv for dashboard

   │
   ▼


ML MODELS
• Random Forest Purchase Prediction (rf_model.pkl)
• IGBM model (Igbm_model.pkl)

   │
   ▼


ANALYTICS & DASHBOARD
• Streamlit dashboard (dashboard.py)
• Explore features, model performance, top product predictions


---

## Features

### Data Engineering
- ✅ Automated ETL scripts for CSV ingestion, merging, and feature creation
- ✅ Processed features saved for ML and dashboard (`features.csv`)
- ✅ User-product, product-level, and user-level features
- ✅ Lightweight SQLite/CSV warehouse for analysis

### Machine Learning
1. **Purchase Prediction**
   - Model: Random Forest
   - Features: User-product interactions, product popularity, reorder rates
   - Metrics: ROC-AUC, F1, Precision, Recall, Accuracy

2. **Top Product Prediction**
   - Simulated Top-N prediction for any user (based on product popularity & reorder rate)
   - Fully integrated in Streamlit dashboard

### Dashboard
- Interactive filters for product-level metrics
- Feature importance visualization
- Top 10 product prediction (works even if `user_id` not present)
- Uses `features.csv` and `rf_model.pkl`


---

## Quick Start

### Prerequisites
- Python 3.9+
- Streamlit
- Pandas, Numpy, scikit-learn, Joblib


## ✨ Features

- **ETL Pipeline**: Automated data loading, merging, and feature engineering
- **Machine Learning Model**: Random Forest binary classifier for purchase prediction
- **Interactive Dashboard**: Streamlit-based visualization with multiple analysis sections
- **Product Recommendations**: Top 10 predicted products ranked by purchase likelihood
- **Feature Importance Analysis**: Understand which factors drive predictions
- **Flexible Filtering**: Filter products by various metrics (product_id, total_orders, reorder_rate, etc.)

## Installation

```bash
# 1. Clone repository
git clone https://github.com/yourusername/grocerystream.git
cd grocerystream

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt
```

## 📖 Usage

### Load Data & Train Model

```bash
python Prediction.py
```

This generates:
- `rf_model.pkl` - Trained Random Forest model
- `features.csv` - Dashboard-ready features

### Run Dashboard

```bash
streamlit run dashboard.py
```

Access the dashboard at `http://localhost:8501`

**Dashboard Features:**
- Top Products section works even if `features.csv` has no `user_id`
- Filter by available columns: `product_id`, `total_orders_product`, `reorder_rate_product`, `avg_cart_position`

## Project Structure

```
GroceryStream/
├── README.md
├── rf_model.pkl                  # Trained Random Forest model
├── lgbm_model.pkl                # Optional ML model
├── features.csv                  # Processed feature file for dashboard
├── Prediction.py                 # ETL + ML training
├── dashboard.py                  # Streamlit dashboard
├── stage/                        # Raw CSVs
├── data/                         # Data storage
├── notebooks/                    # Analysis & ML experiments
└── docs/                         # Documentation
```

## Data Pipeline

### ETL / Feature Generation

1. Loads CSVs from `stage/` directory
2. Merges datasets and creates comprehensive features:
   - User-level features (order history, behavior patterns)
   - Product-level features (popularity, reorder rates)
   - User-product interaction features
3. Saves processed data as `features.csv` for dashboard consumption

### ML Model

- **Algorithm**: Random Forest Binary Classifier
- **Features**: User statistics, product statistics, and interaction metrics
- **Output**: Purchase likelihood probability (0-1)
- **Model File**: `rf_model.pkl`

### Dashboard

**Streamlit Application** with three main sections:

1. **Data Overview**: Summary statistics and data distribution
2. **Feature Importance**: Visual analysis of model feature weights
3. **Top 10 Predicted Products**: ML-powered product recommendations

## 🏆 Top 10 Predicted Products (Simulated User)

The dashboard's "Top 10 Predicted Products" section uses the trained Random Forest model to rank products by **predicted purchase likelihood**.

### Example Output (Simulated User)

| Rank | Product ID | Predicted Score | Total Orders | Reorder Rate |
|------|------------|-----------------|--------------|--------------|
| 1    | 24852      | 126,398         | 149,684      | 0.844        |
| 2    | 13176      | 99,960          | 119,871      | 0.834        |
| 3    | 21137      | 64,074          | 82,627       | 0.775        |
| 4    | 21903      | 59,511          | 76,838       | 0.775        |
| 5    | 47209      | 54,960          | 68,567       | 0.802        |
| 6    | 47766      | 42,450          | 55,907       | 0.759        |
| 7    | 27845      | 35,728          | 42,920       | 0.832        |
| 8    | 47626      | 33,590          | 48,328       | 0.695        |
| 9    | 27966      | 33,271          | 43,278       | 0.769        |
| 10   | 16797      | 31,821          | 45,392       | 0.701        |

### 🔍 Analysis

- **Predicted Score**: Represents the model's confidence that the product will be purchased next by a user. Higher score → higher likelihood.
- **Total Orders**: Popularity indicator; products with more historical orders are more likely to appear in top recommendations.
- **Reorder Rate**: Loyalty metric; higher reorder rates indicate products frequently repurchased.

### 📊 Observations

1. **High Popularity & Reorder**  
   Top-ranked products (e.g., product_id 24852 and 13176) combine high total orders and high reorder rates (≈0.83–0.84), showing consistent customer demand.

2. **Moderate Popularity, Strong Affinity**  
   Products like 27845 have lower total orders but high reorder rate (0.832), suggesting niche products with loyal buyers.

3. **Diverse Mix**  
   The list balances **high-volume items** (many orders) and **high-affinity items** (high reorder rate), providing effective recommendations even without a user-specific profile.

4. **Business Insight**  
   Focusing marketing, promotions, or inventory planning on these top predicted products can increase basket size and reorder probability. The simulated user predictions allow the dashboard to provide **immediate insights** even when individual user_id data is unavailable.

> **Note**: This is a simulated ranking for demonstration purposes; real user-specific predictions would require user_id features.

## 🛠️ Technologies

- **Python 3.x**
- **Pandas** - Data manipulation and analysis
- **Scikit-learn** - Machine learning (Random Forest)
- **Streamlit** - Interactive web dashboard
- **NumPy** - Numerical computing
- **Matplotlib/Seaborn** - Data visualization (optional)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📧 Contact

Project Link: [GroceryStream_Instacart](https://drive.google.com/drive/folders/12rI6p-Bst4EIJNe_9EDZlxIXRaeCiQDU?usp=sharing)

---

**Built with ❤️ for better grocery shopping experiences**
