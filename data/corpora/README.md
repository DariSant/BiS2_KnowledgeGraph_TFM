# Corpora Directory

This directory contains all corpus-related resources used in the Master's Thesis (TFM).
The corpora are organized following a reproducible NLP processing pipeline.

## Directory Structure

### 01_raw
Original, unprocessed documents collected from scientific sources.
Examples:
- PDF files
- Publisher exports
- Original text files

### 02_extracted
Text extracted from raw documents using automated pipelines.
Examples:
- PDF to TXT conversions
- XML or JSON extractions

### 03_normalized
Linguistically normalized versions of the extracted texts.
Typical operations include:
- LaTeX and mathematical symbol normalization
- Unicode normalization
- Lowercasing (when applicable)
- Removal or standardization of noise

### 04_enriched
Structurally enriched and semantically annotated corpus.
Examples:
- Ontology-aligned JSON files
- Named entity annotations
- Metadata-enhanced documents

## Notes
- Each directory represents a distinct processing stage.
- Files should not be manually edited once generated.
- All transformations are documented and reproducible via notebooks.