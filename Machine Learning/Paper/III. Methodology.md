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
- Possibly some hard classes: Cat/Dog, Automobile/Truck

## Implementation of the techniques to counteract class imbalance
- Balanced using all 40000 training images
- Balanced using 20300 images of balanced classes
- Baseline 
- Inverse class frequency weight: $W_{i}=1/N_{i}$
- Balanced class weight using Scikit-learn: $W_{i}=N_{samples}/(N_{classes}*N_{i})$
- Focal Loss using both weights
$$FL(p_i) = -W_i (1 - p_i)^\gamma \log(p_i)$$
$$p_i: Predicted\ probability\ of\ target\ class$$
$$W_i: Weight\ of\ the\ target\ class$$
$$\gamma:Rate\ of\ loss\ decay\ for\ well-classified\ samples$$
- Undersampling
- Oversampling
- Augmentation 1 + Class Weight
- Augmentation 1 + Undersampling
- Augmentation 1 + Oversampling
- Augmentation 1 + Oversampling + Class Weight
- Augmentation 2 + Oversampling
- Augmentation 2 + Oversampling + Class Weight

## Evaluation metrics and their justification
- Accuracy - show that it's not a valid metric | train/val data
- F1 macro - f1 score for each class, averaged | val data
- AUROC - auroc for each class, averaged | val data
- F1 per class - see f1 score for each class individually | val data
- PR Curve - precision vs recall per class | unseen test data
- ROC - TP vs FP per class | unseen test data
- Confusion Matrix | unseen test data

## Data partitioning and cross-validation approach
- CIFAR10 train split into train + val (0.8:0.2; 40,000:10,000)
- train data imbalanced (20,338), val balanced (10,000)
- CIFAR10 test, 1000 images per class
- Undersampling, 800 images per class
- Oversampling, 4000 images per class
- train data shuffled, val and test not


---
Focal Loss for Dense Object Detection
https://doi.org/10.48550/arXiv.1708.02002
Content:
- Introduces the Focal Loss
- Decreases loss for well-classified samples and increases it for misclassified ones
---