<img width="468" height="194" alt="image" src="https://github.com/user-attachments/assets/f9c32fb1-2f59-4cd2-a0d1-c09af776d81c" /># E0095-P02: Dalla Pozza - Paediatric ALL E0200-P12 analysis
[![Python](https://img.shields.io/badge/Python-3.13%2B-blue.svg)](https://www.python.org/downloads/)
[![R](https://img.shields.io/badge/R-4.5.1%2B-blue.svg)](https://www.r-project.org/)
[![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

Short description: code and notebooks to reproduce results for **E0200-P12** which combines the cohorts from **E0095 (The Sydney Children's Hospitals Network, CHW)**, **E0157 (The Royal Children's Hospital, RCH)**, and published data from
**[*Lorentzian et al. Nat Commun (2023)*](https://doi.org/10.1038/s41467-023-42701-9) (British Columbia Children's Hospital, BCCH)**. It also includes the **Conference figures (ANZCHOG & ASH)** and **Manuscript figures**.

---
## Table of contents
- [Overview](#overview)
- [Data access](#data-access)
- [Tech stack](#tech-stack)
- [Getting started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Quick start](#quick-start)
- [Configuration](#configuration)
- [Project structure](#project-structure)
- [Reproducibility](#reproducibility)
- [Outputs](#outputs)
- [Troubleshooting / FAQ](#troubleshooting--faq)
- [Contributing](#contributing)
- [Security & governance](#security--governance)
- [License](#license)
- [Contacts](#contacts)

<a id="overview"></a>
## Overview

- **Translational Relevance:**
  Pediatric B-cell precursor acute lymphoblastic leukemia (BCP-ALL) has an overall survival of greater than 90% with contemporary risk-adapted treatment protocols, but approximately 10-20% of patients will still relapse. Identifying a robust biomarker predictive of relapse at diagnosis could improve current risk stratification, as existing clinical, genomic and response-based approaches do not fully capture relapse-prone patients. The translational value of this approach lies in its potential to guide more precise treatment allocation from the outset. Earlier identification of patients at higher risk of relapse could support timely treatment intensification, while better recognition of patients at lower risk could help avoid unnecessary treatment burden and long-term toxicity. Proteomics provides a measure of protein expression that reflects cellular phenotypes, enabling the study of upregulated and downregulated pathways involved in relapse biology and potentially leading to the development of targeted agents to improve treatment strategies.
  
- **Translational Relevance:**
  **Introduction:**
  Improved risk stratification methods are needed for pediatric B-cell precursor acute lymphoblastic leukemia (BCP-ALL) to optimize therapy and reduce late effects. Current methods of predicting relapse are informed by clinical factors, cytogenetics, molecular assessments, and treatment response. Proteomic data may add biological information not captured by these methods.
  **Methods:**
  BCP-ALL samples from two Australian biobanks (117 patients) were analyzed via data-independent acquisition mass spectrometry (DIA-MS). Publicly available DIA-MS data from an external Canadian cohort (24 patients) underwent similar preprocessing and was harmonized with the Australian cohort. An ensemble machine learning model was developed from three base models to select relapse biomarkers. Validation of the model was conducted using a three-iteration approach, with each round designating one ALL cohort as the training dataset and the remaining two cohorts as external validation datasets.
  **Results:**
  A 13-protein signature was derived that distinguished patients at diagnosis with a high risk of relapse from those at low risk, as determined by permutation testing of class separation (p < 0.05). Pathway analysis comparing high- and low-risk-of-relapse samples implicated RNA processing, mRNA metabolism, and mitochondrial pathways. The signature, in combination with clinical factors (age, sex, cytogenetics, white cell count and measurable residual disease), also improved contemporary risk stratification methods using Cox proportional hazards modeling.
  **Conclusion:**
  In this retrospective multi-cohort analysis, the 13-protein prognostic signature distinguished patients who subsequently relapsed from those who remained in remission. Integration with clinical factors improved contemporary risk stratification. Prospective validation is required to determine its clinical utility for informing risk-adapted therapies. 

- **Inputs:**
    * Frozen peptide matrix `E0200-P12_FrozenPeptideMatrix.tsv`
    * Frozen protein matrix `E0200-P12_FrozenProteinMatrix.tsv`
    * Batch effect corrected working protein matrix `WorkingMatrix_CHW_RCH_BCCH_Combat_WithAdditionalAdjustment_20250531.tsv`
    * Histological/Clinical data: `MetaData_Extracted_CHW_RCH_BCCH_20250516.csv`
- **Outputs:** Results in `.csv` `.pickle` `.json` and figures in `.png` .
- **Status:** <br>
    **WIP: CDS Analysis**<br>
    **Conference Done for AZCHOG**<br>
    **Conference Preparation for ASH**

<a id="data-access"></a>
## Data access
Internal CMRI/ProCan shares (no PHI/PII in repo):<br>
[![Microsoft SharePoint ](https://img.shields.io/badge/Microsoft_SharePoint-0078D4?style=for-the-badge&logo=microsoft-sharepoint&logoColor=white)](https://cmrisydney.sharepoint.com/sites/ProCanOperationsManagement/Shared%20Documents/Forms/AllItems.aspx?id=%2Fsites%2FProCanOperationsManagement%2FShared%20Documents%2F03%20ProCan%2FProjects%20%2D%20Sample%20cohort%20analysis%20and%20associated%20methods%2FE0200%2DP12%5FCombined%20DIA%2DNN%20for%20Bone%20Marrow%20Comparisions&view=0)<br>
**BCCH data** from Nature communication: https://www.nature.com/articles/s41467-023-42701-9

<a id="tech-stack"></a>
## Tech stack
- **Language/runtime:** Python **3.13**, R **4.5.1**
- **Notebooks:** Jupyter
- **Core data & I/O:** `polars==1.34.0`, `pyarrow==21.0.0`, `openpyxl==3.1.5`, `tqdm==4.67.1`
- **Analysis / ML / Stats:** `scikit-learn==1.7.2`, `statsmodels==0.14.5`, `lifelines==0.30.0`, `networkx==3.5`
- **Visualisation & plotting:** `matplotlib==3.10.7`, `seaborn==0.13.2`, `matplotlib-venn==1.1.2`, `adjustText==1.3.0`
- **Python–R interop:** `rpy2==3.6.4`
- **Environment & tooling:** `pip` + `venv` (or conda), Bitbucket
- **OS targets:** macOS / Linux / WSL


<a id="getting-started"></a>
## Getting started
This repo builds **downstream analysis for cohort E0200-P12**. You’ll need Python 3.13 and R 4.5.1 as well as `rpy2`, access to the internal data shares, and the packages pinned in `requirements.txt`.

<a id="prerequisites"></a>
### Prerequisites
- **OS:** macOS / Linux / WSL with `git`
- **Python:** 3.13 (recommended)
- **R**: 4.5.1 (recommended)
- **Access:** Read access to E0200-P12 processed data and metadata shares

<a id="installation"></a>
### Installation
bash
```bash
# 1) Clone
git clone git@bitbucket.org:cmriprocan/repo_e0200-p12_all.git
cd repo_e0200-p12_all

# 2) Create & activate a virtual env (choose one)
# (A) venv + pip
python3.13 -m venv .venv
source .venv/bin/activate

# 3) Upgrade pip tooling
pip install -U pip wheel

# 4) Install pinned dependencies
pip install -r requirements.txt
```
python
```python
# Optional: verify key package versions match requirements.txt
import importlib, pkgutil

pkgs = [
    "polars", "pyarrow", "tqdm", "openpyxl",
    "matplotlib", "seaborn", "matplotlib_venn", "statsmodels",
    "rpy2", "sklearn", "lifelines", "networkx", "adjustText"
]

for name in pkgs:
    # handle import name differences
    mod_name = {"matplotlib_venn": "matplotlib_venn",
                "sklearn": "sklearn",
                "adjustText": "adjustText"}.get(name, name)
    found = pkgutil.find_loader(mod_name) is not None
    if not found:
        print(f"{name}: NOT INSTALLED")
        continue
    m = importlib.import_module(mod_name)
    v = getattr(m, "__version__", "unknown")
    print(f"{name}: {v}")
```
<a id="quick-start"></a>
### Quick start
Run `CAPs_analysis.ipynb` for **cancer associated proteins (CAPs) analysis**.<br>
Run `DEA_plot.ipynb` for **differential expression analysis (DEA) figure generation**.<br>
...<br>
...<br>
...<br>


<a id="configuration"></a>
## Configuration
See coding files for details.

<a id="project-structure"></a>
## Project structure
```bash
repo_e0200-p12_all/
├─ analysis/                    # analysis workflows & outputs
│  ├─ CAPs_analysis.ipynb          # notebook for CAPs analysis
│  ├─ DEA_plot.ipynb               # notebook for DEA figures
│  ├─ CAPs_analysis/            # results for CAPs analysis
│  │  └─ figures/               # exported figures for CAPs analysis
│  ├─ DE_analysis/              # results for DEA analysis
│  │  └─ figures/               # exported figures for DEA
│  └─ Survival_analysis/        # results for survival analysis
│     └─ figures/               # survival analysis plots (KM curves, forest plots)
├─ data/                        # de-identified inputs (git-ignored)
├─ Meetings/                    # meeting slides/notes
├─ src/                         # reusable analysis functions
├─ requirements.txt             # pinned Python deps
├─ .gitignore
└─ README.md
```
<a id="reproducibility"></a>
## Reproducibility
Fixed seeds; deterministic UMAP, tSNE configs where practicable.
Consistent theme (fonts, etc.); bbox_inches='tight', transparent=True.

<a id="outputs"></a>
## Outputs
```
repo_e0200-p12_all/
└─ analysis/                    # analysis workflows & outputs
   ├─ CAPs_analysis/            # results for CAPs analysis
   │  └─ figures/               # exported figures for CAPs analysis
   ├─ DE_analysis/              # results for DEA analysis
   │  └─ figures/               # exported figures for DEA
   └─ Survival_analysis/        # results for survival analysis
      └─ figures/               # survival analysis plots (KM curves, forest plots)

repo_e0200-p12_all/
└─ Meetings/                    # meeting slides/notes
```

<a id="troubleshooting--faq"></a>
## Troubleshooting / FAQ
Common issues and fixes.

<a id="contributing"></a>
## Contributing
Internal only. Use feature branches (feat/branch…) and open a PR to main.

<a id="security--governance"></a>
## Security & governance
No PHI/PII; de-identified IDs only. Do not commit data. Follow CMRI/ProCan data handling guidelines.

<a id="license"></a>
## License
© CMRI/ProCan — internal research use.

<a id="contacts"></a>
## Contacts
* Maintainer: Edward Ni — eni@cmri.org.au
