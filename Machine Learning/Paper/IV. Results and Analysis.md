---
- Comparison of performance metrics: This section presents the results of the evaluation, comparing the performance of each technique based on the chosen metrics.
- Discussion of results and their implications: This section interprets the results, highlighting key insights and discussing the implications of the findings.
- Identification of strengths and limitations of each technique: This section assesses the strengths and limitations of each technique, based on the results and the analysis.
- Recommendations for selecting an appropriate technique for a specific problem: This section provides recommendations for practitioners and decision-makers, based on the results of the evaluation.
---

## Comparison of performance metrics
Trainings metrics:
- F1_Macro Score: Takes precision and recall into account, provides balance of them. F1 score of each class separately and then averages → Weighting each class same
- AUROC_Macro Score: Measure to distinguish FPR and TPR at different thresholds → Same as F1
- Accuracy: To show how deceiving the metric can be and give false performance measures, when data is imbalanced
- Class-wise F1-Score: F1-Score plotted for each class individually to see how different classes perform