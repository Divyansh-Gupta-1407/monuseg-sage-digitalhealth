# monuseg-sage-digitalhealth
This paper was accepted by SAGE Digital Health 

# Automated Nucleus Segmentation in Histology Images using Attention U-Net

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge\&logo=python\&logoColor=ffdd54)
![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=for-the-badge\&logo=TensorFlow\&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-%23D00000.svg?style=for-the-badge\&logo=Keras\&logoColor=white)
![OpenCV](https://img.shields.io/badge/opencv-%23white.svg?style=for-the-badge\&logo=opencv\&logoColor=white)

## Overview

This repository contains the implementation and research documentation for automated nucleus segmentation in histopathology images using a lightweight Attention U-Net architecture.

Nucleus segmentation is a critical step in digital pathology, enabling quantitative analysis for cancer diagnosis, tumor grading, and cellular morphology studies. However, dense nuclear clusters, overlapping cells, and staining variability make accurate segmentation particularly challenging.

To address these challenges, this work combines advanced preprocessing techniques, an attention-based segmentation model, and a robust patch-stitching inference pipeline capable of producing accurate full-resolution segmentation masks.

---

## Research & Documentation

> **Abstract:** Accurate nucleus segmentation is a fundamental task in digital pathology. This study presents a lightweight Attention U-Net framework evaluated on the MoNuSeg 2018 dataset. The proposed methodology integrates stain deconvolution, image enhancement, mask refinement, patch-based training, and overlapping patch inference to improve segmentation quality. The model achieved an IoU score of **0.8745** and a Dice Coefficient of **0.9323** on unseen full-resolution test images, demonstrating the effectiveness of attention mechanisms and the proposed stitching strategy for high-resolution histopathological image analysis.

---

## Methodology & Architecture

### Task

**Semantic Nucleus Segmentation** from histopathology images.

### Architecture

The proposed model utilizes a lightweight **Attention U-Net (~2 Million Parameters)** that extends the traditional U-Net architecture through attention gates placed within skip connections.

These attention gates enable the network to:

* Focus on relevant nuclear regions
* Suppress irrelevant background information
* Improve boundary localization
* Enhance segmentation robustness

### Training Configuration

* Framework: TensorFlow / Keras
* Optimizer: Adam
* Loss Function: Binary Cross Entropy + Dice Loss
* Batch Size: 8
* Maximum Epochs: 100
* Early Stopping and Learning Rate Scheduling

---

## Preprocessing Pipeline

To improve feature visibility and model generalization, a dedicated preprocessing pipeline was developed.

### Image Processing

* Hematoxylin channel extraction via stain deconvolution
* Median filtering for noise reduction
* Contrast Limited Adaptive Histogram Equalization (CLAHE)
* Unsharp masking for boundary enhancement

### Mask Processing

* Upsampling masks from 256×256 to 1000×1000
* Multi-pass Gaussian smoothing
* Binary thresholding
* Contour refinement

---

## Patch-Based Training Strategy

Original histology images are processed at:

```text
1000 × 1000 pixels
```

To preserve fine-grained nuclear information while remaining computationally efficient:

* Images are divided into 256×256 patches
* Corresponding mask patches are extracted
* Approximately 2400 training image-mask pairs are generated

This strategy improves data utilization and serves as an effective augmentation mechanism.

---

## Inference & Stitching Pipeline

Full-resolution segmentation is performed through a multi-stage inference process:

```text
Full Resolution Image
          ↓
Overlapping Patch Generation
          ↓
Attention U-Net Prediction
          ↓
Patch Reconstruction
          ↓
Weighted Stitching
          ↓
Final Segmentation Mask
```

The weighted averaging approach minimizes edge artifacts and ensures seamless reconstruction of the final segmentation map.

---

## Evaluation Metrics

The model was evaluated on the MoNuSeg 2018 benchmark dataset using region-overlap and classification metrics.

### Performance Results

| Metric           | Score      |
| ---------------- | ---------- |
| Dice Coefficient | **0.9323** |
| IoU              | **0.8745** |
| Accuracy         | **0.9721** |
| Precision        | **0.9067** |
| Sensitivity      | **0.9602** |
| Specificity      | **0.9733** |
| AUC              | **0.9936** |

### Comparative Performance

| Model                    | Dice Score | IoU        |
| ------------------------ | ---------- | ---------- |
| Baseline U-Net           | 0.8892     | 0.8031     |
| Mask R-CNN               | 0.8876     | 0.8005     |
| CUMedVision              | 0.9079     | 0.8354     |
| Proposed Attention U-Net | **0.9323** | **0.8745** |

---

## Key Contributions

* Developed a complete nucleus segmentation workflow for digital pathology.
* Implemented a lightweight Attention U-Net architecture.
* Designed a robust preprocessing pipeline incorporating stain deconvolution.
* Proposed a high-fidelity overlapping patch stitching strategy.
* Achieved competitive results on the MoNuSeg 2018 benchmark dataset.

---

## Future Work

* Transformer-based medical image segmentation
* Instance-level nucleus segmentation
* Cross-dataset validation
* Whole-slide image processing
* Clinical deployment and scalability studies

---

## Authors

**Divyansh Gupta**
