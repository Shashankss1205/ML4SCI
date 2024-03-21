## Common Test I. Multi-Class Classification 

| Title                                | Layout        | Project                | Project Size | Year |
|--------------------------------------|---------------|------------------------|--------------|------|
| Multi-Class Classification | gsoc_proposal | DEEPLENSE | 175hr | 2024 |

## Task: 
Build a model for classifying the images into lenses using PyTorch or Keras. Pick the most appropriate approach and discuss your strategy.

## Dataset: 
[dataset.zip - Google Drive](https://drive.google.com/file/d/1ZEyNMEO43u3qhJAwJeBZxFBEYc_pVYZQ/view) - Google Drive

## Dataset Description: 
The Dataset consists of three classes, strong lensing images with no substructure, subhalo substructure, and vortex substructure. The images have been normalized using min-max normalization, but you are free to use any normalization or data augmentation methods to improve your results.

## Evaluation Metrics: 
ROC curve (Receiver Operating Characteristic curve) and AUC score (Area Under the ROC Curve) 
