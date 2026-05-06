# V-JEPA Latent Feature Extraction and Inference Pipeline

Author: Alejandro Meza Tudela

This repository implements a robust inference and visualization pipeline for **V-JEPA (Vision-Joint Embedding Predictive Architecture)** applied to the **BDD100K** autonomous driving dataset. By analyzing the model's high-dimensional latent space, we can interpret how a self-supervised "World Model" understands driving environments without human-labeled data.


## 🚀 Overview
This project focuses on extracting and visualizing the "internal thoughts" of the V-JEPA model. Instead of looking at raw pixels, we project the model's embeddings into interpretable manifolds to track semantic transitions and "surprise" during driving sequences.

## 📊 Analytical Visualizations
The dashboard provides three distinct views into the model's state:

*   **Latent Topology (Manifold Map):** A 2D PCA projection of the 1024-D feature space. Distance between points represents semantic similarity; clusters represent stable environmental states (e.g., highway cruising vs. intersection navigation).
*   **Latent Velocity (Semantic Surprise):** Calculated as the $L_2$ norm of the change between consecutive embeddings. Peaks in this "pulse" identify critical events—such as sudden braking or lane changes—where the model detects a significant shift in the situational context.
*   **Spatial Semantics:** A $14 \times 14$ grid revealing the model’s tokenized understanding. This unsupervised segmentation demonstrates how V-JEPA groups related visual objects (road, cars, sky) through temporal consistency.

### 🎥 V-JEPA Inference Dashboard Demo
<p align="center">
  <video src="https://github.com/jalex3421/vjepa-latent-dynamics-bdd100k/releases/download/v1.0.0-demo/VJEPA_Inference_Visualizer_demo.mp4
" width="100%" controls autoplay muted loop>
    Your browser does not support the video tag.
  </video>
  <br>
  <em>Real-time visualization of Latent Topology and Semantic Pulse on BDD100K sequences.</em>
</p>

## 🧠 Key Findings
Through this inference pipeline, we have verified that **V-JEPA’s latent state is highly sensitive to environmental dynamics**. 

A significant observation in our tests showed that the latent trajectory and velocity graphs recorded measurable shifts when the vehicle came to a complete stop. This confirms that the model is abstracting **situational context** rather than just performing pattern matching on pixels.

## 🛠️ Technical Stack
*   **Model:** V-JEPA (Vision-Joint Embedding Predictive Architecture)
*   **Dataset:** BDD100K (Berkeley DeepDrive)
*   **Dimensionality Reduction:** PCA (scikit-learn)
*   **Signal Processing:** Savitzky-Golay filtering for temporal smoothing
*   **Visualization:** Matplotlib / IPython Display

## ⏩ Next Steps
While this notebook validates the richness of the encoded representations, the ultimate goal of a world model is anticipation. 
*   **Phase 2:** Latent Predictive Analysis (Next-state prediction).
*   **Phase 3:** Integration with downstream control tasks.

---
*Developed as part of an R&D exploration into Self-Supervised World Models.*
