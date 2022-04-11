# Chest-xray-classification
Classify chest x-rays as normal or abnormal using SOTA networks

Chest x-ray uses a very small dose of ionising radiation to produce pictures of the inside of the chest. It is used to evaluate the lungs, heart and chest wall and may be used to help diagnose shortness of breath, persistent cough, fever, chest pain or injury. It is a common examination which is judged by radiologists to decide if any disease is present or not. Since it is widely used, the amount of x-rays to be processed by radiologists can be quite high, which leads to a burden on them.

For this, we plan to classify an x-ray as normal or abnormal. This will save radiologists a lot of time as the normal x-rays will be eliminated from their workload. They will only have to process the abnormal scans for diseases. But it is required that we reach a good accuracy to prevent any misdiagnosis.

### Dataset: <br />
The dataset used was the CheXpert dataset. It is a large dataset of chest X-rays and competition for automated chest x-ray interpretation, which features uncertainty labels and radiologist-labeled reference standard evaluation sets. It contains 224,316 chest radiographs of 65,240 patients. It shows the presence of 14 diseases like (a) Atelectasis, (b) Cardiomegaly, (c) Consolidation, (d) Edema, and (e) Pleural Effusion

Chexpert dataset contains different kinds of labels. For 14 findings, the labels are -1, 0, 1, where -1 is for uncertain whether disease exists or not, 0 is that the scan is abnormal and 1 that scan is normal. Another important detail is that the dataset is very unbalanced, with abnormal cases more than normal ones. This dataset has two types of scans, frontal and lateral.

Two state-of-the-art papers were implemented. The  first paper used [1] reported accuracy for binary classification (normal vs abnormal) as 0.89 using a pretrained (ImageNet) model and 0.88 for a model trained from scratch. The model used in this paper is ResNet18 for 180 000 training images and 1000 testing images. This paper uses data with an imbalance of 79% abnormal scans

The second paper implemented was the Chexpert’s official paper[2]. The pipeline for this paper was to train two models on frontal and lateral scans separately. Then take predictions for both scans from their respective models. The test results for both types of scans are ensembled to give the final accuracy.

## Pre-processing

Image processing algorithm does the following:
1. histogram equalization for contrast enhancement
2. normalization
3. resizing to a size of (320x320)

![output](https://github.com/amalmsaleem/Chest-xray-classification/blob/main/Image/image.png)

For label preprocessing, uncertain labels of diseases were replaced with 0s. This was decided by looking at Chexpert’s official paper [2]. Moreover, a subset of the dataset was created with a class balance (normal vs abnormal) of 50%, with cases of every disease accounted approximately equally in abnormal cases. And frontal and lateral scans were separated. For training,12159 lateral scans were used of which 2103 were for validation. Similarly, for frontal scans, training is done on 32,073 scans and validation on 6184 scans.

## Model
For 3 separate diseases 3 Densenet121 models were trained and ensembled to get predictions.

## Results
Test accuracy following this pipeline is 83.12%.

![output](https://github.com/amalmsaleem/Chest-xray-classification/blob/main/Image/results.png)

