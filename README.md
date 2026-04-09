# Contextual Compression Engine for Extreme Long Inputs

## Video Demonstration and Explanation link : https://youtu.be/9zGykLd-n0Y

## IMPORTANT : 
- Because of CPU and GPU limitations, we have run the full_source_code.ipynb on Google collab so the paths are according to the collab format. To run on VS code, the paths need to be changed (The "/content" needs to be removed from every file's path)

- app.py is ready to be run directly on VS code

## Overview

Enterprises work with very large documents such as policy manuals, legal texts, audit reports, technical runbooks, and long logs. These documents often span hundreds or thousands of pages.

Most AI systems and humans cannot process such documents at once due to context window limitations. Traditional summarization approaches reduce size but lose important details, hide exceptions and risks, and remove traceability.

This project implements a **Contextual Compression Engine** that compresses large documents step by step while preserving decision-critical information and full traceability. The goal is to produce compressed content that can still be trusted for decision-making.

---

## Key Features

- Hierarchical compression (paragraph → section → chapter → executive summary)
- Preservation of decision-critical information:
  - Numbers and thresholds
  - Dates and deadlines
  - Exceptions and constraints
  - Risks
- Full traceability from compressed output to original text
- Drill-down support from summary to original paragraph
- Detection of potential contradictions
- Explainability and information-loss reporting
- Structured JSON outputs for reuse

---

## Why This Approach

Most systems use one-shot summarization, which causes information loss and reduces trust.

This system:
- Compresses content level by level
- Preserves document structure
- Explicitly extracts critical information
- Maintains source references at every stage

The result is compact but trustworthy compressed output.

---

## System Architecture

### Main Components

- **Document Loader**  
  Loads large PDF documents and extracts text with page and character metadata.

- **Hierarchical Chunker**  
  Splits the document into paragraphs, sections, and chapters.

- **Critical Content Extractor**  
  Extracts decision-critical items such as numbers, exceptions, and risks.

- **Hierarchical Compressor**  
  Uses an LLM to compress content step by step while preserving critical information.

- **Contradiction Detector**  
  Uses semantic similarity to flag potentially conflicting statements.

- **Traceability Manager**  
  Maintains links between compressed content and original sources.

- **Explainability Engine**  
  Generates compression statistics and information-loss metrics.

- **Streamlit UI**  
  Provides a simple interface for summaries, drill-down, and traceability inspection.

---

## Input

- A large PDF document  
- A configuration file defining chunk sizes and extraction rules  

The current implementation supports a single document but can be extended to multiple documents.

---

## Output

The system produces:

- Multi-level compressed summaries
- Key facts, exceptions, and risks list
- Structured JSON outputs
- Traceability links for every compressed statement
- Contradiction reports
- Explainability and compression statistics

All outputs are stored in a structured folder for reuse.

---
## Repository Structure

```text
autonomous/
├── app.py
├── config.yaml
├── requirements.txt
├── data/
│   ├── compressed.json
│   ├── critical_items.json
│   ├── contradictions.json
│   ├── traceability.json
│   ├── explainability_report.json
│   ├── chunks.json
│   └── document_metadata.json
└── src/
    ├── document_loader.py
    ├── chunker.py
    ├── extractor.py
    ├── compressor.py
    ├── contradiction.py
    ├── traceability.py
    └── explainability.py
```


---

## Requirements

- To run this project, the following are required:

### Software Requirements

- Python 3.9 or higher
- Ollama installed locally
- A supported Ollama model (for example: `llama3`)
- Internet access for initial model download

### Python Dependencies
All dependencies are listed in `requirements.txt`, including:
- streamlit
- ollama
- pyyaml
- pdfplumber
- PyPDF2
- sentence-transformers
- scikit-learn
- numpy

---

## Setup and Running the Project

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

- Ensure that Ollama is installed and running on your system.

2. Start the Application
```bash
streamlit run app.py
```

## 📘 Using the Application

The Streamlit interface provides the following views:

### 🧭 Executive Summary
- Highest-level compressed view of the document.

### 📑 Chapter and Section Summaries
- Hierarchical summaries with drill-down support.

### 🔎 Paragraph Drill-Down
- Side-by-side view of compressed and original text.

### ⚠️ Key Facts / Exceptions / Risks
- Explicit list of decision-critical information with source references.

### 🔁 Contradictions
- Potential conflicts detected using semantic similarity.

### 📊 Explainability Report
- Compression statistics and information-loss metrics.

### 🗂️ Raw Structured Output
- JSON outputs for programmatic use.

### Explainability and Trust

The system provides:

- Original and compressed character counts

- Compression ratios

- Reduction percentage

- Full source references

This allows users to understand:
- What was kept

- What was removed

- Why the compressed output can be trusted

- Known Issues and Future Updates

### Some sections may contain minor logical or UI inconsistencies.

### Certain edge cases in section-to-chapter linking may require refinement.

### Error handling for malformed or complex PDFs can be improved.

### These issues are known, and the codebase will be updated in future iterations to address them.

### Limitations

- This project does not aim to:

- Train new language models

- Handle millions of documents

- Provide a complex enterprise-grade UI

- The focus is on structure, traceability, and decision-preserving compression.

### Evaluation Alignment

- This project aligns with the Track-4 evaluation criteria:

- Clear hierarchical compression strategy

- Strong traceability and evidence support

- Handling of exceptions and contradictions

- Practical and scalable design

### Conclusion

This project demonstrates that large documents can be compressed without losing trust.
By combining hierarchical compression, explicit preservation of critical information, and full traceability, the system produces compact representations that remain usable for enterprise decision-making.

---
## 👥 Team

This project was developed collaboratively by:

- **Mayank Lande**
- **Ankit Kumar**
- **Mangesh Rakhewar**
- **Aayush Raj**
