# Part 2: Computer Vision Problem Formulation and CNN Prototype

## Problem Type
Image Classification — 4 class surface defect detection

## Why Image Classification?
Each image belongs to exactly one surface condition category.
The task requires assigning a single class label per image which
makes it a multi-class classification problem. Object detection
would only be needed if we had to locate the defect region.

## Dataset Summary
- Total Images : 480 (120 per class)
- Classes      : dent, normal, scratch, stain
- Image Size   : Resized to 64x64 pixels
- Split        : 80% train / 20% test

## Preprocessing Pipeline
- Resized all images to 64x64
- Normalized pixel values by dividing by 255
- Applied augmentation on train set:
  rotation, flip, zoom, brightness, shift
- Stratified 80/20 split per class

## CNN Architecture
| Layer           | Details                  |
|-----------------|--------------------------|
| Conv2D          | 16 filters, 3x3, ReLU   |
| MaxPooling2D    | 2x2                      |
| BatchNorm       |                          |
| Conv2D          | 32 filters, 3x3, ReLU   |
| Conv2D          | 32 filters, 5x5, ReLU   |
| MaxPooling2D    | 2x2                      |
| BatchNorm       |                          |
| Conv2D          | 64 filters, 3x3, ReLU   |
| MaxPooling2D    | 2x2                      |
| Dense           | 128 neurons, ReLU        |
| Dropout         | 0.5                      |
| Dense           | 64 neurons, ReLU         |
| Output          | 4 neurons, Softmax       |

## CNN Concepts Explained
- Convolution: Filters slide over the image detecting local
  patterns like edges, corners, and textures at each layer
- Pooling: Reduces spatial size keeping dominant features,
  also makes model robust to small positional shifts
- ReLU: Removes negative activations, adds non-linearity,
  prevents vanishing gradients during backpropagation
- CNNs vs Dense Networks: Dense networks lose spatial
  structure by flattening pixels. CNNs preserve local
  relationships via weight sharing across spatial locations

## Real World Application
Agriculture — detecting crop leaf diseases by classifying
field images into healthy, bacterial infection, fungal
damage or mechanical injury categories to help farmers
take early corrective action before crop loss.

## Repository Structure
part-2-cnn-computer-vision/
├── README.md
├── notebook.ipynb
├── requirements.txt
├── sample_predictions/
│   └── prediction_outputs.png
└── results/
    ├── sample_class_images.png
    ├── accuracy_loss_curves.png
    └── confusion_matrix.png
