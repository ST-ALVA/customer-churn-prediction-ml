👉 For a quick, no-setup review of the full analysis, see `churn_prediction.html`.

# Customer Churn Prediction — Applied Machine Learning for Retention Strategy

End-to-end customer churn prediction using supervised machine learning and behavioral segmentation to support data-driven retention strategies.

---

## Business Problem
Customer churn represents a critical risk for subscription-based businesses. The objective of this project was to identify customers at high risk of churn, understand the behavioral drivers behind cancellations, and generate actionable insights to support proactive retention strategies.

Given the business cost of missed churn cases, **recall for the churn class was prioritized** over raw accuracy.

---

## Dataset
The dataset represents customers of a fitness chain and includes:
- Demographic information
- Contract characteristics
- Usage frequency and engagement metrics
- Social and referral indicators
- Binary churn labels

The data exhibits **class imbalance**, with churn representing a minority class.

---

## Analytical Approach
- Conducted **exploratory data analysis (EDA)** and statistical validation to assess distributions, outliers, and feature relevance.
- Performed **feature selection** using correlation analysis and Variance Inflation Factor (VIF) to reduce multicollinearity.
- Applied **stratified train-test split** to preserve class proportions.
- Trained and evaluated supervised models with metrics aligned to business risk (recall-focused).
- Applied **clustering techniques** to segment customers and analyze churn behavior across behavioral profiles.

---

## Models & Evaluation

### Logistic Regression (Primary Model)
- **ROC AUC:** **0.957**
- **Recall (Churn, default threshold = 0.5):** 0.79
- **Recall (Churn, adjusted threshold = 0.35):** **0.86**
- **Precision (Churn):** 0.78
- **F1-score (Churn):** 0.82

Threshold tuning significantly improved churn detection, allowing the model to correctly identify **nearly 9 out of 10 churned customers**, at the cost of a moderate increase in false positives — a trade-off aligned with real-world retention priorities.

This model was selected as the **primary decision-support model** due to its superior recall and interpretability.

---

### Decision Tree (Tuned with GridSearchCV)
- **ROC AUC:** 0.892
- **Recall (Churn):** 0.76
- **Precision (Churn):** 0.80
- **F1-score (Churn):** 0.78

Hyperparameter tuning improved generalization and recall while maintaining interpretability, making this model suitable for explaining decisions to non-technical stakeholders.

---

### Random Forest (Ensemble Model)
- **ROC AUC:** **0.943**
- **Recall (Churn):** 0.76
- **Precision (Churn):** 0.82
- **F1-score (Churn):** 0.79

The Random Forest achieved strong overall discriminative performance and was used to identify the **most influential features driving churn**, including customer lifetime, attendance frequency, age, additional spending, and contract length.

---

## Customer Segmentation (Clustering)
Multiple clustering approaches were explored, including:
- KMeans with standardized features
- KMeans with reduced weights for binary variables
- **K-Medoids with Gower distance** (mixed data types)

Although silhouette scores were modest (≈0.14–0.19), the resulting clusters revealed **consistent behavioral patterns** aligned with the predictive models:
- Social engagement (group visits, referrals, partner programs) strongly correlates with retention.
- Early-stage users with short contracts and low engagement show the highest churn risk.
- Older users and long-tenure customers exhibit greater loyalty.

Rather than treating clustering as a purely mathematical exercise, segmentation was evaluated based on its usefulness for decision-making and retention strategy design.

---

## Business Impact
- Identified high-risk customer segments for early intervention.
- Demonstrated how **threshold tuning** can materially change business outcomes without retraining models.
- Validated the importance of social and contractual factors in retention strategies.
- Provided a framework for prioritizing retention actions and marketing investments by customer profile.
- Enabled early identification of at-risk customers during the first months of the lifecycle, when churn probability is highest.

---

## Key Takeaways
- Optimizing recall is critical in churn prediction when false negatives are costly.
- Classification thresholds are powerful business levers, not just technical parameters.
- Combining predictive modeling with segmentation improves interpretability and actionability.
- Strong business insights can emerge even when clustering metrics are imperfect.

---

## Notes
This project was completed as part of the **TripleTen Data Analytics Bootcamp** and simulates a real-world customer retention scenario.

---

## 📄 Notebook & Reproducibility
This project is provided in two formats:

- **Jupyter Notebook (`.ipynb`)** — full, reproducible analysis including data preparation, modeling, and evaluation.
- **HTML version (`.html`)** — static, easy-to-read version for quick review without requiring a local Python environment.

🔹 The HTML file allows reviewers to explore the complete analysis, visualizations, and conclusions directly in the browser.  
🔹 Full reproducibility is supported via a `requirements.txt` file with pinned library versions (Python 3.11).