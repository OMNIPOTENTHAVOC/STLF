# Short-Term Load Forecasting (STLF) with ADMS Integration

This repository contains an end-to-end pipeline for Short-Term Load Forecasting (STLF) using advanced deep learning techniques, combined with an Automated Distribution Management System (ADMS)-based optimization module. It is designed to forecast regional electrical load and optimize load shedding/restoration decisions to maintain grid balance.

## Project Structure

```
STLF_project/
├── data/
│   ├── SEM.csv                  # Raw electrical load data
│   ├── demand_5min.csv          # 5-minute resampled load data (output)
│   ├── features_5min.csv        # Engineered feature dataset
│   ├── demand_forecast.csv      # Forecasted load data output
│   ├── generation_forecast.csv  # Generation forecast input (optional)
│   └── ...                     # Other data supporting files
├── models/                      # Saved models and scalers
├── plots/                       # Visualizations output
├── logs/                        # ADMS log outputs
└── stlf_notebook.ipynb          # Main Jupyter notebook with full workflow
```

## Setup Instructions

### Environment

- Python 3.7 or higher recommended
- Install dependencies via pip:

```bash
pip install tensorflow scikit-learn pandas numpy matplotlib seaborn holidays requests pulp joblib
```

Alternatively, run this command in your notebook or terminal.  
You can also install all dependencies at once by running:

```bash
pip install -r requirements.txt
```

_(See section [Requirements File](#requirements-file) below)_

### Data Preparation

- Place your raw load data as `SEM.csv` inside the `data/` folder.
- Optionally provide generation forecasts as `generation_forecast.csv` in the same folder to run realistic ADMS simulations.
- The pipeline automatically processes and creates the required files (`demand_5min.csv`, `features_5min.csv`, etc.).

## Usage

1. Mount your Google Drive or set your `base_path` accordingly in the notebook.
2. Run the notebook `stlf_notebook.ipynb` sequentially to:
   - Load and preprocess data
   - Engineer features
   - Define, train, and evaluate the forecasting model
   - Run ADMS optimization for load shedding/restoration decisions
   - Generate output plots and logs
3. Inspect results and logs inside the `plots/` and `logs/` directories.

## Evaluation Metrics and Their Interpretation

| Metric        | Purpose                                                         | Ideal Value / Meaning                                      |
|---------------|-----------------------------------------------------------------|------------------------------------------------------------|
| **MAE**       | Mean Absolute Error: average absolute deviation (in MW)         | Lower is better; indicates average forecasting error       |
| **MSE**       | Mean Squared Error: squares errors to penalize large errors     | Lower is better; sensitive to large deviations             |
| **RMSE**      | Root MSE: square root of MSE in MW (same units as target)       | Lower is better; easily interpretable as MW error scale    |
| **MAPE**      | Mean Absolute Percentage Error: percentage error relative to true load | Lower is better; 0.9 is high efficiency                   |

*Replace values above with those from your latest run's output.*

## Customization

- Adjust model architecture, training parameters, and sequence length inside the notebook.
- Customize load profiles, priorities, and the ADMS operational parameters like buffer and cooldown periods to match your system’s requirements.
- Replace synthetic generation forecasts with real/forecasted generation data for realistic operation.

## Requirements File

The `requirements.txt` file included in the repository contains exact package dependencies to reproduce the environment easily.  
To install all required packages, run:

```bash
pip install -r requirements.txt
```

### Contents of `requirements.txt`:

```
tensorflow>=2.6.0
scikit-learn>=1.0
pandas>=1.3.0
numpy>=1.21
matplotlib>=3.4
seaborn>=0.11
holidays
requests
pulp
joblib
```

For local Jupyter Notebook environments, you may optionally install:

```
notebook
ipykernel
```

## Quick Environment Setup

Clone the repository, then run:

```bash
pip install -r requirements.txt
```

If using Google Colab, copy-paste the pip install commands into a dedicated notebook cell before running the pipeline.
