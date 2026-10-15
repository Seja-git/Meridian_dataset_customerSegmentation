# Meridian Customer Analytics

An end-to-end customer analytics project that combines customer segmentation, churn prediction, and product recommendation analysis to turn retail transaction data into actionable business insights.

## Project Overview

Meridian Customer Analytics is a data-driven retail analytics project designed to understand customer purchasing behaviour, identify churn risk, and uncover opportunities for personalized product recommendations.

The project integrates customer, product, store, transaction, digital engagement, customer support, and churn-related data into a unified analytical workflow.

Using Python, statistical analysis, machine learning, and association rule mining, the project addresses three key business questions:

- **Customer Segmentation:** What distinct purchasing behaviours and customer groups exist?
- **Churn Prediction:** Which customers are most likely to stop purchasing, and where should retention efforts be prioritized?
- **Product Recommendations:** Which products are frequently purchased together, and how can these patterns support cross-selling?

The objective is to move beyond descriptive reporting toward customer-level insights that can support targeted marketing, retention planning, and product discovery.

## Project Objectives

- Validate and integrate multiple retail datasets into reliable customer-level analytical datasets.
- Engineer meaningful behavioural features from transaction and engagement data.
- Identify interpretable customer segments using unsupervised learning.
- Develop and evaluate a machine learning model for customer churn prediction.
- Discover product associations using frequent itemset mining and association rules.
- Evaluate recommendation strategies using ranking and relevance metrics.
- Translate analytical findings into actionable business recommendations.

## Project Structure

```text
meridian_customer_analytics/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── 01_data_understanding_preprocessing.ipynb
│   ├── 02_customer_segmentation.ipynb
│   └── 03_churn_and_recommendation_analysis.ipynb
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
```

*Note: Update the notebook names and folder structure above to match the actual files in the repository. The raw and processed data directories may be excluded from Git if the datasets are large or restricted.*

## Dataset Overview

The project uses seven interconnected retail datasets.

| Dataset | Description |
|---|---|
| `customers` | Customer demographics, acquisition channels, and loyalty information |
| `products` | Product attributes, categories, pricing, and private-label information |
| `stores` | Store locations, formats, and floor areas |
| `transactions` | Customer orders, purchased products, quantities, discounts, and revenue |
| `digital_engagement` | Monthly web/app engagement and loyalty activity |
| `support_tickets` | Customer support interactions and satisfaction information |
| `churn_labels` | Customer churn outcome labels |

### Dataset Statistics

| Metric | Records / Count |
|---|---:|
| Customers | 12,000 |
| Products | 391 |
| Stores | 27 |
| Transaction lines | 575,516 |
| Unique orders | 158,115 |
| Digital engagement records | 160,680 |
| Support tickets | 10,411 |
| Churn label records | 7,237 |

**Transaction coverage:** August 1, 2024 – July 31, 2026.

## Project Components

### 1. Customer Segmentation

**Objective:** Identify meaningful customer groups based on purchasing behaviour rather than relying exclusively on predefined loyalty categories.

**Methodology**

- Performed data validation, exploratory analysis, and preprocessing.
- Engineered 25 customer-level behavioural features.
- Applied K-Means clustering and compared it with Gaussian Mixture Models (GMM).
- Evaluated clustering quality using the silhouette score.
- Compared cluster assignments using the Adjusted Rand Index (ARI).
- Profiled the resulting segments to understand their purchasing patterns and potential business needs.

**Model evaluation**

| Algorithm | Evaluation Metric | Score |
|---|---|---:|
| K-Means (K = 5) | Silhouette Score | 0.0971 |
| Gaussian Mixture Model | Silhouette Score | 0.0169 |
| K-Means vs. GMM | Adjusted Rand Index | 0.9651 |

The five-cluster K-Means solution was selected for customer profiling and business interpretation. The relatively low silhouette score indicates that the customer groups overlap, so the segments should be interpreted as behavioural profiles rather than perfectly separated populations.

**Identified customer segments**

| Customer Segment | Customers | Share of Customers |
|---|---:|---:|
| Premium Home & Living Shoppers | 3,025 | 27.59% |
| Frequent Personal Care Shoppers | 2,600 | 23.72% |
| Family & Household Shoppers | 2,389 | 21.79% |
| Health & Wellness Specialists | 1,631 | 14.87% |
| Lapsed Everyday Shoppers | 1,320 | 12.03% |

**Business applications**

- Design targeted campaigns for distinct customer groups.
- Identify opportunities for cross-selling and personalized offers.
- Develop segment-specific engagement and retention strategies.
- Replace one-size-fits-all marketing with behaviour-based customer targeting.

### 2. Customer Churn Prediction

**Objective:** Identify customers at risk of becoming inactive so that retention efforts can be prioritized before further customer loss occurs.

**Methodology**

- Defined a temporal prediction framework with a cutoff date of April 30, 2026.
- Used the subsequent period, May 1 – July 31, 2026, to determine churn outcomes.
- Applied eligibility criteria requiring at least two lifetime orders and one order during the six months preceding the cutoff.
- Engineered customer-level predictive features from relevant transactional and engagement information.
- Prepared 51 raw features and 59 encoded model features.
- Trained a HistGradientBoosting classifier.
- Evaluated predictive performance using ROC-AUC, PR-AUC, top-decile precision, and a selected classification threshold.

**Model evaluation**

| Metric | Result |
|---|---:|
| Eligible customers | 7,247 |
| Churn rate | 23.15% |
| ROC-AUC | 0.8552 |
| PR-AUC | 0.7395 |
| Top-decile precision | 93.10% |
| Selected classification threshold | 0.8066 |

**Key findings**

- The model achieved strong discrimination between customers who churned and those who remained active.
- A top-decile precision of 93.10% indicates that the highest-ranked risk group was highly concentrated with churn cases in the evaluation data.
- The selected threshold supports classification based on the project's chosen evaluation criteria.

**Business applications**

- Prioritize high-risk customers for retention campaigns.
- Allocate retention budgets toward customers with elevated predicted churn risk.
- Support personalized re-engagement offers and loyalty initiatives.
- Help marketing teams identify customers who may require proactive attention.

*Evaluation metrics describe performance on the project's evaluation data and should not be interpreted as a guarantee of future results.*

### 3. Product Recommendation Analysis

**Objective:** Discover product purchasing associations and evaluate whether recommendation techniques can help customers discover relevant products and support cross-selling.

**Methodology**

- Prepared transaction data at the order level.
- Mined frequent itemsets using association analysis.
- Generated and evaluated association rules.
- Examined meaningful product-pair relationships and cross-category associations.
- Evaluated recommendation approaches using customer-level ranking metrics.
- Compared a popularity-based baseline with Item-Item Cosine and Singular Value Decomposition (SVD) approaches.

**Association analysis results**

| Metric | Result |
|---|---:|
| Training orders | 135,945 |
| Frequent itemsets | 387 |
| Association rules | 224 |
| Meaningful product-pair rules | 116 |
| Cross-category rules | 70 |
| Evaluation customers | 5,832 |

**Recommendation evaluation**

The popularity-based baseline achieved the following results:

| Metric | Score |
|---|---:|
| Precision@5 | 0.1187 |
| Recall@10 | 0.0976 |
| Hit Rate@5 | 0.4417 |

Item-Item Cosine and SVD were also evaluated but performed worse than the popularity baseline under the project's evaluation setup.

**Business applications**

- Identify complementary products for cross-selling.
- Discover purchasing relationships within and across product categories.
- Support product bundling and targeted promotional campaigns.
- Establish a measurable baseline before adopting more complex recommendation algorithms.

The results demonstrate the importance of evaluating recommendation methods against a simple baseline rather than assuming that a more complex model will perform better.

## Technology Stack

| Category | Technologies |
|---|---|
| Programming | Python |
| Data manipulation | Pandas, NumPy |
| Machine learning | Scikit-learn |
| Customer segmentation | K-Means, Gaussian Mixture Models |
| Churn prediction | HistGradientBoosting |
| Recommendation analysis | Frequent itemset mining, association rules, Item-Item Cosine, SVD |
| Evaluation | Silhouette Score, ARI, ROC-AUC, PR-AUC, Precision@K, Recall@K, Hit Rate@K |
| Development environment | Jupyter Notebook, VS Code |
| Version control | Git, GitHub |

## Analytical Workflow

1. **Data understanding:** Inspect datasets, schemas, distributions, missing values, and data quality.
2. **Data preprocessing:** Validate relationships, handle data quality issues, and prepare analytical tables.
3. **Feature engineering:** Create customer-level behavioural features and recommendation inputs.
4. **Model development:** Apply clustering, churn classification, and product association techniques.
5. **Model evaluation:** Assess clustering quality, predictive performance, and recommendation relevance.
6. **Business interpretation:** Translate model outputs into customer profiles, risk prioritization, and cross-selling opportunities.

## Key Learnings

- Integrating multiple datasets requires careful validation of customer, product, order, and time relationships.
- Customer segmentation is most useful when the resulting clusters can be interpreted and translated into business actions.
- Temporal cutoffs are important in churn prediction to reduce information leakage from future outcomes.
- Imbalanced classification benefits from evaluation metrics beyond accuracy.
- Recommendation systems should be compared against simple baselines using appropriate ranking metrics.
- Model performance and business usefulness are related but distinct: both technical evaluation and practical interpretation matter.

## How to Run the Project

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd meridian_customer_analytics
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the notebooks

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Run the notebooks in the documented workflow order after placing the required datasets in the appropriate directories.

**Data availability:** The notebooks require the project's input datasets. If raw data is not included in the repository, provide appropriate access instructions or document the expected schemas and preprocessing steps. Do not commit confidential or restricted data.

## Future Enhancements

- Develop a reusable pipeline for data validation and feature generation.
- Add model explainability to identify the factors associated with churn risk.
- Evaluate churn predictions and customer segments over successive time periods.
- Improve recommendation quality through additional candidate-generation and ranking strategies.
- Build an interactive Power BI dashboard to communicate customer, churn, and recommendation insights.
- Monitor model performance and business outcomes as new data becomes available.

## Conclusion

Meridian Customer Analytics brings together three complementary analytical capabilities: behavioural customer segmentation, churn risk prediction, and product recommendation analysis.

By combining data preparation, feature engineering, machine learning, model evaluation, and business interpretation, the project demonstrates an end-to-end approach to solving practical retail analytics problems.

The resulting insights can help businesses understand their customers, prioritize retention efforts, and identify opportunities to improve product discovery and cross-selling.

---

**Developed using:** Python | Pandas | NumPy | Scikit-learn | Jupyter Notebook | Git
