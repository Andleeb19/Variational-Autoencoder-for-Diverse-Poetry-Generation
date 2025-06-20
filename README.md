# Poetry VAE: A Variational Autoencoder for Diverse Poetry Generation


## 📜 Overview

**Poetry VAE** is a deep learning model based on **Variational Autoencoders (VAEs)**, designed to generate creative and stylistically diverse poems. Built with an encoder-decoder architecture and enhanced by **self-attention mechanisms**, this project explores the computational creativity domain by learning meaningful representations of poetic structure and content from real-world poetic corpora.

---

## ✨ Features

- Variational Autoencoder with bidirectional LSTM encoder and decoder.
- Integrated self-attention mechanism for better contextual encoding.
- Latent space visualization using t-SNE and PCA.
- Repetition penalization and temperature-based sampling for poetry generation.
- Training dynamics tracking: loss curves, KL divergence, perplexity.
- Supports controlled and diverse text generation.

---

## 📝 Dataset

- **Source**: [Poetry Foundation Dataset - Kaggle](https://www.kaggle.com/datasets/tgdivy/poetry-foundation-poems)
- **Size**: ~13,800 poems, filtered to 5,591 high-quality entries.
- **Split**: 
  - Train: 64%  
  - Validation: 16%  
  - Test: 20%

---

## ⚙️ Model Architecture

- **Encoder**:
  - Embedding Layer (dim=256)
  - Bidirectional LSTM (2 layers, 512 hidden units)
  - Self-attention module
  - Outputs mean & log variance vectors for latent space

- **Latent Space**:
  - 128-dimensional latent representation
  - Reparameterization trick for sampling

- **Decoder**:
  - LSTM (2 layers, 512 hidden units)
  - Latent vector concatenated with input at each time step
  - Softmax over vocabulary

---

## 🛠️ Training Details

- **Loss Function**:  
  `Loss = CrossEntropy + β * KL Divergence`  
  with β annealed from 0 → 1 over 15 epochs

- **Optimizer**: Adam (`lr=0.001`, scheduler applied)
- **Regularization**:
  - Dropout: 0.5
  - Early stopping (patience = 7)
- **Training Duration**: ~8 epochs (early stopping)

---

## 🎨 Generation Techniques

- **Temperature Sampling**: Ranges from 0.5 (deterministic) to 1.1 (creative/random)
- **Repetition Penalization**: Bigram blocking + frequency-based token penalization
- **Post-processing**:
  - Removal of unknown tokens
  - Line break insertion
  - Repetition filtering

---

## 📈 Results & Analysis

| Metric              | Value (Best VAE) |
|---------------------|------------------|
| Accuracy            | —                |
| Validation Perplexity | ~1100         |
| KL Divergence       | ~1e-5 (KL collapse observed) |
| Training Loss       | ↓ from ~7.1 to ~4.2 |
| Generation Quality  | Diverse but incoherent at high temperatures |
| Latent Space        | Thematically clustered poems (via t-SNE, PCA) |

---

## 🖼️ Visualizations

- Training & validation loss curves
- KL divergence trends
- t-SNE / PCA plots of latent space
- Attention heatmaps per poem
- Examples of generated poems across temperature settings

---

## 📊 Evaluation

| Temperature | Sample Quality       | Perplexity |
|-------------|----------------------|------------|
| 0.5         | Coherent, repetitive | 1075.3     |
| 0.7         | Balanced              | 1096.8     |
| 0.9         | Diverse, less coherent | 1112.4   |
| 1.1         | Most creative, least coherent | 1124.6 |
