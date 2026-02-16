# Automated Information Extraction & Knowledge Graph Construction for -Based Superconductors

This repository contains the end-to-end pipeline for the automated extraction of scientific knowledge from unstructured physics literature. By leveraging Large Language Models (LLMs) and "Literate Programming" principles, this project transforms a corpus of  superconductor research into a structured, queryable **Domain Knowledge Graph (KG)**.

## 🔬 Project Overview

The "information fragmentation" in materials science prevents researchers from seeing the "big picture" across thousands of PDF publications. This project operationalizes the **Materials Science GPT** paradigm by:

1. **Curation:** Filtering the arXiv repository for high-fidelity  literature.
2. **Extraction:** Using open-weights LLMs (**Gemma 2.5 9B** & **Qwen 3 8B**) for Named Entity Recognition (NER) and Relation Extraction (RE).
3. **Synthesis:** Constructing a Directed Multigraph to visualize the research ecosystem and identify "hub" materials and hidden property correlations.

---

## 🏗️ Repository Structure

The project follows a "Separation of Concerns" architecture to ensure data provenance and computational reproducibility.

```text
TFM/                             
├── notebooks/                   # Sequential Jupyter notebooks (01–05.3)
├── code/                        # Supporting scripts and utility functions
├── data/
│   ├── raw/                     # Original PDF binaries
│   ├── processed/               # Intermediate processed datasets
│   ├── output/                  # Final analysis outputs
│   └── corpora/                 # Data snapshots at distinct processing stages
│       ├── 01_raw/              # Metadata and JSON snapshots
│       ├── 02_extracted/        # Text converted from PDFs
│       ├── 03_normalized/       # Cleaned and standardized text
│       └── 04_enriched/         # Ontology-aligned corpus with Claims/Entities
└── results/                     # Figures, tables, and visualization outputs

```

---

## ⚙️ The Computational Pipeline

The workflow is divided into four distinct phases, executed via sequential notebooks:

### Phase I: Data Acquisition

* **Notebook 01: Corpus Acquisition** | Implements an iterative query architecture (v3.0) via the arXiv API. Uses Boolean exclusions to filter noise (e.g., bismuthate compounds).
* **Notebook 02: Binary Retrieval** | Downloads full-text PDFs and uses **PyMuPDF** for layout-aware text extraction to preserve reading order.

### Phase II: Text Engineering

* **Notebook 03: Section Segmentation** | Isolates "Conclusion" and "Summary" sections using "Strict Mode" regex (v3.1) with lookahead assertions to prevent reference bleed.
* **Notebook 04: Scientific Normalization** | Uses a custom `ScientificTextNormalizer` to map PUA characters and standardize LaTeX formatting (e.g., converting `ho` to `ρ` and consistent  subscript handling).

### Phase III: Semantic Extraction (LLM Pipeline)

* **Notebook 5.1: Epistemological Claim Extraction** | Uses **Gemma 2.5 9B-IT** (4-bit) to classify assertions (Observation, Inference, Speculation) and resolve anaphora (replacing "it" with specific material formulas).
* **Notebook 5.2: NER** | Uses **Qwen 3 8B** to identify nodes based on a strict ontology: `Material`, `Property`, `Condition`, `Method`, and `Value`.

### Phase IV: Knowledge Synthesis

* **Notebook 5.3: Relation Extraction & Graph Assembly** | Extracts Subject-Predicate-Object triplets. Performs entity fuzzy matching for canonicalization and executes **Louvain Clustering** for community detection.

---

## 🛠️ Tech Stack & Methodology

* **Language:** Python
* **NLP/Graphing:** NetworkX, PyVis, PyMuPDF (fitz)
* **LLM Frameworks:** Hugging Face Transformers, `bitsandbytes` (4-bit quantization)
* **Hardware:** Optimized for consumer-grade GPUs (e.g., NVIDIA T4 / 16GB VRAM)
* **Key Concepts:** * **Literate Programming:** Notebooks serve as verifiable technical appendices.
* **Prompt Engineering:** Chain-of-Thought (CoT) and "Materials Scientist" persona patterns. Hard constraints into formatted output to prevent hallucination and malformed inferences.



---

## 📊 Key Outcomes

* **Final Corpus:** 122 verified, high-confidence papers.
* **Graph Density:** 2,035 unique entities and 5,743 relational edges.
* **Topological Insights:** Identified 51 distinct scientific sub-communities. Confirmed  as the primary central "hub" node.
* **Performance:** "Strict Mode" extraction reduced boundary failures and noise by **90%** compared to baseline regex methods.

---

## 🚀 Future Work

* **Syntactic Normalization:** Pre-processing Stage I to rewrite complex sentences into atomic SVO structures.
* **Vision Integration:** Implementing vision-based models to extract synthesis parameters from tables and figures.
* **Scaling:** Migrating to multi-GPU inference for larger-scale physics corpora.

---


## 🤝 Citation

If you use this dataset, pipeline, or methodology in your research, please cite:

> **Santos Prego, Dario**. (2026). *Automated Knowledge Graph Construction for BiS₂-based Layered Superconductors*. Master's Thesis.

---

*Maintained by [DariSant*](https://www.google.com/search?q=https://github.com/DariSant)