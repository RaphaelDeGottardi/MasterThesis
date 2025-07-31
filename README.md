# 🧬 Master Thesis: Bin2Cell Methods for Spatial Transcriptomics

> **Evaluation of Bin2Cell methods for Spatial Transcriptomics**

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-orange.svg)](https://jupyter.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📖 Overview

This repository contains comprehensive analysis tools and benchmarking pipelines for evaluating bin-to-cell assignment methods in spatial transcriptomics. All code is implemented in Python using Jupyter notebooks, providing reproducible research workflows for extending and validating thesis results.

---

## 🚀 Quick Start

### Prerequisites

You'll need a conda or Python environment to run the code. Choose one of the following options:

#### Option 1: Create from Environment Files
You can find the yml files in the ./Environments folder. the environment required to run a notebook can be found in the first few (markdown) cells of each jupyter notebook.
```bash
# Navigate to the environments folder
cd ./Environments

# Create environment from YAML file
conda env create -f environment.yml
conda activate your-environment-name
```

#### Option 2: Manual Installation
Create your own environment and install packages as needed. Required packages are can be deducted form the inports the first few cells of the notebooks.

---

## 📊 Repository Structure

### 🔬 Benchmarking Pipeline
Comprehensive evaluation metrics and analysis tools organized by thesis chapters:
- **General Metrics**
  - VpX performance metrics
  
- **Segmentation Metrics**
  - VpX segmentation evaluation

- **Cell Type Assignment Metrics**
  - Azimuth analysis notebooks
  - Celltypist evaluation
  - Classical annotation methods
  
- **Scoring Methods**
  - MECR (Mutual Exclusivity Cell Recognition)
  - Spurious coexpression analysis


### 📈 Analysis Workflows

| 📁 Folder | 🎯 Purpose | 🔍 Key Files |
|-----------|------------|--------------|
| `Sushi outputs/` | Post-processing [Sushi](https://fgcz-sushi.uzh.ch/) bin-to-cell results | Analysis notebooks for Bin2Cell & ENACT Apps|
| `Benchmarking pipeline/` | Thesis plots and metrics | Look for `*_plots.ipynb` files (summary metrics) or find the method specific results in corresponding notebooks.|
| `Xenium Segmentation Transfer/` | Visium HD data processing | Protocol and coordinate conversion tools. Contains own README.md |

---

## 📁 Data Sources

### 🌐 Public Datasets
- **Source**: [10X Genomics Datasets](https://www.10xgenomics.com/resources/datasets)
- **Format**: Publicly available spatial transcriptomics data
- **Sushi**: Input and output files can be found in Project 37785. Please contact [FGCZ](https://fgcz.ch/) Genome Informatics for access.

## 🎯 Use Cases

### 📊 Analyzing Sushi Results
If you've successfully run Sushi bin-to-cell applications:

1. Navigate to `📁 Sushi outputs/`
2. Open the relevant notebook:
   - `Bin2Cell_outputs.ipynb` - For Bin2Cell results
   - `ENACT_outputs.ipynb` - For ENACT results
3. Follow the guided analysis to generate key plots and insights
4. Checking the segmentation outputs is strongly recommended. Adapte the parameters if you are not satisfied with teh results. More information an parameter tuning can be found in the tesis appendix.

### 📈 Reproducing Thesis Plots
All figures from the thesis can be reproduced and are containes in this repo:

1. Browse `📁 Benchmarking pipeline/`
2. Look for notebooks ending with `*_plots.ipynb`
3. Dataset-specific analyses are organized by method and data type
4. Folder structure mirrors thesis chapter organization

### 🔬 Processing Visium HD with Xenium Data
For Visium post-Xenium spatial data:

1. Start with `📁 Xenium Segmentation Transfer/PROTOCOL.md`
2. Follow the coordinate conversion workflow
3. Use provided transformation and reformatting tools
4. **Required**: Install Xenium Explorer for manual image alignment

---

## 📝 Notes

- Each notebook contains environment requirements in its first few cells
- Use the specified environments to ensure reproducible results
- All analysis code is designed for extensibility and modification.

---

## 📞 Support

For questions about data access or technical issues, please contact:
- **Data Access**: [FGCZ](https://fgcz.ch/)
- **Code Issues**: Open an issue in this repository

---

*Happy analyzing! 🧪✨*