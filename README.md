# TinyESPCN-SR
# 🧠 TinyESPCN Super-Resolution

## 📘 Overview
This repository implements a **lightweight and efficient image super-resolution pipeline** built on a modified **TinyESPCN (Efficient Sub-Pixel Convolutional Network)**.  
The model is designed for **real-time image upscaling** with **high perceptual quality** and **low computational cost**, making it ideal for deployment on **edge devices**.

The project follows a **two-phase training strategy**:
1. **Base Training:** The model is first trained on the **LSDIR dataset**, enabling it to learn general image reconstruction and texture recovery.
2. **Fine-tuning:** The pretrained model is then fine-tuned using **20,000 random images from the CelebA dataset**, improving its ability to reconstruct natural skin textures and facial structures.

---

## 🚀 Key Features
- ⚡ **Tiny architecture** – highly optimized for speed and memory efficiency.
- 🧩 **Enhanced layers** – integrates **channel attention** and **residual refinement blocks**.
- 🎯 **Hybrid loss** – combination of **pixel-wise (L1)**, **VGG perceptual**, **edge**, and **LAB color losses**.
- L_total = 0.6 * L1_loss + 0.2 * VGG_perceptual_loss + 0.1 * Edge_loss + 0.1 * LAB_color_loss
    Where:
    
    L1_loss → pixel-wise accuracy.
    
    VGG_loss → maintains perceptual similarity.
    
    Edge_loss → enhances sharp details.
    
    LAB_color_loss → ensures color fidelity.
- 🧍‍♂️ **Domain adaptation** – fine-tuned on facial image dataset for realism and smooth textures.
- 🖼️ **Single-image inference** – supports bicubic downsampling and real-time super-resolution.
- 💻 **Fully implemented in PyTorch** – modular and extendable for 2×, 3×, or 4× upscaling.

---

## 🧮 Model Architecture

### 🔹 Overview
The **TinyESPCN** is a lightweight adaptation of the ESPCN (Shi et al., 2016), enhanced with:
- Compact convolutional feature extractor.
- Channel attention mechanism for adaptive feature weighting.
- Sub-pixel convolution for efficient upscaling (avoids checkerboard artifacts).
- Residual refinement blocks to stabilize training and improve fine textures.

### 🏗️ Architecture Summary

Input (Low-Resolution Image)
│
▼
Conv Layer (3×3, ReLU Activation)
│
▼
10 × Residual Blocks (Each: Conv + ReLU)
│
▼
Channel Attention Module
│
▼
Conv Layer (3×3) → Pixel Shuffle (Scale = 2)
│
▼
Skip Connection (+ Bicubic Upsampled Input)
│
▼
Output (Super-Resolved Image)

### 🔹 Key Components

| Component  | Description |
|------------|-------------|
| **Conv Layers** |       Extract low-level and high-level spatial features. |
| **Residual Blocks** |   Preserve contextual information and stability during training. |
| **Channel Attention** | Dynamically re-weights channels to emphasize important features. |
| **Pixel Shuffle** |     Rearranges feature maps for efficient upscaling by a factor of 2. |
| **Skip Connection** |   Adds bicubic-upsampled input to retain structural details. |

### 🔹 Output
- Produces a **2× upscaled high-resolution image**.
- Final image combines **learned details** from the network and **smooth structure** from the bicubic interpolation.


---

## 🧰 Datasets Used

### 1️⃣ LSDIR (Large Scale Dataset for Image Restoration)
- Used for **base training**.
- Contains paired **Low-Resolution (LR)** and **High-Resolution (HR)** images.
- Provides diverse spatial textures for generic super-resolution learning.

### 2️⃣ CelebA Subset
- Used for **fine-tuning**.
- **20,000 random face images** selected for domain adaptation.
- Focuses on facial feature enhancement, texture preservation, and tone correction.
- Cropped and aligned faces resized to **128×128** resolution.

---

@misc{tinyespcn2025,
  author = {Rishi Kumar Saawarn},
  title = {TinyESPCN: Lightweight Super-Resolution using LSDIR and CelebA Fine-Tuning},
  year = {2025}
}



