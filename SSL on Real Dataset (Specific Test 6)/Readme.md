## Specific Test IV. SSL on Real Dataset 

| title                                                  | layout          | project                                                    | project size | year | organization                     |
|--------------------------------------------------------|-----------------|------------------------------------------------------------|--------------|------|----------------------------------|
| Learning Representation Through Self-Supervised...     | gsoc_proposal  | DEEPLENSE                                                  | 175hr        | 2024 | Alabama, Brown, BITS Pilani...   |

# Rotational Augmentation
## Link to Colab Notebook:
https://colab.research.google.com/drive/1mioRlVC_bTNEvhTLoNOFqjMNKmBBF1uJ?usp=sharing

## Link to Model weights:
https://drive.google.com/drive/folders/1a3z4W_eEtv1m4GJhGF_n8IRE6OybO8el?usp=sharing

# Gaussian Blur Augmentation
## Link to Colab Notebook:
https://colab.research.google.com/drive/13xumzicKExRXCmx2qSAbsFmrWeBAoeHe?usp=sharing

## Link to Model weights:
https://drive.google.com/drive/folders/1I9PJfZoezdR4UkpBnyK3oL86DVqT1nXg?usp=sharing


## Approaching the Task: 

1) Having a background in image classification and generation, It was easy to work with the dataset provided.
2) My first step was to take a look over the dataset provided in the problem statement and gather the relevant information regarding gravitational lensing and how does it affect an image.
3) Secondly, I went onto study and analyse the model architecture and chose contrastive methods of SSL because of its vast use-case, light architecture and high accuracy.
4) Lastly, I started implementing the code in my notebook taking reference from the implementations of a reference notebook created by ML4SCI in GSOC previous year.
5) While writing my code, I suffered from NaN loss after training my model various times and bringing relevant changes, finally leading me to realize that the input data itself has some NaN values to take care of.

## Introduction to SSL(Self-Supervised Learning):

The goal of self-supervised learning is to minimize or altogether replace the need for labeled data. While labeled data is relatively scarce and expensive, unlabeled data is abundant and relatively cheap. Essentially, pretext tasks yield “pseudo-labels” from unlabeled data. The term “pretext” implies that the training task is not (necessarily) useful unto itself: it is useful only because it teaches models data representations that are useful for the purposes of subsequent downstream tasks. Pretext tasks are thus also often referred to as representation learning.

Models pre-trained with SSL are often fine-tuned for their specific downstream tasks: this fine-tuning often involves true supervised learning (albeit with a fraction of the labeled data needed to train a model with supervised learning alone).

Though the discipline of SSL is diverse in both methodology and use cases, models trained with SSL use one (or both) of two machine learning techniques: self-predictive learning and contrastive learning.
![SSL](https://github.com/Shashankss1205/ML4SCI/blob/main/Image%20Folder/ssl_architecture.png)

## Model Architecture:

Self-supervised learning methods encompass three key components:

1) The encoder or feature extractor, responsible for automatically extracting essential image features into vectors
2) Data augmentation, which enhances encoder training by providing diverse perspectives of images through strategies like Resized Crop and Color Jitter
3) Contrastive learning methods, employing positive and negative pairs to train encoders using contrastive loss
![Model Architecture](https://github.com/Shashankss1205/ML4SCI/blob/main/Image%20Folder/encoder_decoder.png)


## Working Methodology:

Implementing a SSL model is simple. I define a model that takes Images as inputs and then performs a pretext task onto them. After training on pretext task, the model's head is changed to a classification head for image classification:

1) Define a pretext task, such as similarity/difference detection after rotation or gaussian blurring, to automatically generate labeled data pairs (X,y) without human involvement.
2) Train a neural network on the pretext task to learn general features of the data distribution.
3) Extract feature layers from the pre-trained model and combine them with task-specific final layers.
4) Fine-tune the model on the downstream task using a limited amount of labeled data, achieving good performance with less human annotation.

## Evaluation Metrics: 

1) In the Rotational fine-tuned model, the value of RUC-AOC curve is high, because of the pretext training.
![ROC-AUC curve for Rotational](https://github.com/Shashankss1205/ML4SCI/blob/main/SSL%20on%20Real%20Dataset%20(Specific%20Test%206)/Rotational/ROC-AUC.png)

2) In the Gaussian Blur fine-tuned model, the value of RUC-AOC curve is high, because of the pretext training.
![ROC-AUC curve for Gaussian Blur](https://github.com/Shashankss1205/ML4SCI/blob/main/SSL%20on%20Real%20Dataset%20(Specific%20Test%206)/Gaussian/ROC-AUC.png)

## Possible Improvisations:

There are a few things that I can try to improve the model:

1) Experiment with different data augmentation techniques to create diverse views of input data. Explore advanced augmentation methods such as CutMix, MixUp, or RandAugment to generate more informative pretext tasks.

2) Explore transfer learning techniques to leverage knowledge learned from pretext tasks for downstream tasks.

## References:

1. [Self-Supervised Learning Model](https://github.com/ML4SCI/DeepLense/tree/main/Deeplens_Self_Supervised_Learning_Yashwardhan_Deshmukh)
2. [Contrastive Learning for SSL](https://arxiv.org/pdf/2305.17326v5.pdf)
