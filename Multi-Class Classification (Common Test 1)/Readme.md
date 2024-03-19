## Common Test I. Multi-Class Classification

| Title                                | Layout        | Project    | Year |
|--------------------------------------|---------------|------------|------|
| Multi-Class Classification           | gsoc_proposal | DEEPLENSE  | 2024 |

## Link to Colab Notebook:
https://colab.research.google.com/drive/1Kpd543qfX0U0D3-bLM8f9Ql4_A6_vbgl?usp=sharing

## Link to Model weights:
https://drive.google.com/drive/folders/1r5QUIbUqeRvldYiJdN6RChNDHWXBb5y6?usp=sharing

## Approaching the Task: 

1) Having a background in image classification and generation, It was easy to work with the dataset provided.
2) My first step was to take a look over the dataset provided in the problem statement and gather the relevant information regarding the three classes, strong lensing images with no substructure, subhalo substructure, and vortex substructure.
3) Secondly, I went onto study and analyse the model architecture and chose ResNet18 because of its vast use-case, light architecture and high accuracy.
4) Lastly, I started implementing the code in my notebook taking reference from the implementations of a reference notebook created by ML4SCI in a hackathon, 3 years ago.

## Introduction to Strong Lensing Challenge - Multi-Class Classification:

Gravitational lensing has been a cornerstone in many cosmology experiments and studies since it was discussed in Einstein’s calculations back in 1936 and discovered in 1979, and one area of particular interest is the study of dark matter via substructure in strong lensing images. In this challenge, I focus on exploring the potential of supervised models in identifying dark matter based on simulated strong lensing images with different substructure.

This is an example notebook for the Multi-Class Classification Challenge. In this notebook, I demonstrated 2 models:

1) A Resnet18 model implemented using the PyTorch library to solve the task of multi-class classification of strong lensing images.
2) A simple CNN model implemented using the PyTorch library to solve the task of multi-class classification of strong lensing images.

## Model Architecture:

### Residual Block
1) A basic building block used in ResNet, consisting of two convolutional layers with batch normalization and ReLU activation applied after each convolutional layer.
2) The input is added to the output of the second convolutional layer, allowing the model to learn residual mappings.
3) A downsample layer is applied to match the dimensions of the input and output.

### ResNet Model
1) Begins with a convolutional layer followed by batch normalization and ReLU activation.
2) Max-pooling layer is applied.
3) Three layers of residual blocks are stacked, with different numbers of blocks in each layer.
4) An adaptive average pooling layer is applied to convert the spatial dimensions of the feature maps to 1x1.
5) Finally, a fully connected layer is used for classification.

### ResNet18 Model Instance
1) Created using the ResNet class with ResidualBlock as the basic block and a configuration of [2, 2, 2] for the number of blocks in each layer.
2) This follows the ResNet18 architecture, which consists of 2 blocks in each of the three layers.
![Model Architecture](https://github.com/Shashankss1205/ML4SCI/blob/main/Multi-Class%20Classification%20(Common%20Test%201)/Images%20Folder/ResNet18.png)

## Working Methodology:

Implementing a ResNet18 model is simple:

1) Implemented the ResNet18 architecture for multiclass image classification, with modifications in the final fully connected layer to accommodate the number of classes specific to the problem (e.g., classes representing different types of dark matter substructure).
2) Chose an appropriate loss function for multiclass classification tasks, such as cross-entropy loss, which penalizes the model based on the difference between predicted and actual class probabilities.
3) Utilized optimization algorithms such as Adam, stochastic gradient descent (SGD), or RMSProp to train the model.

## Evaluation Metrics: 

1) In the ResNet18 Model, the value of RUC-AOC curve is very high, because of the complex model architecture.
![ROC-AUC curve for ResNet18](https://github.com/Shashankss1205/ML4SCI/blob/main/Multi-Class%20Classification%20(Common%20Test%201)/Images%20Folder/ROC_ResNet18.png)

2) The AUC score is very low here, since I have trained a basic CNN model.
![ROC-AUC curve for CNN](https://github.com/Shashankss1205/ML4SCI/blob/main/Multi-Class%20Classification%20(Common%20Test%201)/Images%20Folder/ROC_CNN.png)

## Possible Improvisations:

There are a few things that I can try to improve the model:

1) While ResNet18 is relatively shallow, deeper variants such as ResNet34, ResNet50, ResNet101, and ResNet152 are commonly used for more complex tasks and datasets.

2) Augment training data with techniques like random rotations, flips, crops, and color jittering. This helps to increase the diversity of the training data and improve the model's generalization ability.

## References:

1. [GravitationalLensingChallenge by ML4SCI](https://github.com/ML4SCI/ML4SCIHackathon/tree/main/GravitationalLensingChallenge)



