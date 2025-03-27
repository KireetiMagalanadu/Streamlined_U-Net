# Streamlined U-Net for Brain Tumor Segmentation

## Overview

This repository contains the implementation and experimental evaluation of a streamlined U-Net architecture designed specifically for brain tumor segmentation in MRI images. The project addresses the challenges of model complexity and deployment on resource-constrained devices by integrating several optimization strategies.

## Motivation

Brain tumor detection and segmentation are critical for early diagnosis and treatment planning. However, conventional models such as the original U-Net, with approximately 31 million trainable parameters, demand extensive computational resources. This project aims to balance segmentation accuracy with computational efficiency by:
- Reducing model parameters significantly.
- Maintaining high segmentation performance.
- Enabling deployment on edge devices.

## Key Contributions

- **Optimized U-Net Architecture:** Tailored lightweight U-Net that reduces the number of parameters (up to 80% in some experiments) while retaining accurate segmentation.
- **Optimization Techniques:** Integration of depthwise separable convolutions and low-rank factorization into the U-Net framework.
- **Comprehensive Evaluation:** Detailed analysis comparing the baseline lightweight U-Net with models optimized using:
  - Low-rank factorization.
  - Depthwise separable convolution.
  - A combined approach of both techniques.
- **Trade-Off Analysis:** In-depth discussion on the balance between model size reduction and segmentation accuracy, including practical implications for clinical deployment.

## Methodology

1. **Data Collection and Pre-processing:**  
   - Utilized the LGG MRI Segmentation dataset from Kaggle.
   - Applied systematic pre-processing (resizing, normalization, and augmentation) to standardize MRI scans and segmentation masks.

2. **Lightweight U-Net Construction:**  
   - Built upon a modified U-Net architecture with significantly fewer parameters (~457,617) compared to the original design.
   - Adapted skip connections to reduce computational overhead while preserving essential spatial features.

3. **Optimization Strategies:**  
   - **Depthwise Separable Convolution:** Replaces standard convolutions to reduce computational cost (up to an 80% reduction in parameters).
   - **Low-Rank Factorization:** Decomposes convolutional filters to lower the parameter count by about 58%.
   - **Combined Approach:** Integrates both techniques, achieving a balanced reduction (~50% reduction) with improved segmentation performance.

4. **Training and Evaluation:**  
   - Models were trained using the Adamax optimizer with a learning rate of 0.001.
   - Evaluation metrics included Dice Coefficient, Intersection over Union (IoU), accuracy, and loss curves.
   - Experiments also included failed attempts with model pruning and quantization due to TensorFlow optimization constraints.

## Experiments and Results

- **Experiment 0 (Pruning & Quantization):**  
  Failed to apply due to the non-linear nature of the U-Net architecture.

- **Experiment 1 (Low-Rank Factorization):**  
  Reduced parameters from 457,617 to ~185,457. Achieved Dice coefficients around 0.85–0.89.

- **Experiment 2 (Depthwise Separable Convolution):**  
  Reduced parameters to ~102,460. Achieved competitive segmentation accuracy with Dice coefficients in the mid-80% range.

- **Experiment 3 (Combined Approach):**  
  Resulted in approximately 221,500 parameters with the highest Dice coefficient (~0.88 on test data), striking an optimal balance between efficiency and accuracy.

## Limitations

- **Data Limitations:**  
  The training data is limited and may not capture the full variability of clinical scenarios.
- **Domain Shift:**  
  MRI images from different devices and protocols may affect the model’s performance.
- **Optimization Constraints:**  
  Techniques like pruning and quantization were not effective due to TensorFlow’s constraints with non-linear architectures.

## Future Work

- Expand and diversify the training dataset to improve model generalizability.
- Investigate hybrid optimization techniques and domain adaptation strategies.
- Develop a user-friendly interface for real-time clinical decision support.




