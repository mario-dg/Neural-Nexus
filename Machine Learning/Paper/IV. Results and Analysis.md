---
- Comparison of performance metrics: This section presents the results of the evaluation, comparing the performance of each technique based on the chosen metrics.
- Discussion of results and their implications: This section interprets the results, highlighting key insights and discussing the implications of the findings.
- Identification of strengths and limitations of each technique: This section assesses the strengths and limitations of each technique, based on the results and the analysis.
- Recommendations for selecting an appropriate technique for a specific problem: This section provides recommendations for practitioners and decision-makers, based on the results of the evaluation.
---

## Comparison of performance metrics
Trainings metrics (Evaluated on validation set):
- F1_Macro Score: Takes precision and recall into account, provides balance of them. F1 score of each class separately and then averages → Weighting each class same
- AUROC_Macro Score: Measure to distinguish FPR and TPR at different thresholds → Same as F1
- Accuracy: To show how deceiving the metric can be and give false performance measures, when data is imbalanced
- Class-wise F1-Score: F1-Score plotted for each class individually to see how different classes perform

Evaluation metrics (Evaluated on unseen test set):
- PR-Curve: Precision over recall on different thresholds, observe shape of curve to see if model biased towards precision or recall.
- ROC-Curve: Similar to AUROC
- Confusion Matrix: Shows possible misclassification/confusion patterns, see where the model performs especially good or bad on concrete examples

Runs to use:
- Reduced Balanced
- Baseline
- Class Weight
- Focal Loss
- Undersampling
- Oversampling
- Heavy Augmentation + Class Weight
- Heavy Augmentation + Oversampling
- Simple Augmentation + Oversampling

