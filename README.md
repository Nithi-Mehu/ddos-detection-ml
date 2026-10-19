# DDoS Attack Detection using Machine Learning

A binary classification project to detect **DDoS attacks** in network traffic using classical machine learning models, with feature selection, hyperparameter tuning, and model explainability (SHAP).

## Dataset
- **CIC-IDS2017**, Friday afternoon DDoS capture (`Friday-WorkingHours-Afternoon-DDos.pcap_ISCX.csv`)
- Network flow features labeled as `BENIGN` or `DDoS`
- The dataset is available on Kaggle and is not included in this repository due to its size

## Workflow
1. **Data quality check:** missing values, infinite values, duplicates and constant columns
2. **EDA:** class distribution (count plot and pie chart)
3. **Preprocessing:** replaced infinite values, removed duplicates, dropped constant columns, encoded labels (`BENIGN` = 0, `DDoS` = 1)
4. **Train-test split:** 80/20, stratified to preserve the class ratio
5. **Leak-free pipeline:** median imputation, standard scaling and **RFE** (Recursive Feature Elimination) fitted on training data only, selecting the top 25 features
6. **Base models:** Naive Bayes, Logistic Regression, Decision Tree
7. **Ensemble:** Soft Voting Classifier combining the three models
8. **Hyperparameter tuning:** `GridSearchCV` with 5-fold Stratified CV, scored on weighted F1
9. **Evaluation:** Accuracy, Precision, Recall, F1-score, ROC-AUC, classification report, confusion matrix (counts and normalized) and ROC curves
10. **Overfitting check:** 5-fold cross-validation compared against test accuracy
11. **Explainability:** SHAP summary plot to identify the features that drive predictions

## Models Compared
| Model | Variants |
|-------|----------|
| Naive Bayes | Base, Tuned |
| Logistic Regression | Base, Tuned |
| Decision Tree | Base, Tuned |
| Voting Ensemble | Base, Tuned |

The best model is selected automatically by F1-score and ROC-AUC. Full results, plots and the final comparison table are available in the notebook.

## Tech Stack
Python, pandas, NumPy, scikit-learn, SHAP, matplotlib, seaborn

## How to Run
```bash
pip install pandas numpy matplotlib seaborn scikit-learn shap
```
1. Download the dataset from Kaggle and update the file path in Cell 2
2. Open `ddos-detection.ipynb` in Jupyter Notebook or Kaggle
3. Run all cells

## Future Improvements
- Try ensemble models such as Random Forest and XGBoost
- Test on other CIC-IDS2017 attack types (multi-class detection)
- Evaluate on unseen days of traffic to check generalization
