# Deep Learning for Respiratory Rate (RR) Prediction from PPG (BIDMC)

This repository contains code and documentation for predicting **respiratory rate (RR)** from **photoplethysmography (PPG)** signals using deep learning (CNN/LSTM) with optional denoising autoencoders. The project evaluates which model performs best on the **BIDMC PPG and Respiration Dataset** (PhysioNet).

> **Goal:** Build a reproducible pipeline to preprocess PPG, optionally denoise, train models to predict RR, and report metrics (MAE, RMSE, correlation), then compare models.

## Repository Structure

```
.
├── FINAL CODE DISERTATION.ipynb    # Main notebook (training + evaluation)
├── Project Dissertation (3).pdf     # Project proposal (methods & plan)
├── data/                            # (empty) place dataset files here (see below)
│   └── README.md
├── results/                         # (optional) save figures/metrics here
├── requirements.txt
├── .gitignore
├── LICENSE
└── README.md
```

## Dataset

- **Name:** BIDMC PPG and Respiration Dataset (v1.0.0, CSV format)
- **Source:** PhysioNet (Beth Israel Deaconess Medical Center subset of MIMIC-II)
- **Contents:** 53 recordings, each 8 minutes; PPG, impedance respiration, ECG sampled at 125 Hz; numerics (RR, HR, SpO₂) sampled at 1 Hz; manual breath annotations by two annotators.
- **Link (CSV panel):** https://physionet.org/content/bidmc/1.0.0/bidmc_csv/

> **Do not commit raw data.** Download locally and keep under `data/`. See `data/README.md` for exact file placement.

**License & Attribution:** The dataset is distributed via PhysioNet under an attribution license. Please read the license on the dataset page and **cite the authors** (Pimentel, Johnson, Charlton, Clifton) and the associated IEEE TBME paper when you use the data in publications (see *Citation* below).

## Quickstart

### 1) Clone the repo

```bash
git clone https://github.com/<YOUR-USERNAME>/<YOUR-REPO-NAME>.git
cd <YOUR-REPO-NAME>
```

### 2) Create a Python environment and install deps

```bash
python -m venv .venv
# Windows PowerShell
. .venv/Scripts/Activate.ps1
# macOS/Linux
source .venv/bin/activate

pip install --upgrade pip
pip install -r requirements.txt
```

### 3) Download the dataset (do not commit it)

- Open: https://physionet.org/content/bidmc/1.0.0/bidmc_csv/
- Download the `*_Signals.csv`, `*_Breaths.csv`, and other CSVs you need.
- Place them under: `data/` (keep original filenames).

### 4) Run the notebook

Open `FINAL CODE DISERTATION.ipynb` in Jupyter/Colab and run cells in order. The notebook:
- Loads and cleans the PPG signal
- (Optionally) denoises with an autoencoder
- Trains CNN/LSTM models to predict RR
- Evaluates models using MAE, RMSE, and correlation
- Saves plots/metrics (you can direct outputs to `results/`)

### 5) Reproducible runs

- Seed setting is included in the notebook where applicable.
- Export results to `results/metrics.json` and figures to `results/figures/` (optional).

## How to Compare Models

1. Enable/disable the denoising step and record metrics.
2. Train each model (e.g., **CNN**, **LSTM**, **CNN+LSTM hybrid**, **baseline regressor**) using identical splits.
3. Report **MAE**, **RMSE**, **Pearson r** and consider Bland–Altman plots for agreement.
4. Summarize in a table and pick the best model on the held-out test set.

## Expected Results (to fill in)

| Model              | MAE (↓) | RMSE (↓) | r (↑) |
|-------------------|---------:|---------:|-----:|
| Baseline          |         |          |      |
| CNN               |         |          |      |
| LSTM              |         |          |      |
| CNN+LSTM (hybrid) |         |          |      |

> Replace the above with your final numbers and include sample predictions/plots from `results/`.

## Reproducibility & Hardware

- Python 3.10+
- Runs on CPU or GPU (TensorFlow/Keras). GPU recommended for faster training.

## Citation

If you use this repository or the BIDMC dataset, please cite appropriately. For the dataset (and paper on robust RR estimation from pulse oximeters):

- **Pimentel MAF, Johnson AEW, Charlton PH, Watkinson PJ, Tarassenko L, Clifton DA.** *Towards a Robust Estimation of Respiratory Rate from Pulse Oximeters*. IEEE Transactions on Biomedical Engineering, 2017.

Also cite the PhysioNet dataset page:

- **BIDMC PPG and Respiration Dataset (v1.0.0).** PhysioNet. https://physionet.org/content/bidmc/1.0.0/

## License

Code in this repository is released under the **MIT License** (see `LICENSE`). The **BIDMC dataset is not included** and is governed by its own license and terms on PhysioNet—review those terms before use.

## Acknowledgements

- PhysioNet and the BIDMC dataset authors.
- TensorFlow/Keras and the scientific Python ecosystem.
