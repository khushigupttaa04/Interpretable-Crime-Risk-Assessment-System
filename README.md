# Interpretable Crime Risk Assessment

Spatial crime risk prediction on 7.8M+ Chicago crime records using grid-based hotspot detection, XGBoost and Random Forest, SHAP explainability and privacy-aware data handling.

## Pipeline

```mermaid
flowchart LR
    A[Raw data<br/>7.8M records] --> B[Cleaning and<br/>temporal features]
    B --> C[1 km grid<br/>aggregation]
    C --> D[Hotspot score and<br/>risk labels]
    D --> E[Privacy controls]
    E --> F[XGBoost / RF<br/>risk and category models]
    F --> G[SHAP explanations]
    F --> H[Case similarity<br/>retrieval]
```

## What it does

- Bins crimes into roughly 1 km grid cells, normalises counts into a hotspot score and labels each cell High, Medium or Low risk.
- Trains XGBoost and Random Forest models for two tasks: crime risk level and crime category (Property, Violent, Drug).
- Evaluates the risk model on a temporal hold-out. Labels are rebuilt per period, models train on 2001-2019 and are tested on 2020 onwards, and results are compared against a persistence baseline. Class balancing is applied to the training set only.
- Explains predictions with SHAP (summary and waterfall plots) and maps the top drivers to suggested actions.
- Applies privacy controls: coordinate masking to about 100 m, k-anonymity (k=5) on rare crime types, separate public and training views of the data, and a JSON audit log.
- Retrieves the most similar historical cases for a new incident using cosine similarity.

## Results

Risk models are tested on 2020 onwards. The test set is imbalanced, so macro F1 is the main metric.

| Task | Model | Accuracy | Macro F1 |
|---|---|---|---|
| Crime risk | Persistence baseline | TBD | TBD |
| Crime risk | XGBoost | TBD | TBD |
| Crime risk | Random Forest | TBD | TBD |
| Crime category | XGBoost | TBD | TBD |
| Crime category | Random Forest | TBD | TBD |

<p>
  <img src="assets/crime_count_by_year.png" width="48%">
  <img src="assets/top10_crime_types.png" width="48%">
</p>

## Repository structure

```
notebooks/crime_risk_assessment.ipynb   full pipeline
data/README.md                          dataset download instructions
assets/                                 figures used in this README
requirements.txt
```

## Running it

```bash
git clone https://github.com/khushigupttaa04/Interpretable-Crime-Risk-Assessment-System.git
cd Interpretable-Crime-Risk-Assessment-System
pip install -r requirements.txt
jupyter notebook notebooks/crime_risk_assessment.ipynb
```

Download the dataset into `data/` first (see `data/README.md`). On Google Colab, put the CSV in Drive and uncomment the Drive lines in Section 1. A high-RAM runtime helps with the full dataset.

## Team

- Khushi Gupta: data preprocessing, grid-based spatial aggregation, risk labelling
- Sanjhi Pareek: data security and privacy controls, case similarity system
- Priya: XGBoost and Random Forest models, SHAP explainability

Minor project, B.Tech CSE (AI/ML), UPES Dehradun.
