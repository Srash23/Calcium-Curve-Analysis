# Calcium Signaling Dynamics in T Cells

This repository presents a high-throughput analytical pipeline to quantify, visualize, and classify calcium activation events in single T cells. The analysis processes time-series fluorescence intensity data from over 29,000 measurements, captured across 522 individual cell tracks.


## Project Overview
Calcium signaling is a key regulator of immune responses. This project reconstructs cell-specific activation curves from microscopy-based time-lapse data and identifies which T cells become activated based on their calcium flux signatures. 

We focus on smoothing, gap-filling, and derivative-based detection of activation peaks.


## Objectives
- Preprocess noisy calcium intensity data from individual T cell tracks
- Interpolate and standardize time series for comparative analysis
- Detect activation events via derivative-based peak detection
- Classify cells as Activated or Non-Activated
- Quantify population-level activation dynamics


## Dataset Description
The input file is an Excel sheet (`calcium_curves.xlsx`) containing:

| Column Name       | Description                              |
|-------------------|------------------------------------------|
| Intensity Mean    | Calcium signal per cell per timepoint    |
| Time              | Frame number (1–121)                     |
| TrackID           | Unique identifier for each cell track    |

Total data points: **28,940** across **522 cell tracks**


## Pipeline Summary

### 1. Data Preprocessing
- Extract `Intensity Mean`, `Time`, and `TrackID`
- Sort values by `TrackID` and `Time`
- Detect and interpolate missing timepoints for each cell

### 2. Signal Smoothing & Derivatives
- Apply a moving average (window = 5) to smooth calcium traces
- Compute derivative of smoothed signal to detect rapid changes

### 3. Activation Detection
- Define activation as a positive peak in derivative > 10
- Use `scipy.signal.find_peaks` to identify these events
- Classify each TrackID as **Activated** or **Not Activated**

### 4. Population-Level Metrics
- Visualize activated vs non-activated cell dynamics
- Compute percent activation across the dataset
- Align activation curves to activation onset (T = 0)
- Generate error-bar plots with standard error


## Key Results
- **Total Cells Processed**: 522
- **Activated Cells**: 267
- **Activation Rate**: 51.1%
- Peak-aligned population curve highlights coordinated activation kinetics across T cells


## Tech Stack
- **Python**: pandas, numpy, matplotlib, scipy
- **Signal Processing**: moving averages, derivative curves
- **Peak Detection**: `scipy.signal.find_peaks`


## Example Visualizations
- Activation vs non-activation heatmaps
- Derivative plots per cell
- Time-aligned calcium intensity with error bands


## How to Run
```bash
# Clone this repo
$ git clone https://github.com/your-username/calcium-tcell-analysis.git

# Open Jupyter or your IDE and run the main notebook
```

## Insights & Applications
- Enables quantification of T cell heterogeneity in calcium signaling
- Provides baseline for comparing response under different treatments
- Framework adaptable to other time-series cell signaling datasets


## 📄 License
This project is open-sourced under the MIT License.
