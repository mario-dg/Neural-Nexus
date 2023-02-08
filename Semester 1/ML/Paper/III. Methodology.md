---
- Data preparation and pre-processing: This section explains how the data is prepared and pre-processed, including any necessary data cleaning, normalization, and augmentation techniques.
- Implementation of the techniques to counteract class imbalance: This section describes the techniques used to counteract class imbalance in the CIFAR10 dataset, including over-sampling, under-sampling, and cost-sensitive learning.
- Evaluation metrics and their justification: This section outlines the evaluation metrics used to assess the performance of each technique, and explains the rationale for choosing these metrics.
- Data partitioning and cross-validation approach: This section explains how the data is split into training and testing sets, and the cross-validation approach used to ensure the robustness of the results.
---

## Data preparation and pre-processing
- No pre-processing or data-cleaning necessary, since CIFAR10 already error free
- Images are small in dimension, but rather noise free
- All images are normalized using a mean and standard deviation of 0.5 to reduce the variance of input data
$$x_{norm} = \frac{x - mean}{std}$$
- 2 augmentation compositions used
	- RandomHorizontalFlip
	- RandomVerticalFlip
	- RandomRotation
	- RandomCrop
	- ColorJitter

	- RandomHorizontalFlip
	- RandomCrop
	- ColorJitter
- Dataset was manually imbalanced using following equation
$$N_{i}=4000m^{\frac{i}{9}-1} | m=5; i=[0,9]$$
- 20338 samples in total, steadily decreasing images per class
- Largest difference 800:4000 $\equiv$ 1:5

## Implementation of the techniques to counteract class imbalance
- Inverse class frequency weight: $W_{i}=1/N_{i}$
- Balanced class weight using Scikit-learn: $W_{i}=N_{samples}/(N_{classes}*N_{i})$
- Focal Loss using both weights
$$FL(p_i) = -W_i (1 - p_i)^\gamma \log(p_i)$$
$p_i: Predicted\ probability\ of\ target\ class$
$W_i: Weight\ of\ the\ target\ class$
$\gamma:$



---
Focal Loss for Dense Object Detection
https://doi.org/10.48550/arXiv.1708.02002
Content:
- Introduces the Focal Loss
- Decreases loss for well-classified samples and increases it for missclassified ones
---