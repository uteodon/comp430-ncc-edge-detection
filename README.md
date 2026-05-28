# Noise-Aware Automatic Threshold Selection for Robust Canny Edge Detection

[![Python](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the official implementation of the **Noise-Calibrated Canny (NCC)** edge detection framework, developed as a final term project for the **COMP430 Digital Image Processing** course.

## 📌 Overview

The classical Canny edge detector requires manual tuning of the Gaussian smoothing scale and hysteresis thresholds, making it highly sensitive to varying noise conditions. This project introduces a self-calibrating pipeline that automatically derives both the smoothing parameter and the hysteresis thresholds from a single per-image noise estimate. 

### Key Contributions:
1. **Robust Noise Estimation:** Uses Median Absolute Deviation (MAD) of the Laplacian residual to estimate the noise floor.
2. **Adaptive Smoothing:** Scales the Gaussian blur $\sigma$ proportionally to the estimated noise.
3. **Noise-Proportional Thresholding:** Dynamically calculates high and low hysteresis thresholds to prevent noise-induced gradient responses while preserving true structural edges.

## 📊 Dataset & Degradation
The experiments are conducted on 50 test images from the **Berkeley Segmentation Dataset (BSDS500)**. To evaluate robustness, synthetic Additive White Gaussian Noise (AWGN) is injected into the images at three severity levels: **σ = 5, 10, and 25**.

## 🛠️ Repository Structure

* `digital_image.ipynb`: The main Google Colab notebook containing the entire pipeline.
* `results_summary.csv`: Quantitative benchmarking results (Precision, Recall, F-measure) for all methods across all noise levels.
* `ablation_summary.csv`: Results of the ablation study isolating the effects of adaptive smoothing and adaptive thresholding.
* `results/`: Generated plots including F-measure comparisons, Precision-Recall curves, visual edge map comparisons, and hyperparameter sensitivity graphs.

## 🚀 How to Run (Reproducibility)

The entire pipeline is self-contained within a single Jupyter Notebook, designed to run seamlessly on Google Colab.

1. Open `digital_image.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Go to the menu bar and select **Runtime > Run all**.
3. The notebook will automatically:
   * Download and extract the BSDS500 dataset.
   * Inject synthetic noise into the test images.
   * Run the baseline methods (Sobel, Standard Canny, Otsu-Canny) and the proposed NCC method.
   * Calculate objective metrics (Precision, Recall, F-measure).
   * Generate and display all comparative plots and data tables.
   * Export the results to CSV files.

## 📈 Results Summary

Experimental results demonstrate that standard methods (like Otsu-Canny and Standard Canny) operate in a high-recall but extremely low-precision regime under heavy noise (σ=25). The proposed **NCC method** successfully filters out noise-induced gradients while preserving true boundaries, achieving a superior and balanced F-measure across all tested noise levels.

| Method | σ | Precision | Recall | F-measure |
| :--- | :---: | :---: | :---: | :---: |
| Standard Canny | 25 | 0.1739 | 0.9840 | 0.2906 |
| Otsu-Canny | 25 | 0.1726 | 0.9884 | 0.2891 |
| Sobel | 25 | 0.3205 | 0.8929 | 0.4454 |
| **NCC (Proposed)** | **25** | **0.5032** | **0.5503** | **0.5081** |

## 👨‍💻 Author
**Dilhan Deniz**  
Department of Computer Engineering  
Abdullah Gül University, Kayseri, Turkey
