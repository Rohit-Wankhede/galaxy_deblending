# Galaxy Deblending with Deep Learning

A comprehensive computer vision and deep learning workflow for galaxy image deblending, processing astronomical surveys, patch extraction, flux calibration, and variational autoencoder (VAE) inference.

---

## 📌 Project Overview

Astronomical imaging surveys frequently capture overlapping ("blended") galaxy sources. This repository provides a complete pipeline to:

1. **Process & Catalog Raw Astronomical Data:** Clean catalogs, perform flux calibration, match celestial objects, and extract spatial patches/tiles.
2. **Dataset Generation:** Partition astronomical fields into TensorFlow and PyTorch-compatible tile matrices for machine learning workflows.
3. **Model Inference & Benchmarking:** Train and run probabilistic generative models (such as Variational Autoencoders via `debvader`) to perform source separation and deblending.

---

## 📁 Repository Structure

```text
├── cleaning.ipynb                      # Catalog filtering & pre-processing
├── dataset_divide.ipynb                # Train/Val/Test split assignment
├── flux_calibration.ipynb              # Photometry & flux calibration routines
├── patch_selection_script.ipynb        # Spatial patch selection & filtering
├── Slicing and tiling.ipynb            # Tile/patch matrix extraction
├── tensorflow_compatible.ipynb         # Pipeline conversion for TF/Keras formats
├── VAE_FINAL INFERENCE.ipynb           # Final VAE model inference & benchmarks
├── testing grounds.ipynb               # Experimental scratchpad
│
├── PROCESSED/
│   ├── figures/                        # Generated analysis plots and figures
│   │   └── galleries/                  # Visual evaluation galleries (best/worst fits)
│   ├── model_comparison_results/       # Metric evaluations & residual results (.parquet)
│   ├── tile_manifest.parquet           # Metadata manifest for extracted tile patches
│   ├── tile_manifest_tf.parquet        # TensorFlow dataset manifests
│   └── patch_split_assignment.parquet  # Partition mapping for dataset splits
│
├── requirements.txt                    # Primary Python dependencies
└── .gitignore                          # Excluded virtual environments & heavy data
```

---

## 📊 Dataset & External Setup Instructions

Due to GitHub's file storage limits, the heavy raw survey data (~15 GB) and multi-gigabyte tile arrays are hosted externally on **Kaggle**.

### 1. Download External Datasets

Download the following dataset components from Kaggle:

- **Raw Data (`RAW/`):** Original survey images and FITS files.
- **Tile Datasets (`TILES/` & `TILES_TF/`):** Cutout image patches and tensor representations.
- **Catalogs (`.parquet`):** `cleaned_catalog.parquet` and `cleaned_catalog_with_blendedness_truth.parquet`.

👉 **[Download Dataset on Kaggle](https://www.kaggle.com/datasets/rohitwankhede123/galaxy-deblending-dataset)** 

### 2. Local Directory Placement

Extract the downloaded files into your local repository folder so the directory structure matches:

```text
GALAXY_DEBLENDING_DATASET/
├── RAW/                                     # Extracted raw files
├── PROCESSED/
│   ├── TILES/                               # Extracted image tile arrays
│   ├── TILES_TF/                            # Extracted TensorFlow tiles
│   ├── cleaned_catalog.parquet
│   └── cleaned_catalog_with_blendedness_truth.parquet
```

---

## 🛠️ Environment Setup & Installation

### 1. Virtual Environment Creation

Create and activate a Python virtual environment:

```bash
# Create environment
python -m venv deblend_env

# Activate on Windows
deblend_env\Scripts\activate

# Activate on Linux/macOS
source deblend_env/bin/activate
```

### 2. Install Dependencies

Install all required libraries using `requirements.txt`:

```bash
pip install -r requirements.txt
```

### 3. Setup Legacy Keras for VAE Inference

The `debvader` model architecture relies on legacy TensorFlow Keras. Set the following environment variable in your Python scripts or Jupyter notebooks before importing TensorFlow:

```python
import os
os.environ["TF_USE_LEGACY_KERAS"] = "1"
```

---

## 🚀 Pipeline Workflow Execution

To reproduce the project workflow end-to-end, execute the notebooks in the following sequence:

1. **`cleaning.ipynb`** — Filters raw catalog tables and creates catalog baselines.
2. **`flux_calibration.ipynb`** — Performs flux conversions and brightness calibrations.
3. **`patch_selection_script.ipynb`** — Selects candidate coordinates for galaxy patch extraction.
4. **`Slicing and tiling.ipynb`** — Slices FITS/image fields into square numpy matrices.
5. **`dataset_divide.ipynb`** — Generates balanced train/validation/test splits (`patch_split_assignment.parquet`).
6. **`tensorflow_compatible.ipynb`** — Formats arrays into TF Dataset pipelines.
7. **`VAE_FINAL INFERENCE.ipynb`** — Evaluates model performance and generates reconstruction figures.

---

## 📈 Evaluation & Results

Visual evaluation outputs and residual performance plots can be found under `PROCESSED/figures/`:

- **Reconstruction Metrics:** Check `PROCESSED/model_comparison_results/` for validation scores.
- **Visual Verification:** Check `PROCESSED/figures/galleries/` for best-case and worst-case galaxy deblending reconstructions across blendedness tiers.
