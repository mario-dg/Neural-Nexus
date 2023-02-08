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