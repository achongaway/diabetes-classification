# Predictive Analytics for Diabetes Risk Classification

Can routinely collected health indicators classify diabetes status accurately enough to support proactive screening? This project builds and compares three classification models on the public BRFSS-derived Diabetes Health Indicators dataset (250,000+ observations, 21 predictors), evaluating each with metrics appropriate for an imbalanced target.

## Approach

- **Target:** the original three-level variable (no diabetes / pre-diabetes / diabetes) is converted to binary, focusing on confirmed diabetes.
- **Imbalance handling:** class weighting on all models, F1-optimized hyperparameter search, and PR-AUC reporting alongside ROC-AUC.
- **Models:** logistic regression (standardized pipeline, interpretable baseline), decision tree (depth/leaf-constrained via grid search), and random forest (tuned ensemble with balanced subsample weighting).
- **Validation:** stratified 80/20 train/test split, 3-fold stratified cross-validation for tuning, and a majority-class baseline as the accuracy floor.

## Results

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| Random Forest | 0.774 | 0.344 | 0.686 | 0.458 | 0.820 |
| Logistic Regression | 0.732 | 0.311 | 0.761 | 0.441 | 0.820 |
| Decision Tree (Tuned) | 0.707 | 0.293 | 0.782 | 0.426 | 0.814 |

Random forest delivered the strongest overall balance and is recommended for screening-oriented use, where flagging elevated-risk individuals for follow-up costs little relative to a missed case. Key predictors converged on BMI, age, blood pressure, and self-rated general health — indicators routinely available in primary care.

## Repository Structure

```
notebooks/diabetes_risk_classification.ipynb   Full analysis with narrative
data/README.md                                 Dataset source and setup
requirements.txt                               Python dependencies
```

## Running

```
pip install -r requirements.txt
jupyter notebook notebooks/diabetes_risk_classification.ipynb
```

Download the dataset first per `data/README.md`.

## Limitations

Survey-based, self-reported data; internal validation only; the binary target does not distinguish pre-diabetes. See the notebook's conclusions for discussion and next steps.
