# TFM: Mapping Scientific Controversy in BiS2 Superconductors

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![Domain](https://img.shields.io/badge/Domain-Computational%20Linguistics%20%7C%20Condensed%20Matter%20Physics-blue)
![Python](https://img.shields.io/badge/Python-3.9%2B-green)

## 📖 Abstract

This Master’s Dissertation (TFM) explores the intersection of **Computational Linguistics** and **Materials Physics**. The project builds a Knowledge Graph (KG) to map the evolution of scientific consensus and controversy regarding the *$BiS_2$-based superconductor family* (2012–2025).

Unlike standard information extraction pipelines, this project focuses on **epistemic modality**: how authors use "hedging" (e.g., *"suggests,"* *"might indicate"*) to express uncertainty about the pairing mechanism (Phonon-mediated vs. Unconventional).

## 🎯 Objectives

1.  **Corpus Construction:** Curate a domain-specific corpus of arXiv papers excluding "false friends" (e.g., Topological Insulators like $Bi_2Se_3$).
2.  **Ontological Modeling:** Define a schema connecting *Materials*, *Techniques* (e.g., $\mu$SR, ARPES), and *Physical Properties* ($T_c$, Gap Symmetry).
3.  **Linguistic Analysis:** Detect and map rhetorical patterns of disagreement and uncertainty using NLP and LLM-assisted extraction.
4.  **Graph Analysis:** Use Neo4j to visualize how the "controversy" structure changes over time.

## 📂 Project Structure (Notebooks)

The technical pipeline is divided into 7 modular Jupyter Notebooks. The final extraction phase (Notebook 5) is split into three sub-notebooks due to computational constraints and the use of different LLMs for specific tasks.

### 1️⃣ `TFM_Notebook1_CorpusBuild_latest.ipynb`
* **Goal:** Corpus Construction from arXiv.
* **Method:** Queries the arXiv API using strict inclusion/exclusion logic to target the $BiS_2/BiCh_2$ family.
* **Output:** `corpus_metadata.csv` and initial dataset.

### 2️⃣ `TFM_Notebook2_PDFDownload.ipynb`
* **Goal:** PDF Download & Raw Text Extraction.
* **Method:** Iterates through the corpus metadata, downloads full-text PDFs, and extracts raw text for NLP tasks.
* **Output:** Raw text files from PDFs.

### 3️⃣ `TFM_Notebook3_TextExtractionAndEvaluation.ipynb`
* **Goal:** Text Preprocessing & Section Extraction.
* **Method:** Rule-based pipeline to clean text (ligature correction, de-hyphenation) and isolate specific sections (Abstracts, Conclusions). Includes evaluation against a Gold Standard.
* **Output:** Cleaned text segments.

### 4️⃣ `TFM_Notebook4_Normalization.ipynb`
* **Goal:** Text Normalization & Entity Standardization.
* **Method:** Standardizes chemical formulas and entities (e.g., unifying "LaO0.5F0.5BiS2" and "La(O,F)BiS2") to ensure consistency across the dataset.
* **Output:** Normalized text ready for extraction.

### 5️⃣ `TFM_Notebook5.1_ClaimExtraction_Gemma_2.5_9B-it.ipynb`
* **Goal:** Claim Extraction (Stage 1).
* **Method:** Uses **Gemma 2 (9B)** to extract epistemological claims and structured attributes from the scientific text.
* **Output:** Extracted claims with uncertainty markers.

### 6️⃣ `TFM-Notebook5.2_EntityExtraction_Qwen_3_8b.ipynb`
* **Goal:** Named Entity Recognition (NER).
* **Method:** Uses **Qwen 3 (8B)** to identify and categorize domain-specific entities (Materials, Methods, Properties) within the extracted claims.
* **Output:** Structured entities linked to claims.

### 7️⃣ `TFM_Notebook5.3_RelationsAndGraph.ipynb`
* **Goal:** Relation Extraction & Graph Construction.
* **Method:** Extracts semantic relationships between entities using LLMs and builds the final Knowledge Graph.
* **Output:** Final Knowledge Graph (nodes and edges).

## 🛠️ Installation & Usage

**Prerequisites:**
* Python 3.9+
* Neo4j Desktop (or AuraDB free tier)

**Setup:**
1.  Clone the repo:
    ```bash
    git clone [https://github.com/](https://github.com/)[YourUsername]/TFM_BiS2_Graph.git
    ```
2.  Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```
3.  Configure Environment:
    * Create a `.env` file for API keys (if using OpenAI/Anthropic for extraction).

## ⚠️ Data Constraints
* **Raw PDF Data:** Due to copyright restrictions, raw PDFs are not hosted in this repository.
* **Reproducibility:** The `01_Corpus_Acquisition` notebook allows anyone to reconstruct the dataset from public arXiv identifiers.

## 🎓 Academic Context
* **Author:**  Dario Santos
* **Program:** MA in Computational Linguistics
* **Institution:** La Rioja University
* **Year:** 2025-2026

---
*Disclaimer: This tool is for academic research purposes only.*
