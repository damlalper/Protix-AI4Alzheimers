# Protix

**Protix** is an advanced AI-driven platform for **protein modeling** and **drug discovery** targeting **Alzheimer’s Disease**. The platform combines deep learning, graph neural networks, and molecular simulation to predict protein folding, understand amyloid-beta aggregation, and propose potential therapeutic compounds.

---

## 🧬 Project Motivation

Alzheimer’s Disease (AD) is a neurodegenerative disorder with complex pathophysiology and limited treatment options. Early detection and targeted drug development are critical. **Protix** aims to:

1. Predict the 3D structure of AD-related proteins (Amyloid-beta, Tau) using AI-based protein modeling.
2. Simulate protein-ligand interactions to identify promising drug candidates.
3. Provide **explainable AI insights** to guide biomedical research and hypothesis generation.

By integrating multiple computational approaches, **Protix** provides a research-grade tool that could accelerate therapeutic discovery.

---

## 🔬 Key Features

- **Protein Structure Prediction:**  
  - Implements AlphaFold2-inspired deep learning architectures for high-accuracy folding predictions.
  - Supports multiple conformational states of AD-related proteins.
  
- **Drug Discovery Pipeline:**  
  - Virtual screening of small molecules from DrugBank and custom ligand libraries.
  - ML-based binding affinity scoring using graph neural networks.
  - Identification of novel compounds with potential amyloid-beta aggregation inhibition.
  
- **Graph Neural Networks (GNN):**  
  - Models protein-ligand interactions as graphs.
  - Provides node-level and edge-level interpretability to highlight critical residues and interactions.
  
- **Explainable AI:**  
  - Uses SHAP and LIME to interpret model decisions.
  - Generates heatmaps of influential residues in protein-ligand binding.
  
- **Multimodal Data Integration:**  
  - Combines structural (PDB), sequence (UniProt), and biochemical assay data.
  - Enables holistic analysis of protein behavior and ligand efficacy.

---

## 🛠️ Tech Stack

| Layer | Technologies & Approach |
|-------|------------------------|
| **Programming** | Python 3.12, TypeScript (frontend interactivity) |
| **Deep Learning / AI** | PyTorch, PyTorch Lightning, HuggingFace Transformers |
| **Graph Modeling** | PyTorch Geometric (PyG) for protein-ligand interactions |
| **Protein & Molecular Tools** | Biopython, RDKit, OpenMM, PyRosetta |
| **Backend** | FastAPI (model serving & API endpoints), Dockerized pipelines, REST + WebSocket for real-time updates |
| **Frontend** | React.js, Plotly Dash / Three.js for 3D protein visualization, responsive design, dynamic dashboards |
| **Data Integration / Multi-Modal** | Protein sequences (UniProt), 3D structures (PDB), Ligand / drug databases (DrugBank, ChEMBL), Clinical / MRI metadata (ADNI), Optional: Speech/text biomarkers (DementiaBank) |
| **Visualization / Dashboard** | Plotly, Matplotlib, Seaborn, PyMol, 3D interactive dashboards for protein-ligand & multimodal data |
| **Model Deployment / Serving** | FastAPI endpoints, Docker, GPU-enabled inference, Jupyter/Colab integration |
| **Reproducibility / CI-CD** | Conda environments, requirements.txt, GitHub Actions, versioned model checkpoints |
| **Explainable AI (XAI)** | SHAP, LIME, Grad-CAM for protein-ligand and multimodal interpretability |


---

## 📈 Project Pipeline

1. **Data Acquisition & Preprocessing:**  
   - Protein sequences & 3D structures retrieved from UniProt and PDB.  
   - Ligand datasets from DrugBank and ChEMBL.  
   - Normalization, featurization, and graph construction.

2. **Protein Modeling:**  
   - Predict folding and 3D structures with AlphaFold-inspired CNN + Transformer hybrid models.  
   - Validate predicted structures against known crystal structures using RMSD metrics.

3. **Ligand Docking & Screening:**  
   - Molecular docking simulations via OpenMM and RDKit.  
   - GNN models evaluate binding affinity and predict inhibitory potential.

4. **Explainable AI Analysis:**  
   - Use SHAP/LIME to highlight critical residues or ligand features.  
   - Generate interpretable reports for research insights.

5. **Results Visualization:**  
   - 3D protein-ligand interaction maps using PyMol.  
   - Heatmaps of key residues contributing to drug efficacy.  
   - Performance metrics for predictive models (MAE, RMSE, R², ROC-AUC).

---

## 📂 Repository Structure

Protix/
├── data/ # Raw and processed datasets
├── frontend/ # Visualization of predictions
├── backend/ # FASTAPI endpoints
├── notebooks/ # Jupyter notebooks for experiments
├── src/ # Source code (preprocessing, training, evaluation)
├── models/ # Saved model weights
├── results/ # Visualizations, metrics, reports
├── Dockerfile # Optional containerized environment
├── requirements.txt # Dependencies
└── README.md # This document


---

## 🎯 Impact & Vision

**Protix** is designed to bridge **AI research and biomedical applications**:

- Accelerates discovery of **potential therapeutics** for Alzheimer’s.  
- Provides **interpretable AI models** to support research transparency.  
- Can be extended to other neurodegenerative diseases or drug targets.  

With this project, we aim to demonstrate how **state-of-the-art AI techniques** can be leveraged in **computational biology**, providing a showcase-ready portfolio project for both hackathons and CVs.

---

## 📚 References & Resources

- [AlphaFold Paper](https://www.nature.com/articles/s41586-021-03819-2)  
- [PyTorch Geometric Documentation](https://pytorch-geometric.readthedocs.io/)  
- [RDKit Documentation](https://www.rdkit.org/docs/)  
- [ADNI Dataset](http://adni.loni.usc.edu/)  
- [DrugBank](https://www.drugbank.ca/)  
- [UniProt](https://www.uniprot.org/)  

---
