# Meridian Customer Analytics

## Project Overview

Meridian Customer Analytics is a customer analytics project focused on
understanding customer behaviour and developing data-driven customer
segmentation.

The project combines transactional, customer, product, store, digital
engagement, support and churn-related data to identify meaningful customer
behaviour patterns and translate them into actionable business insights.

The project is being developed using Python, Pandas, Scikit-learn and
Jupyter Notebook.

---

## Project Objective

The initial objective of the project is to:

- Understand and validate the available customer and transaction data.
- Create reliable customer-level analytical datasets.
- Develop behaviour-based customer segments.
- Replace purely descriptive loyalty tiers with data-driven behavioural
  segmentation.
- Profile each customer segment.
- Recommend targeted marketing actions for each segment.

---

## Dataset Overview

The project contains the following datasets:

| Dataset | Description |
|---|---|
| `customers` | Customer demographic, acquisition and loyalty information |
| `products` | Product, category, pricing and private-label information |
| `stores` | Store information including format, location and floor area |
| `transactions` | Customer order and transaction-line information |
| `digital_engagement` | Monthly web/app engagement and loyalty activity |
| `support_tickets` | Customer support interactions and satisfaction information |
| `churn_labels` | Customer churn outcome labels |

### Key Dataset Statistics

After preprocessing and validation:

- Customers: **12,000**
- Products: **391**
- Stores: **27**
- Transaction lines: **575,516**
- Unique orders: **158,115**
- Digital engagement records: **160,680**
- Support tickets: **10,411**
- Churn labels: **7,237**

Transaction coverage:

- Start: **2024-08-01**
- End: **2026-07-31**

---

# Project Structure

```text
meridian_customer_analytics/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── 01_data_understanding_preprocessing.ipynb
│   └── 02_customer_segmentation.ipynb
│
├── outputs/
│   ├── figures/
│   │   └── exploration/
│   └── tables/
│
├── src/
│
├── .gitignore
├── requirements.txt
└── README.md