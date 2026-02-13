# JPMC Take-Home Test: Income Modeling and Customer Segmentation

This repository contains an end-to-end data science workflow on U.S. Census-style data:
- Supervised classification to predict income class (`- 50000.` vs `50000+.` style labels in source data)
- Unsupervised customer segmentation for business targeting

Primary implementation is in a single notebook:
- `notebooks/income_modeling_and_segmentation.ipynb`

Fallback notebook access (if the notebook does not render in Local):
- GitHub: https://github.com/MPhaniTarun/JPMC-take-home-test
- Colab: https://colab.research.google.com/drive/1rfB68NdNPPmxIQe2z1JpaOJ9vJbea09X?usp=sharing

## Repository Structure

```text
.
├── data/
│   ├── census-bureau.data          # Raw dataset (~199k rows)
│   └── census-bureau.columns       # Column names (42 fields)
├── notebooks/
│   └── income_modeling_and_segmentation.ipynb
├── report/
│   └── report.pdf
├── requirements.txt
└── README.md
```

## Requirements

- Python 3.10+ (3.11 recommended)
- `pip`
- Jupyter (for local notebook execution)

This project has been tested with:
- Python 3.10-3.11 (recommended: 3.11)
- macOS (Apple Silicon M-series), Windows, and Linux

Warning: Python 3.13+ is not recommended, as some compiled libraries (for example `xgboost`) may not yet be fully compatible.

Python packages are listed in `requirements.txt`:
- numpy
- pandas
- matplotlib
- seaborn
- scikit-learn
- xgboost
- optuna
- ipython
- plotly

## Local Setup

### Python Installation (macOS and Windows)

Use one of the following installation options.

#### Option 1 - Normal install (no pyenv)

macOS:
- If Python 3.11 is already installed, use it.
- Or install via Homebrew:

```bash
brew install python@3.11
```

- Or download/install from Python.org:
  https://www.python.org/downloads/

Windows:
- Download and install Python 3.11 from:
  https://www.python.org/downloads/

#### Option 2 - Install and use Python 3.11 via pyenv (if available)

Use this option only if `pyenv` is already installed.

Check availability:

macOS/Linux:

```bash
command -v pyenv
```

Windows (PowerShell):

```powershell
pyenv --version
```

macOS (`pyenv`):

```bash
unset PYENV_VERSION
pyenv install 3.11.8
pyenv local 3.11.8
python --version
```

Windows (`pyenv-win`):

```powershell
pyenv install 3.11.8
pyenv local 3.11.8
python --version
```

### Create Virtual Environment and Install Dependencies

macOS/Linux:

```bash
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

Windows:

```powershell
py -3.11 -m venv .venv
.venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

### macOS Only: OpenMP Requirement for XGBoost

If you encounter:
- `XGBoost Library (libxgboost.dylib) could not be loaded`
- `Library not loaded: libomp.dylib`

Install OpenMP runtime:

```bash
brew install libomp
```

This is required for XGBoost on macOS.

### Verify Installation

After installation:

```bash
python -c "import xgboost, sklearn, optuna; print('Environment ready')"
```

If no errors appear, setup is successful.

## Compile and Execute Instructions

This project is Python/notebook-based, so there is no separate compile step. Execution is done by running notebook cells.

### Option 1: Run Locally in Jupyter

1. Start Jupyter:

```bash
jupyter notebook
```

2. Open:

```text
notebooks/income_modeling_and_segmentation.ipynb
```

3. Confirm data files are present.
- The notebook resolves paths automatically via `resolve_data_paths()`.
- Keep these files in `data/`:
  - `data/census-bureau.data`
  - `data/census-bureau.columns`
- Do not rename files or remove extensions. The `.data` and `.columns` filenames are required.

4. Run all cells in order (`Kernel -> Restart & Run All`).

### Option 2: Run in Google Colab

1. Open the shared Colab notebook:
- https://colab.research.google.com/drive/1rfB68NdNPPmxIQe2z1JpaOJ9vJbea09X?usp=sharing

2. Upload the two data files into `/content/`:
- `data/census-bureau.data`
- `data/census-bureau.columns`

3. Run all cells.

## What the Notebook Executes

The notebook covers:
- Data loading and schema assignment
- Missing-value handling and categorical encoding
- Feature engineering (income-related transformations)
- EDA
- Classification model comparison and hyperparameter tuning (Optuna)
- KMeans segmentation, profiling, and business analysis views

## Notes

- Full execution can take significant time when hyperparameter trials are high.
- If you only want a quick run, reduce tuning trials in modeling cells.
- Final written analysis is available in `report/report.pdf`.
