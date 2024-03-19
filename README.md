# ML4SCI
This is my personal repository to submit my solutions to the test problems provided by ML4SCI as a selection test for GSOC'24.

![gsoc_ml4sci](https://github.com/royforestano/2023_gsoc_ml4sci_qmlhep_gnn/assets/96851867/3ed6ecda-bbe2-4e80-8e97-fa3e3b6647bf)

# Project Details

| Title                                | Layout        | Project    | Description                                                |
|--------------------------------------|---------------|------------|------------------------------------------------------------|
| Multi-Class Classification (Common Test 1) | gsoc_proposal | DEEPLENSE  | Implementing multi-class classification.  
| DDPM (Specific Test 4)               | gsoc_proposal | DEEPLENSE  | Implementing denoising diffusion probabilistic model. [This will be my GSOC'24 proposal project] |

# Diffusion Model
Image generated at first epoch
![At initial time](https://github.com/Shashankss1205/ML4SCI/blob/main/Image%20Folder/Diffusion_start.png)
Image generated at 20th epoch
![At final time](https://github.com/Shashankss1205/ML4SCI/blob/main/Image%20Folder/Diffusion_final.jpg)

# Multi-Class Classification: Common Test 1
| Model Architecture | Number of epochs | Learning rate | Training Loss | Training Accuracy | Micro-average ROC-AUC | Macro-average ROC-AUC |
|---------------------|------------------|---------------|---------------|-------------------|-----------------------|-----------------------|
| ResNet18            | 50               | 1e-4          | 0.00114       | 1                 | 1.0                   | 1.0                   |
| CNN                 | 50               | 1e-4          | 1.03          | 0.461             | 0.6626                | 0.64877               |

# ROC-AUC Curve for ResNet18:
![ROC-AUC curve for ResNet18](https://github.com/Shashankss1205/ML4SCI/blob/main/Multi-Class%20Classification%20(Common%20Test%201)/Images%20Folder/ROC_ResNet18.png)