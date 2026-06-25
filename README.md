# EOG-Classification

Classify horizontal EOG (electrooculography) eye-movement signals by feature extraction and nearest-neighbour matching.

## Overview

Electrooculography (EOG) measures the electrical potential produced by eye
movement. This project takes a set of labelled horizontal EOG signals, reduces
each one to a small feature vector, and then identifies an unknown test signal
by finding the labelled sample whose features are closest to it.

The whole pipeline lives in [`main.ipynb`](main.ipynb):

1. Load the labelled signals from `2- Horizontal Signals.xlsx` (each column is
   one signal; the last row holds the label).
2. Extract features from every signal and build a feature matrix
   (`Features-Matrix.xlsx`).
3. Load the unknown signal from `3- Test Signal.txt` and extract the same
   features.
4. Classify it with a 1-nearest-neighbour rule using Euclidean distance over the
   standardized feature vectors, and report the matched label.

## Features extracted

Each signal is summarised by seven features:

- Mean
- Standard deviation
- Maximum peak value
- Area under the curve (Simpson's rule)
- Three autoregression coefficients (`AutoReg`, lags = 2)

## Tech stack

- Python (Jupyter Notebook)
- pandas, NumPy
- SciPy (`scipy.integrate.simpson`, `scipy.spatial.distance.euclidean`)
- statsmodels (`AutoReg`)
- matplotlib
- openpyxl (Excel I/O)

## Getting started

Prerequisites: Python 3 and Jupyter.

```bash
pip install pandas numpy scipy statsmodels matplotlib openpyxl jupyter
```

## Usage

Open the notebook and run the cells top to bottom:

```bash
jupyter notebook main.ipynb
```

The final cell prints the label of the labelled signal that most closely matches
the test signal in `3- Test Signal.txt`.

## Project structure

```
main.ipynb                  # full pipeline: load, extract features, classify
2- Horizontal Signals.xlsx  # labelled EOG signals (one per column)
3- Test Signal.txt          # unlabelled signal to classify
Features-Matrix.xlsx        # generated feature matrix
```

## License

Released under the [MIT License](LICENSE).
