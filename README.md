# Deep Learning Project Submission

## Overview

This repository contains the implementation for the assigned tasks under the project guidelines. The work includes:

- Common Test Implementation
- Specific Task VII
- Specific Task IX (A)
- Specific Task IX (B)

All models were trained and evaluated using a 90:10 train-test split as required. Evaluation metrics are reported on the validation set.


---

## Methodology

### Data Processing
- Dataset loading and preprocessing performed using PyTorch and standard utilities.
- 90:10 train-test split applied.
- Data normalization and transformations applied where necessary.

### Model Architecture
The models were implemented using PyTorch.

Model selection was based on:
- Suitability for classification task
- Strong generalization performance
- Compatibility with evaluation metrics such as Accuracy and AUC

### Training Setup
- Optimizer: Adam
- Loss Function: CrossEntropyLoss (for classification)
- Learning Rate: 1e-4 (configurable)
- Device: CUDA (if available)

---

## Evaluation Metrics

Validation metrics reported include:

- Accuracy
- AUC Score
- Phys score (if applicable to task)

Metrics are computed on the 10% held-out validation set.


## Model Weights

If trained weights are included:

- Saved in `.pt` or `.pth` format
- Located in the `models/` directory

If not included due to size limitations, they can be shared upon request.

---

## Hardware & Environment

Training was performed on:

- Platform: Google Colab
- GPU: NVIDIA Tesla T4 (16GB VRAM)
- Python: 3.10
- Framework: PyTorch

CUDA acceleration was used for faster model training.

---

## Author

Name: Sarthak Jagota  
GitHub: https://github.com/SarthakJagota
Email: sarthakjagota34@gmail.com

---

## Notes

- All results are reproducible by running the notebooks.
- Code is modular and well-structured for clarity.
- Submission follows the official guidelines.


