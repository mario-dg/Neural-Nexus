---
- Summary of findings and contributions: This section summarizes the key findings of the paper, and explains how the study contributes to the literature on class imbalance and the CIFAR10 dataset.
- Future directions for research: This section outlines areas for future research, including potential extensions of the study or new directions for investigation.
- Implications for practitioners and decision-makers: This section explains the practical implications of the results, and provides guidance for practitioners and decision-makers.
- Limitations of the study and opportunities for improvement: This section acknowledges any limitations of the study, and identifies opportunities for improvement in future research.
---

## Summary of findings and contributions
- Project showed how class imbalances impacts performance of a normally good performing model
- Shows that model evaluation shouldn't solely happen on the accuracy-metric, since it's deceiving high score on imbalanced data
- Thus a set of metrics should be used to a get a good overview of a model, and it's classification capabilities
- Compares how different techniques try to counteract mentioned imbalance, depicts their strength and limitations and shows that a combination of methods most likely results in a better performance
- Gives good general overview about the topic, it's problems and shows simple solutions to mitigate the error introduced by an imbalanced distribution of classes

## Future directions for research
- Include more techniques
- Try out more variations of used techniques:
	- Using different ways of choosing the class weights
	- Trying different sets and combinations of augmentations
	- Mix of undersampling and oversampling
	- Undersample differently
	- Oversample differently
	- Choosing a different classifier
- Compare different dataset and other forms of imbalance (e.g. non-linear)
- Compare different model architectures
