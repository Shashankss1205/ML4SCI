## Specific Test VI. SSL on Real Dataset

| title                                                  | layout          | project                                                    | project size | year | organization                     |
|--------------------------------------------------------|-----------------|------------------------------------------------------------|--------------|------|----------------------------------|
| Learning Representation Through Self-Supervised...     | gsoc_proposal  | DEEPLENSE                                                  | 175hr        | 2023 | Alabama, Brown, BITS Pilani...   |

## Task: 
Build a Self-Supervised Learning model for classifying the images into lenses using PyTorch or Keras. Pick the most appropriate approach and discuss your strategy. 

## Dataset: 
[dataset.zip - Google Drive](https://drive.google.com/file/d/1aafE2nDp7S6j59sZcBIzP3FnQxVCmHCx/view)

## Dataset Description: 
The Dataset consists of two classes, strong lensing images with lenses and non-lenses in npy format. For non-lensing images, the images start with nl_. These images are from the Hubble Space Telescope. 

## Evaluation Metrics: 
ROC curve (Receiver Operating Characteristic curve) and AUC score (Area Under the ROC Curve). Although the dataset is small and results may not be perfect, the pipeline should be such that with more data, the model could achieve high performance.