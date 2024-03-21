## Specific Test IV. SSL on Real Dataset 

| title                                                  | layout          | project                                                    | project size | year | organization                     |
|--------------------------------------------------------|-----------------|------------------------------------------------------------|--------------|------|----------------------------------|
| Learning Representation Through Self-Supervised...     | gsoc_proposal  | DEEPLENSE                                                  | 175hr        | 2024 | Alabama, Brown, BITS Pilani...   |

# Rotational Augmentation
## Link to Colab Notebook:
https://colab.research.google.com/drive/1MrrI02G3gaOXldxojqdOSMHk6EHyW3X1?usp=sharing

## Link to Model weights:
https://drive.google.com/drive/folders/1a3z4W_eEtv1m4GJhGF_n8IRE6OybO8el?usp=sharing

# Gaussian Blur Augmentation
## Link to Colab Notebook:
https://colab.research.google.com/drive/13xumzicKExRXCmx2qSAbsFmrWeBAoeHe?usp=sharing

## Link to Model weights:
https://drive.google.com/drive/folders/1I9PJfZoezdR4UkpBnyK3oL86DVqT1nXg?usp=sharing


## Approaching the Task: 

1) Having an academic background in Mechanical Engineering and thermodynamics helped me better understand the working of the probabilistic denosing of the images.
2) My first step was to take a look over all the references provided in the problem statement and gather the relevant data.
3) Secondly, I went onto study and analyse the model architecture from the research paper.
4) Lastly, I started implementing the research paper in my notebook taking reference from the implementations of diffusion models on CIFAR10 dataset.

## Introduction to SSL(Self-Supervised Learning):

The goal of self-supervised learning is to minimize or altogether replace the need for labeled data. While labeled data is relatively scarce and expensive, unlabeled data is abundant and relatively cheap. Essentially, pretext tasks yield “pseudo-labels” from unlabeled data. The term “pretext” implies that the training task is not (necessarily) useful unto itself: it is useful only because it teaches models data representations that are useful for the purposes of subsequent downstream tasks. Pretext tasks are thus also often referred to as representation learning.

Models pre-trained with SSL are often fine-tuned for their specific downstream tasks: this fine-tuning often involves true supervised learning (albeit with a fraction of the labeled data needed to train a model with supervised learning alone).

Though the discipline of SSL is diverse in both methodology and use cases, models trained with SSL use one (or both) of two machine learning techniques: self-predictive learning and contrastive learning.
![SSL](https://github.com/Shashankss1205/ML4SCI/blob/main/Image%20Folder/ssl_architecture.png)

## Model Architecture:

U-Net, originally developed for semantic segmentation, is an architecture that is widely used for implementing diffusion models but with some slight modifications:

1) The network accepts two inputs: Image and time step
2) Self-attention between the convolution blocks once we reach a specific resolution (16x16 in the paper)
3) Group Normalization instead of weight normalization
![Model Architecture](https://github.com/Shashankss1205/ML4SCI/blob/main/Image%20Folder/encoder_decoder.png)


## Working Methodology:

Implementing a SSL model is simple. I define a model that takes Images as inputs and then performs a pretext task onto them. After training on pretext task, the model's head is changed to a classification head for image classification:

1) Define a pretext task, such as similarity/difference detection after rotation or gaussian blurring, to automatically generate labeled data pairs (X,y) without human involvement.
2) Train a neural network on the pretext task to learn general features of the data distribution.
3) Extract feature layers from the pre-trained model and combine them with task-specific final layers.
4) Fine-tune the model on the downstream task using a limited amount of labeled data, achieving good performance with less human annotation.

## Evaluation Metrics: 

1) In the Rotational fine-tuned model, the value of RUC-AOC curve is high compared to supervised model, because of the pretext training.
![ROC-AUC curve for Rotational](https://github.com/Shashankss1205/ML4SCI/blob/main/SSL%20on%20Real%20Dataset%20(Specific%20Test%206)/Gaussian/ROC-AUC.png)

2) In the Gaussian Blur fine-tuned model, the value of RUC-AOC curve is high compared to supervised model, because of the pretext training.
![ROC-AUC curve for Gaussian Blur](https://github.com/Shashankss1205/ML4SCI/blob/main/SSL%20on%20Real%20Dataset%20(Specific%20Test%206)/Gaussian/ROC-AUC.png)

## Possible Improvisations:

There are a few things that I can try to improve the model:

1) Experiment with different data augmentation techniques to create diverse views of input data. Explore advanced augmentation methods such as CutMix, MixUp, or RandAugment to generate more informative pretext tasks.

2) Explore transfer learning techniques to leverage knowledge learned from pretext tasks for downstream tasks.

## References:

1. [Self-Supervised Learning Model](https://github.com/ML4SCI/DeepLense/tree/main/Deeplens_Self_Supervised_Learning_Yashwardhan_Deshmukh)
2. [Contrastive Learning for SSL](https://arxiv.org/pdf/2305.17326v5.pdf)
