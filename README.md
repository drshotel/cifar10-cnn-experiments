# CIFAR-10 CNN Experiments

A Convolutional Neural Network (CNN) built with PyTorch for image classification on the CIFAR-10 dataset. This project explores the effects of Batch Normalization, Dropout, and Learning Rate selection on model performance.

## Overview

The goal of this project was to design and train a CNN capable of classifying images from the CIFAR-10 dataset while investigating how different architectural and optimization choices affect performance.

Experiments were conducted on:

- Batch Normalization
- Dropout
- Learning Rate Selection
- Confusion Matrix Analysis

## Dataset

CIFAR-10 consists of 60,000 color images (32×32 pixels) across 10 classes:

- Airplane
- Automobile
- Bird
- Cat
- Deer
- Dog
- Frog
- Horse
- Ship
- Truck

## Model Architecture

```text
Input (3×32×32)

Conv2D(3 → 32, kernel=3)
BatchNorm2D
ReLU
MaxPool2D(2×2)

Conv2D(32 → 64, kernel=3)
BatchNorm2D
ReLU
MaxPool2D(2×2)

Conv2D(64 → 128, kernel=3)
BatchNorm2D
ReLU

Conv2D(128 → 128, kernel=3)
BatchNorm2D
ReLU

MaxPool2D(2×2)

Flatten

Linear(128 → 256)
Dropout(0.5)

Linear(256 → 10)
```

## Training Configuration

- Framework: PyTorch
- Optimizer: Adam
- Loss Function: CrossEntropyLoss
- Epochs: 15
- Batch Size: 64

## Baseline Results

| Epochs | Validation Accuracy |
|---------|---------|
| 3 | 68.8% |
| 15 | 77.8% |

The baseline model achieved a validation accuracy of approximately **77.8%** after 15 epochs of training.

---

# Experiment 1: Batch Normalization

## Objective

Determine whether Batch Normalization improves convergence speed and overall performance.

## Results

| Model | Final Validation Accuracy |
|---------|---------|
| Without BatchNorm | 68.9% |
| With BatchNorm | 69.5% |

### Sample Comparison

| Epoch | With BatchNorm | Without BatchNorm |
|---------|---------|---------|
| 1 | 50.1% | 45.1% |
| 5 | 65.7% | 60.7% |
| 10 | 69.9% | 67.6% |
| 15 | 69.5% | 68.9% |

### Conclusion

Batch Normalization improved convergence speed and allowed the model to reach higher validation accuracy earlier in training. Although the final performance difference was relatively small, the BatchNorm model learned more efficiently during the early epochs.

---

# Experiment 2: Learning Rate Comparison

## Objective

Identify the learning rate that provides the best trade-off between convergence speed and final accuracy.

## Results

| Learning Rate | Validation Accuracy |
|--------------|----------------------|
| 0.1 | 19.1% |
| 0.01 | 54.7% |
| 0.001 | **77.8%** |
| 0.0001 | 71.3% |

### Conclusion

The learning rate of **0.001** achieved the best performance, reaching **77.8% validation accuracy**.

A learning rate of **0.1** was too large and caused unstable optimization, while **0.0001** learned more slowly and was unable to reach the same accuracy within 15 epochs.

---

# Experiment 3: Dropout

## Objective

Evaluate the effect of dropout on model generalization.

## Results

| Configuration | Validation Accuracy |
|--------------|----------------------|
| No Dropout | 75.0% |
| Dropout (0.5) | 69.5% |

> **Note:** These dropout results should be interpreted with caution. I only tracked validation accuracy during this experiment and did not record training accuracy, making it difficult to evaluate whether dropout reduced overfitting. Future experiments should compare both training and validation accuracy.

### Conclusion

In this experiment, dropout reduced validation accuracy. This suggests that a dropout rate of 0.5 may have been too aggressive for the architecture, causing underfitting and limiting performance. 

---

# Confusion Matrix Analysis

A confusion matrix was generated using the trained model to visualize class-wise performance.

### Observations

- Visually similar classes were more likely to be confused.
- Common CIFAR-10 misclassifications included:
  - Cat ↔ Dog
  - Deer ↔ Horse
  - Automobile ↔ Truck
- Classes with distinctive visual features, such as airplanes and ships, were classified with higher accuracy.

The confusion matrix provided insight into the strengths and weaknesses of the model beyond overall accuracy.

## Results Summary

| Experiment | Key Finding |
|------------|------------|
| Batch Normalization | Improved convergence speed |
| Learning Rate | 0.001 achieved the best performance |
| Dropout | Reduced validation accuracy in this configuration |
| Best Accuracy | 77.8% Validation Accuracy |

## Technologies Used

- Python
- PyTorch
- torchvision
- scikit-learn
- Matplotlib

## Future Improvements

Potential improvements include:

- Data augmentation
- Learning rate scheduling
- Residual connections
- Deeper CNN architectures
- Hyperparameter tuning
- Transfer learning

## Feedback

I'm a second-year Software Engineering student learning machine learning.

If you notice areas where the model, experiments, or code could be improved, I'd love to hear your suggestions. Feedback and constructive criticism are always appreciated.
