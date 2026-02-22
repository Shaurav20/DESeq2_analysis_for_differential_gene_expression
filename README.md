# **DESeq2 Differential Gene Expression Analysis (Dexamethasone Treatment Study)**

## **Overview**

This project implements a reproducible RNA-seq differential gene expression (DGE) analysis pipeline using DESeq2 in R.
The analysis evaluates transcriptional changes induced by dexamethasone treatment, starting from raw read counts and ending with statistically validated results and publication-ready visualizations.

**The workflow prioritizes:**

- Statistical rigor
- Biological interpretability  
- Reproducibility
- Clear documentation of challenges and solutions

## **Project Structure**
```
├── analysis_script.R        # Complete DESeq2 analysis & visualization pipeline
├── counts_data.csv          # Raw gene count matrix
├── sample_info.csv          # Sample metadata
├── results/
│   ├── figures/             # PCA, heatmaps, MA plot, volcano plot
│   ├── tables/              # DESeq2 result tables (CSV)
│   └── logs/                # Session info & summaries
├── README.md                # Project documentation
└── LICENSE                  # MIT License
```

## **Installation**

### **System Requirements**
- R ≥ 4.0
- RStudio (recommended)

### **Required R Packages**

install.packages(c("tidyverse", "ggplot2", "pheatmap", "RColorBrewer", "ashr"))

if (!require("BiocManager", quietly = TRUE))
  install.packages("BiocManager")

BiocManager::install(c(
  "DESeq2",
  "AnnotationDbi",
  "org.Hs.eg.db",
  "DEGreport"
))

## **Usage**

### **1. Place input files in the project directory:**

counts_data.csv

sample_info.csv

### **2. Set working directory:**

setwd("path/to/project")

### **3. Run the analysis:**

source("analysis_script.R")
Outputs will be automatically saved in the results/ directory.

## **Methodology**

### **Data Validation**

Matching samples between counts and metadata

Column reordering if necessary

### **DESeq2 Workflow**

DESeqDataSet construction

Library size and dispersion estimation

Differential expression testing

### **Filtering & Normalization**

Low-count gene filtering

Variance Stabilizing Transformation (VST)

### **Visualization**

PCA

Sample distance heatmap

MA plot

Volcano plot

Heatmap of top 50 DEGs

### **Gene Annotation**

Ensembl ID → Gene symbol mapping (human)

## **Results**

### **Generated Outputs**

**Figures (PNG):**

PCA plot

Sample distance heatmap

MA plot

Volcano plot

Heatmap of top 50 differentially expressed genes

**Tables (CSV):**

Complete DESeq2 results

Significant DE genes

Annotated DE results

Normalized expression matrix

**Logs:**

R session information

Analysis summaries

All outputs are stored in the results/ directory.

## **Problems and Solutions**

### **Problem 1: Noisy differential expression results**

Low-count genes caused unstable fold changes and weak clustering.

**Solution**

Applied gene filtering
keep <- rowSums(counts(dds) >= 10) >= 3

Used VST normalization  
vsd <- vst(dds, blind = FALSE)

**Outcome:** 
Cleaner PCA separation and more biologically meaningful DE genes.

### **Problem 2: Blank heatmap image files**

The heatmaps were saved as empty PNG files.

Root Cause: pheatmap() uses grid graphics, which require explicit rendering.

**Solution**

grid::grid.newpage()

**Outcome:** 
Heatmaps rendered correctly and reproducibly.

## **References**

Love MI, Huber W, Anders S. Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2. Genome Biology, 2014.

R Core Team (2024). R: A language and environment for statistical computing. https://www.r-project.org/

Bioconductor Project. https://bioconductor.org/

## **License**

This project is licensed under the MIT License. You are free to use, modify, and distribute this code with appropriate attribution.

## **Author**
Shaurav Bhattacharyya

- GitHub: @Shaurav20 (https://github.com/Shaurav20)
- LinkedIn: Shaurav Bhattacharyya (https://www.linkedin.com/in/shaurav-bhattacharyya-a347b5156/)
- Email: shaurav.feb@gmail.com

## **Acknowledgements**

DESeq2 - Love, Huber, Anders (2014)

R/Bioconductor - Open-source community

Gene Ontology & Ensembl - Annotation resources

