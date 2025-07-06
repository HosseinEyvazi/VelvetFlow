
# VelvetFlow: An Engineering Pipeline for Robust Multi-density Clustering

## Overview

**VelvetFlow** is a robust engineering pipeline for clustering datasets with varying internal densities and for detecting outliers without requiring extensive hyperparameter tuning. It is particularly effective for complex synthetic datasets and adaptable to real-world scenarios.

The pipeline is composed of three main stages:

* **Contextual-Density Splitting**
  Classifies data into high- and low-density subsets based on relative local densities.

* **Density-Aware Clustering**
  Applies appropriate clustering algorithms (e.g., DBSCAN, HDBSCAN, FusedNeighbor) tailored to each density context.

* **Scaled MST Verification**
  Detects and verifies outliers through a scaled Minimum Spanning Tree combined with \$k\$-NN refinement.

This repository includes the full implementation of VelvetFlow, hyperparameter tuning results for various baseline methods, and per-dataset experimental notebooks.

---

## Repository Structure

```
.
├── dataset/                      # Input datasets used for clustering experiments
│   ├── synthetic.txt
│   ├── jain.txt
│   ├── isolation.txt
│   └── compound.txt
├── velvetflow_results/          # Contains 4 notebooks, one per dataset
│   ├── VelvetFlow_synthetic.ipynb
│   ├── VelvetFlow_jain.ipynb
│   ├── VelvetFlow_isolated.ipynb
│   └── VelvetFlow_compound.ipynb
├── MDBSCAN_results.ipynb        # Notebook running MDBSCAN across all datasets
├── dbscan_result/               # DBSCAN results (.xlsx per dataset)
│   ├── synthetic.xlsx
│   ├── jain.xlsx
│   ├── isolation.xlsx
│   └── compound.xlsx
├── hdbscan_result/              # HDBSCAN results (.xlsx per dataset)
│   ├── synthetic.xlsx
│   ├── jain.xlsx
│   ├── isolation.xlsx
│   └── compound.xlsx
├── requirements.txt             # Required Python packages
└── README.md
```

---

## Datasets and Experiment Setup

VelvetFlow was evaluated on four classical clustering benchmarks, all located in the `dataset/` directory:

### 1. Synthetic Dataset

A mixture of elongated filaments, tight Gaussian blobs, and isolated outliers—challenging traditional algorithms due to its density variability.

### 2. Jain Dataset

Two intertwined clusters with different internal densities, ideal for stress-testing multi-density resolution.

### 3. Isolation Dataset

Two tight clusters plus distant singletons. Sensitive to over- and under-segmentation.

### 4. Compound Dataset

A combination of compact clusters and a long low-density tail—ideal for assessing shape preservation.

---

## Results Overview

### MDBSCAN

The `MDBSCAN_results.ipynb` notebook runs MDBSCAN **four times per dataset**, testing various hyperparameter combinations. Metric summaries and best configurations are saved into `.xlsx` files under:

* `dbscan_result/`
* `hdbscan_result/`

Each `.xlsx` file includes:

* NMI, ARI, Pairwise F1
* Associated hyperparameters (e.g., `eps`, `minPts`)

### VelvetFlow

Each dataset is tested individually in `velvetflow_results/`:

| Dataset   | Notebook                     |
| --------- | ---------------------------- |
| Synthetic | `VelvetFlow_synthetic.ipynb` |
| Jain      | `VelvetFlow_jain.ipynb`      |
| Isolation | `VelvetFlow_isolated.ipynb`  |
| Compound  | `VelvetFlow_compound.ipynb`  |

Each notebook includes:

* Full pipeline application
* Outlier detection steps
* Final metric scores:

  * Normalized Mutual Information (NMI)
  * Adjusted Rand Index (ARI)
  * Pairwise F1 score

---

## Setup and Installation

### 1. Clone the repository

```bash
git clone https://github.com/HosseinEyvazi/VelvetFlow.git
cd VelvetFlow
```

### 2. Install dependencies

Using pip:

```bash
pip install -r requirements.txt
```

Or with conda:

```bash
conda create --name velvetflow-env --file requirements.txt
conda activate velvetflow-env
```

---

## Running the Notebooks

Open Jupyter Notebook or JupyterLab:

```bash
jupyter notebook
```

Then navigate to the `velvetflow_results/` directory and select any of the dataset notebooks to execute the pipeline step-by-step.

---

## Contributions

We welcome contributions! You can:

* Fork this repo and submit a pull request
* Open issues for bugs or feature requests
* Improve documentation or add more datasets

---

## License

This repository is released under the **MIT License**. See `LICENSE` for more details.

---

## Acknowledgments

VelvetFlow was developed by **Hossein Eyvazi**, **Mohammad Badzohreh**, and **Seyed Ali Shahrokhi** as part of their research in clustering algorithms and anomaly detection. We also acknowledge the creators of DBSCAN, HDBSCAN, and the benchmark datasets used in this project.

