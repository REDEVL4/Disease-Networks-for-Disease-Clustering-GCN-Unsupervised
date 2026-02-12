# 🧬 Disease Networks for Disease Clustering  
(Graph Convolutional Networks – Unsupervised)

**University of Houston–Clear Lake | Jul 2025 – Dec 2025**

An unsupervised disease clustering pipeline that integrates a disease–gene network with Gene Ontology (Biological Process) annotations using a Graph Convolutional Network (GCN) encoder to generate semantically meaningful disease embeddings.

This project demonstrates how combining **graph structure + functional annotations** improves disease clustering quality over raw feature-based methods.

---

## 🎯 Project Objective

To cluster diseases by integrating:

- Disease–gene network (shared gene relationships)
- Gene Ontology (Biological Process) annotations
- Graph Convolutional Networks (GCN)

The goal is to generate **disease embeddings** that capture:

- Functional similarity (GO biological processes)
- Network similarity (shared genes)
- Ontological semantic relationships

---

## 🧠 Why Disease Clustering?

Disease clustering helps:

- Reveal hidden biomedical relationships
- Support drug repurposing
- Improve comorbidity prediction
- Understand shared molecular mechanisms

---

## 📊 Data Sources

1. **Disease–Gene Incidence Matrix**
   - Binary matrix (disease × gene)

2. **Gene Ontology (GOA – Biological Process)**
   - Gene → GO BP annotations

3. **Disease Ontology (DO)**
   - Used for semantic shortest-path validation

4. OMIM / DisGeNET
   - Used for disease–gene relationships

---
Disease × Gene Matrix
↓
Map Genes → GO Biological Process Terms
↓
Disease × GO Binary Feature Matrix
↓
Construct Disease Graph (shared genes)
↓
3-Layer GCN Encoder (PyTorch)
↓
Disease Embeddings (Z)
↓
KMeans Clustering
↓
Validation via Disease Ontology Shortest Path

---

## 🧮 Graph Construction

- Nodes: Diseases
- Edges: Shared associated genes
- Adjacency Matrix A ∈ R^(N×N)
- Feature Matrix X ∈ R^(N×d)

Edge exists if two diseases share ≥1 gene.

---

## 🧠 Model Architecture

### 3-Layer Graph Convolutional Network

Layer-wise propagation rule:

H(l) = σ( D̃^(-1/2) Ã D̃^(-1/2) H(l-1) W(l) )

Where:
- Ã = A + I (self-loops)
- D̃ = degree matrix
- ReLU activation
- Final layer produces disease embeddings

Architecture:
Input Features (GO matrix)
↓
GCN Layer 1
↓
GCN Layer 2
↓
Linear Projection
↓
Embeddings (Z)

---

## 🔬 Experimental Setup

Three datasets:

| Dataset | Diseases | BP Features | Embedding Dim |
|----------|----------|------------|---------------|
| D1a40 | 40 | 220 | 60 |
| D2a50 | 50 | 220 | 70 |
| D3a60 | 60 | 220 | 75 |

Clustering performed with:
- k = 2 (KMeans)

---

## 📈 Baseline vs GCN Embedding Clustering

We compared:

1. Clustering on raw GO features
2. Clustering on GCN embeddings

### Validation Method

Used **Disease Ontology (DO) shortest-path distance**:

- Intra-cluster distance → should be small
- Inter-cluster distance → should be larger
- Larger (inter − intra) difference = better clustering

---

## 📊 Results

### Difference (Inter − Intra DO Distance)

| Dataset | Raw GO Features | GCN Embeddings |
|----------|------------------|----------------|
| D1a40 | 0.90 | **1.45** |
| D2a50 | 0.85 | **1.25** |
| D3a60 | 1.10 | **1.85** |

### 🔥 Improvement

Clear improvement in cluster separation using GCN embeddings:

- 0.90 → 1.45
- 0.85 → 1.25
- 1.10 → 1.85

GCN embeddings produced **more semantically coherent clusters**.

---

## 🛠 Tech Stack

- Python
- PyTorch
- NumPy / Pandas
- scikit-learn (KMeans, Silhouette)
- NetworkX
- Disease Ontology (DO OBO file)
- Gene Ontology (GOA)

---

## 📂 Repository Structure

├── data/
│ ├── disease.csv
│ ├── gene.csv
│ ├── mat_disease_gene.csv
│ ├── HumanDO.obo
│ ├── goa_human_combined_filtered.csv
│
├── notebooks/
│ └── GCN_project_Disease_Clustering.ipynb
│
└── README.md
## 🏗️ Pipeline Overview

---

## 📌 Key Contributions

- Integrated network structure + GO annotations
- Built disease×GO binary feature matrix
- Implemented 3-layer GCN encoder in PyTorch
- Compared raw vs embedding clustering
- Validated with Disease Ontology shortest-path metric
- Demonstrated improved semantic cluster quality

---

## 🔍 Insights

- Pure feature clustering (GO only) yields weaker separation
- GCN effectively aggregates:
  - Local neighborhood structure
  - Functional annotations
- Ontology-based validation confirms improved biological relevance

---

## 🚀 Future Work

- Expand dataset to larger disease sets
- Try spectral clustering / DBSCAN
- Incorporate phenotype or symptom data
- Use contrastive learning on graphs
- Apply to drug repurposing pipelines

---

## 👨‍💻 Authors

Govardhan Reddy Narala  
University of Houston–Clear Lake  

---


