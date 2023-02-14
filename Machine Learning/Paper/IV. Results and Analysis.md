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

## Discussion of results and their implications
- Reduced Balanced vs Baseline:
	- Obvious and expected reduction in performance
	- Loss slightly worse, with lower validation loss → Validation set balanced
	- Accuracy slightly better, giving the misconception of a good performing model
	- Complete opposite, when looking at AUROC and F1_Macro. Dropped to 1/8th and worse
	- Multiclass F1-Score shows massive drop in scores, with all classes below 1.5
	- Obvious when looking at confusion matrix, underrepresented classes gets predicted much less, resulting in overprediction of overrepresented class → higher accuracy
	- Baseline struggles with objects of similar type, i.e. (dog, cat, frog and automobile/truck)
	- ROC-Curve and PR-Curve similar, both struggle with same classes, but in both cases Baseline performs slightly worse
- Baseline vs CW vs FL:
	- Training loss CW > Training Loss FL > Training Loss Baseline, whereas validation loss same
	- Accuracy of FL slightly worse, but CW same
	- AUROC exactly same for all 3, FL and CW greater slope of F1_macro curve, but converge in same value → less training needed for same results
	- Multiclass F1-Score similar behaviour with convergence, majority classes converge on slightly lower F1-Scores, but minority classes on the other hand perform better
	- CW and FL show much greater slope of especially of the minority classes, with very small to irrelevant performance differences between CW and FL
	- Much better performance of minority classes, when looking at CM, still some overprediction of majority classes, truck ship for FL and truck for CW. 
	- Less confusion between multiple classes in FL, but CW performs better on previously mentions similar classes, i.e. dog, cat
- Baseline vs US vs OS:
	- Undersampling always worse than baseline, Oversampling greater reduction in loss and greater slope of accuracy
	- Oversampling slightly bigger slope in first 20 epochs on AUROC, Undersampling worse respectively
	- Undersampling can't reach same F1_Macro-Score, whereas Oversampling reaches it much faster → More samples
	- Undersampling worse on majority classes than Baseline, but slightly better on minority classes. Whereas Oversampling outperforms on all classes
	- Also visible in ROC-Curve and PR-Curve
	- Undersampling much more confusion, worse performance on majority classes, slightly better on 2 classes with the least amount of samples
	- Oversampling good on minority and majority classes, still some confusion on hard classes

Rarely just one technique used, combination mostly yields the best results. Only the best performing techniques from above are used in combination.

- Baseline vs Heavy Augmentation + CW vs Heavy Augmentation + OS
	- Much greater difference between val and train loss, with HA + OS, having the worst train_loss, accuracy also greatly decreases
	- Both methods converge on same F1_Macro and AUROC score, which is significantly lower compared to Baseline, but HA + OS has a greater slope in beginning → Augmentation might be too strong, for the small images
	- Baseline outperforms both techniques on majority classes, HA + OS performs better than HA + CW on most of the majority classes
	- Same trend visible in ROC-Curve and PR-Curve: Generally baseline is better, and both techniques have performed much worse on cat and deer
	- HA + CW much more general confusion with smaller outliers, whereas HA + OS generalizes better but has higher peaks when misclassifying the hard classes
- Baseline vs Simple Augmentation + OS
	- Much less difference between train and validation loss, although a slightly higher loss in total, same for accuracy
	- Very similar AUROC, but a slightly greater slope in beginning, F1_Macro also increases faster, but converges on a lower value
	- Confirmed by looking at Multiclass F1-Scores, greater performance on minority classes, but slightly worse on majority classes
	- ROC-Curve and PR-Curve much better Baseline → Best generalization yet achieved on unseen test data
	- Also visible on CM, no big spikes in misclassification of hard classes, minority and majority classes predicted accurately, generalization pretty good

## Identification of strengths and limitations of each technique
- Focal Loss and Class Weights behave similar on this dataset, although CW seemed slightly more stable
- Undersampling really bad, since number of samples already pretty low
- Oversampling in contrast works pretty good, since number of samples greatly increased, less prone to overfitting
- Heavy augmentation too strong for the small images, possibly resulted in too much noise, where class characteristics weren't visible anymore
- Simpler and less augmentation worked better
