# V-JEPA Latent Feature Extraction and Inference Pipeline

**Author:** Alejandro Meza Tudela

This repository implements a robust inference and visualization pipeline for **V-JEPA (Vision-Joint Embedding Predictive Architecture)** applied to autonomous driving datasets (such as **BDD100K** and **PIE**)[. By analyzing the model's high-dimensional latent space, we can interpret how a self-supervised "World Model" understands driving environments without human-labeled data.

---

## 📄 Documentation & Presentation

For a complete breakdown of the theoretical background, experimental setup, latent distance metrics (Cosine vs. Euclidean), and situational evaluations (traffic state shifts, traffic lights, pedestrian detection), please refer to the detailed presentation deck:

* 📊 **Presentation Deck:** [`docs/V-JEPA-SELF-DRIVING.pptx`](docs/V-JEPA-SELF-DRIVING.pptx)

---

## 📌 Overview

This project focuses on extracting and visualizing the "internal thoughts" of the V-JEPA model. Instead of looking at raw pixels, we project the model's embeddings into interpretable manifolds to track semantic transitions and "surprise" during continuous driving sequences.

---

## 📊 Analytical Visualizations

The dashboard provides three distinct views into the model's state:

* **Latent Topology (Manifold Map):** A 2D PCA projection of the 1024-D feature space. Distance between points represents semantic similarity; clusters represent stable environmental states (e.g., highway cruising vs. intersection navigation).
* **Latent Velocity (Semantic Surprise):** Calculated via Cosine distance and Euclidean magnitude shifts between consecutive embeddings. Peaks in this "pulse" identify critical events—such as sudden braking, acceleration, or lane changes—where the model detects a significant shift in the situational context.
* **Spatial Semantics:** A $14 \times 14$ grid revealing the model’s tokenized understanding. This unsupervised spatial representation demonstrates how V-JEPA groups related visual objects (road, cars, sky) through temporal consistency.

---

## 🎬 V-JEPA Inference Dashboard Demo

[![V-JEPA Model Dynamics](https://img.youtube.com/vi/1W32YP6wckc/0.jpg)](https://youtu.be/1W32YP6wckc)

*Click the image above to watch the full-resolution demo on YouTube.*

---

## 🔍 Key Findings

Through this inference pipeline, we have verified that **V-JEPA’s latent state is highly sensitive to macro-environmental dynamics**:

* **Macro-Kinematic Detection:** The latent trajectory and velocity graphs record clear, measurable shifts during major state transitions (e.g., accelerating from a stop or decelerating to a complete halt) without requiring fine-tuning. This confirms that the model abstracts high-level **situational context**.
* **Fine-Grained Limitations:** Out-of-the-box, the global representation prioritizes macro context over localized micro-details, making fine-grained events (such as sudden traffic light changes or subtle pedestrian appearances) harder to detect purely via unsupervised latent distance heuristics.

---

## 🛠️ Technical Stack

* **Model Checkpoint:** `vjepa_vitl16.pth` (ViT-L/16 backbone, 1024-D embedding space)
* **Datasets:** BDD100K, PIE (Pedestrian Intention Estimation) Dataset
* **Dimensionality Reduction:** PCA (`scikit-learn`)
* **Signal Processing:** Savitzky-Golay filtering for temporal smoothing
* **Visualization:** Matplotlib / OpenCV / IPython Display

---

## ⏩ Next Steps

While this pipeline validates the richness of the encoded representations, the ultimate goal of a world model is anticipation:
* **Phase 1 (Probing Heads):** Train lightweight downstream adapters/heads on top of frozen V-JEPA embeddings to capture fine-grained spatial and localized scene features.
* **Phase 2 (Latent Predictive Analysis):** Evaluate next-state prediction capabilities ($z \rightarrow \hat{s}_y$).
* **Phase 3 (Control Integration):** Integrate latent dynamics into downstream trajectory planning and autonomous driving control tasks.

---
*Developed as part of an R&D exploration into Self-Supervised World Models.*
