# Unpaired-Image-to-Image-Translation-for-MR-to-CT-Synthesis

## 📌 Overview
This project explores **unpaired medical image translation** for **MR-to-CT brain image synthesis** using state-of-the-art GAN-based architectures. The study compares **CycleGAN**, **Augmented CycleGAN**, **Contrastive Unpaired Translation (CUT)**, and a **novel Hybrid GAN** that integrates cycle-consistency, contrastive learning, and data augmentation.

The goal is to generate **CT-like images from MR scans without paired data**, reducing the need for dual-modality acquisition in clinical workflows such as **radiotherapy planning**.

---

## 🧠 Key Contributions
- Comparative analysis of **three unpaired translation frameworks**
- Proposal of a **Hybrid GAN (Augmented CycleGAN + CUT)**
- Extensive evaluation using:
  - **FID, LPIPS**
  - **SSIM, PSNR**
  - **MSE, RMSE**
- **Explainable AI (XAI)** analysis using saliency maps and Grad-CAM
- Experiments conducted on **two unpaired MR–CT brain datasets**

---

## 🏗️ Models Implemented
### 1. CycleGAN (Baseline)
- Dual generators (MR → CT, CT → MR)
- Cycle-consistency and identity losses

### 2. Augmented CycleGAN
- On-the-fly data augmentation (rotations, flips, intensity jitter)
- Latent reconstruction loss
- Improved generalization on small datasets

### 3. CUT (Contrastive Unpaired Translation)
- Single generator–discriminator
- PatchNCE contrastive loss for content preservation
- Reduced computational complexity

### 4. Hybrid GAN (Proposed)
- Combines:
  - Cycle-consistency (CycleGAN)
  - Contrastive PatchNCE loss (CUT)
  - Data augmentation and latent reconstruction loss
- Optimized using **RMSProp**
- Achieves the best balance between realism and anatomical fidelity

---

## 📂 Datasets Used
Two publicly available **unpaired brain MR–CT datasets**:

### Dataset 1: Unpaired MR–CT Brain Dataset
- 179 axial slices  
- 90 MR (T1-weighted), 89 CT  
- Resolution: 256 × 256  

### Dataset 2: CT-to-MRI CGAN Dataset
- 402 unpaired slices (201 MR, 201 CT)
- Multi-planar views (axial, coronal, sagittal)
- Diverse scanners and slice thicknesses

### Preprocessing
- Resize/crop to 256 × 256  
- Intensity normalization to **[-1, 1]**  
- Grayscale → pseudo-RGB (3 channels)  
- 80/20 train–test split  
- Data augmentation for selected models  

---

## ⚙️ Training Configuration
- **Framework**: PyTorch  
- **Input Size**: 256 × 256 × 3  
- **Batch Size**: 1  
- **Epochs**: 100  
- **Optimizers**:
  - Adam (CycleGAN, Augmented CycleGAN, CUT)
  - RMSProp (Hybrid GAN)
- **Hardware**: NVIDIA Tesla T4 (Kaggle)

---

## 📊 Evaluation Metrics
| Category        | Metrics              |
|-----------------|---------------------|
| Distribution    | FID                 |
| Perceptual      | LPIPS               |
| Structural      | SSIM                |
| Pixel-level     | MSE, RMSE           |
| Reconstruction  | PSNR                |

---

## 🔍 Explainable AI (XAI)
- **Grad-CAM** applied to generators and discriminators
- Saliency maps highlight:
  - Ventricles
  - Cortical folds
  - Subcortical regions
- Hybrid model shows **most localized and clinically relevant attention**

---

## 🏆 Results Summary
- **Hybrid GAN outperforms all baselines**
- Lowest FID and RMSE
- Improved SSIM and PSNR
- Best trade-off between:
  - Anatomical structure
  - Perceptual realism
  - Interpretability

---

## 🚀 Applications
- Radiotherapy treatment planning
- CT-free dose calculation
- Cross-modality medical imaging
- Low-resource clinical environments
