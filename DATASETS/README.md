# DATASETS Directory Manifest & Documentation

This folder contains all benchmark and custom datasets utilized for the research paper on **Real-Time Frontal EEG Emotion Recognition via Metaheuristic Optimization**.

All datasets in this directory are fully validated, cleaned, properly labeled, and free of missing or null values.

---

## 1. Custom Frontal EEG Wearable Dataset

* **Acquisition Setup:** 3 frontal dry channels (**Fp1, Fp2, Fz**) operating at 256 Hz across 9 healthy human subjects.
* **Trial Count:** **8,388 balanced trial epoch windows** (1-second windows, 128 samples per window).
* **Target Classes:** Discrete affective states: `Happy` (2,796 trials), `Neutral` (2,796 trials), `Sad` (2,796 trials).

### A. Preprocessed Signal & Raw Feature Datasets

1. **[`psd_dataset_8k.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/psd_dataset_8k.csv)**
   * **Role:** Primary unoptimized feature dataset extracted via Welch's Power Spectral Density (PSD) across 5 frequency bands (\(\delta, \theta, \alpha, \beta, \gamma\)).
   * **Shape:** \(8,388 \times 4\) (PSD feature columns + `Emotion` target label).
   * **Usage:** Serves as the unoptimized baseline input for all classifier benchmark evaluations and feature selection optimization loops.

2. **[`eeg_preprocessed_full.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/eeg_preprocessed_full.csv)**
   * **Role:** Preprocessed time-series EEG data after FIR bandpass filtering (0.5–45 Hz), FastICA artifact removal, and z-score normalization (+28% SNR improvement).
   * **Shape:** \(10,000 \times 7\) (`Time`, `POz`, `Oz`, `P3`, `P4`, `O1`, `O2`).
   * **Usage:** Denoising validation and time-series feature analysis.

---

## 2. Metaheuristic-Optimized Custom Feature Datasets

The following 8 datasets represent the optimal feature subsets selected by nature-inspired metaheuristic optimizers on the custom dataset. Each dataset has shape \(8,388 \times 4\) with zero missing values and balanced emotion classes:

1. **[`woa_optimized_psd_dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/woa_optimized_psd_dataset.csv)** — Selected by Whale Optimization Algorithm (WOA). Achieved peak overall accuracy of **83.3%** with Ensemble (Bagged Trees).
2. **[`de_optimized_psd_dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/de_optimized_psd_dataset.csv)** — Selected by Differential Evolution (DE). Achieved **81.1%** accuracy with Ensemble (Bagged Trees) and top F1-score for sad emotion detection.
3. **[`pso_optimized_psd_dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/pso_optimized_psd_dataset.csv)** — Selected by Particle Swarm Optimization (PSO). Achieved **81.0%** accuracy.
4. **[`ga_optimized_psd_dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/ga_optimized_psd_dataset.csv)** — Selected by Genetic Algorithm (GA). Achieved **80.9%** accuracy.
5. **[`aco_optimized_psd_dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/aco_optimized_psd_dataset.csv)** — Selected by Ant Colony Optimization (ACO). Achieved **80.7%** accuracy.
6. **[`bbo_optimized_psd_dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/bbo_optimized_psd_dataset.csv)** — Selected by Biogeography-Based Optimization (BBO).
7. **[`firefly_optimized_psd_dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/firefly_optimized_psd_dataset.csv)** — Selected by Firefly Algorithm (FA).
8. **[`gwo_optimized_psd_dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/gwo_optimized_psd_dataset.csv)** — Selected by Grey Wolf Optimization (GWO).

---

## 3. Public DEAP Benchmark Datasets (Cross-Dataset Validation)

1. **[`DEAP_Dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/DEAP_Dataset.csv)**
   * **Role:** Benchmark 32-channel public DEAP EEG signal dataset used to evaluate model generalizability.
   * **Shape:** \(8,064 \times 32\) (32 electrode channels: `Fp1`, `AF3`, `F3`, `F7`, `FC5`, `FC1`, `C3`, `T7`, `CP5`, `CP1`, `P3`, `P7`, `PO3`, `O1`, `Oz`, `Pz`, `Fp2`, `AF4`, `Fz`, `F4`, `F8`, `FC6`, `FC2`, `Cz`, `C4`, `T8`, `CP6`, `CP2`, `P4`, `P8`, `PO4`, `O2`).
   * **Null Values:** 0 (cleaned of trailing empty columns).

2. **[`de_optimized_deap_dataset.csv`](file:///e:/Study/MATH%20RESEARCH/EEG/DATASETS/de_optimized_deap_dataset.csv)**
   * **Role:** DE-Optimized feature subset extracted from the DEAP corpus.
   * **Shape:** \(7,937 \times 64\) (64 selected features + `Emotion` target label).
   * **Classes:** `Neutral` (2,651), `Sad` (2,643), `Happy` (2,643).
   * **Performance:** Achieved peak validation accuracy of **98.68%** (Ensemble Bagged Trees) and **98.75%** (Fine KNN).

---

## 4. Integrity Summary

| Dataset File | Shape | Missing Values | Target Label | Class Distribution |
| :--- | :---: | :---: | :---: | :--- |
| `psd_dataset_8k.csv` | \(8,388 \times 4\) | 0 | `Emotion` | Happy: 2,796, Neutral: 2,796, Sad: 2,796 |
| `eeg_preprocessed_full.csv` | \(10,000 \times 7\) | 0 | None | N/A (Preprocessed Signal Matrix) |
| `woa_optimized_psd_dataset.csv` | \(8,388 \times 4\) | 0 | `Emotion` | Happy: 2,796, Neutral: 2,796, Sad: 2,796 |
| `de_optimized_psd_dataset.csv` | \(8,388 \times 4\) | 0 | `Emotion` | Happy: 2,796, Neutral: 2,796, Sad: 2,796 |
| `pso_optimized_psd_dataset.csv` | \(8,388 \times 4\) | 0 | `Emotion` | Happy: 2,796, Neutral: 2,796, Sad: 2,796 |
| `ga_optimized_psd_dataset.csv` | \(8,388 \times 4\) | 0 | `Emotion` | Happy: 2,796, Neutral: 2,796, Sad: 2,796 |
| `aco_optimized_psd_dataset.csv` | \(8,388 \times 4\) | 0 | `Emotion` | Happy: 2,796, Neutral: 2,796, Sad: 2,796 |
| `bbo_optimized_psd_dataset.csv` | \(8,388 \times 4\) | 0 | `Emotion` | Happy: 2,796, Neutral: 2,796, Sad: 2,796 |
| `firefly_optimized_psd_dataset.csv` | \(8,388 \times 4\) | 0 | `Emotion` | Happy: 2,796, Neutral: 2,796, Sad: 2,796 |
| `gwo_optimized_psd_dataset.csv` | \(8,388 \times 4\) | 0 | `Emotion` | Happy: 2,796, Neutral: 2,796, Sad: 2,796 |
| `DEAP_Dataset.csv` | \(8,064 \times 32\) | 0 | None | N/A (32 EEG Channels Signal Matrix) |
| `de_optimized_deap_dataset.csv` | \(7,937 \times 64\) | 0 | `Emotion` | Neutral: 2,651, Sad: 2,643, Happy: 2,643 |
