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


## Visualizations

Below are key outputs from the analysis pipeline that capture calcium signaling dynamics in T cells:

### 1. Single-Cell Calcium Curve
This plot shows the characteristic intensity spike during calcium influx in a representative T cell.
![Calcium Curve]<img width="581" alt="Screenshot 2025-04-20 at 8 51 34 PM" src="https://github.com/user-attachments/assets/91e061f1-382a-4485-a96a-7788c9fb3d3d" />

### 2. Activated T Cells
Time-series traces from a subset of 50 activated cells, with red peaks marking the activation event (derivative threshold >10).
![Activated Cells]<img width="905" alt="Screenshot 2025-04-20 at 8 51 57 PM" src="https://github.com/user-attachments/assets/fd695c58-b207-4f65-b9ac-c5d8486e7785" />

### 3. Deactivated T Cells
Representative curves from 50 non-responsive cells showing no significant calcium influx.
![Deactivated Cells]<img width="905" alt="Screenshot 2025-04-20 at 8 52 12 PM 1" src="https://github.com/user-attachments/assets/10b09ae7-3145-4d52-94bb-10c4000dbf53" />

### 4. Mean Intensity Across All Cells
Aggregate view of calcium activity across the full cell population (n = 522), including both responders and non-responders.
![Average Intensity All]<img width="563" alt="Screenshot 2025-04-20 at 8 52 36 PM" src="https://github.com/user-attachments/assets/feb62cc2-e31c-4804-a017-54a24ad74370" />


### 5. Post-Onset Intensity in Activated Cells
Average calcium intensity over time in the subset of activated cells (n ≈ 265), realigned to the point of activation.
![Activated Avg Intensity]<img width="576" alt="Screenshot 2025-04-20 at 8 52 52 PM" src="https://github.com/user-attachments/assets/7db57e36-edab-494b-a337-7d994ba70058" />


## Insights & Applications
- Enables quantification of T cell heterogeneity in calcium signaling
- Provides baseline for comparing response under different treatments
- Framework adaptable to other time-series cell signaling datasets


## License
This project is open-sourced under the MIT License.
