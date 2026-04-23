# Research---A Computational Pipeline to find SNP–miRNA Interactions in Neurodegenerative Diseases
A computational pipeline for identifying and prioritizing 3′UTR SNP–miRNA interactions in Alzheimer's, Parkinson's, and ALS using GWAS data, Ensembl BioMart, and weighted scoring.

---

## 📌 Overview

This project implements a multi-step bioinformatics pipeline that:

1. Retrieves genome-wide significant SNPs from the **NHGRI-EBI GWAS Catalog**
2. Maps SNPs to **3′UTR regions** using Ensembl BioMart (GRCh38)
3. Predicts **miRNA binding site gain/loss** using miRNASNP-v4, TargetScan, and miRmap
4. Applies **MAF filtering**, evolutionary conservation, and brain-expression criteria
5. Calculates a **weighted prioritization score** for each SNP–miRNA interaction
6. Generates visualizations and exports a curated candidate table
---

## ⚙️ Methodology

### Step 1 — Data Collection
- Uses **pandasGWAS** to query the GWAS Catalog for AD, PD, and ALS
- Filters genome-wide significant SNPs (p < 5×10⁻⁸)
- Removes duplicate rsIDs and saves combined dataset as CSV/Excel

### Step 2 — SNP Mapping & 3′UTR Selection
- Connects to **Ensembl BioMart (GRCh38)** via **pybiomart**
- Maps SNPs to genes and transcripts
- Filters only SNPs located in **3′UTR regions**
- Focuses on disease-relevant genes

### Step 3 — miRNA Binding Prediction
- Matches 3′UTR SNPs against **miRNASNP-v4** bulk data using pandas
- Predicts **gain or loss** of miRNA binding sites
- Uses **TargetScan + miRmap consensus** for top candidates

### Step 4 — Filtering, Prioritization & Scoring
Filters applied:
- Minor Allele Frequency (MAF > 0.01)
- Evolutionary conservation score
- Brain-expressed miRNAs (GTEx / miRBase)

**Weighted Prioritization Score:**
```
Score = (Conservation × 0.4) + (Binding Impact × 0.4) + (Brain Relevance × 0.2)
```

Optional: Pathway enrichment via **Enrichr API**

### Step 5 — Output & Visualization
**Output columns:** `rsID | Gene | miRNA | Predicted Effect | Score | Disease`

**Visualizations (matplotlib, seaborn, plotly):**
- Bar charts — number of candidates per disease
- Ranked tables and heatmaps of top SNP–miRNA pairs

---

## 🧪 Expected Outcomes

- Identification and prioritization of novel **SNP–miRNA interactions** predicted to alter miRNA binding efficiency and post-transcriptional gene regulation
- Generation of curated datasets and computational predictions for future **experimental validation**
- Improved understanding of **epigenetic and post-transcriptional regulatory mechanisms** in neurodegenerative diseases
- Reusable framework adaptable for other complex genetic disorders

---

