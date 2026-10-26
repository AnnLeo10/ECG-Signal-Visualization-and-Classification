# ECG Signal Visualization and Classification

An educational Data Science project that explores Electrocardiogram (ECG) signals and uses Machine Learning to classify heartbeat segments as normal or selected abnormal beats.

## Project Overview

Electrocardiography (ECG) records the electrical activity of the heart. Visualizing ECG waveforms helps us observe patterns in cardiac signals, while Machine Learning can be used to explore differences between annotated heartbeat classes.

This project uses the **MIT-BIH Arrhythmia Database** to visualize ECG waveforms at different time intervals, inspect signal quality, extract heartbeat segments, and train a Logistic Regression model for binary heartbeat classification.

> **Disclaimer:** This project is for educational purposes only. It is not a medical diagnostic tool and must not be used to make clinical decisions.

## Objectives

- Load and explore ECG recordings and their annotations.
- Visualize ECG waveforms over 5-, 10-, and 20-second intervals.
- Assess signal quality and check for missing or non-finite values.
- Extract fixed-length heartbeat segments from annotated ECG signals.
- Classify normal and selected abnormal heartbeat segments using Logistic Regression.
- Evaluate model performance using accuracy, precision, recall, F1-score, a classification report, and a confusion matrix.

## Clinical Question

Can a Logistic Regression model distinguish normal heartbeats from selected abnormal heartbeats, specifically atrial premature beats and premature ventricular contractions, using fixed-length ECG segments?

## Dataset

**MIT-BIH Arrhythmia Database**

- **Source:** [PhysioNet — MIT-BIH Arrhythmia Database](https://physionet.org/content/mitdb/1.0.0/)
- **Recording used for visualization:** Record 100
- **Training recordings:** 100, 101, 103, 105, 108, 112, 114, 116, 119, 200, 201, and 203
- **Held-out test recording:** 106
- **Sampling frequency:** 360 Hz
- **Channels in Record 100:** MLII and V5

The dataset is accessed using the `wfdb` Python library. The raw dataset is not included in this repository.

## Target Variable

| Annotation | Label | Meaning |
|---|---:|---|
| N | 0 | Normal beat |
| A | 1 | Atrial premature beat |
| V | 1 | Premature ventricular contraction |

The selected abnormal annotations (`A` and `V`) are combined into one class, making this a binary classification task. Other annotation symbols are excluded.

## Methodology

### 1. Data Loading and Understanding

- Loaded ECG recordings and reference annotations using `wfdb`.
- Inspected sampling frequency, channel names, signal dimensions, duration, and annotation symbols.
- Examined signal statistics, including minimum, maximum, mean, and standard deviation.
- Checked for missing (`NaN`) and infinite values.

### 2. ECG Visualization

Generated separate waveform plots for the first 5, 10, and 20 seconds of the MLII channel.

### 3. Preprocessing

- Selected heartbeat annotations `N`, `A`, and `V`.
- Extracted 252-sample segments, consisting of 90 samples before and 162 samples after each annotated beat.
- Excluded segments that crossed signal boundaries or contained non-finite values.
- Encoded normal beats as `0` and selected abnormal beats as `1`.

Each segment represents approximately 0.7 seconds of ECG data at 360 Hz.

### 4. Model Training

- **Algorithm:** Logistic Regression
- **Feature scaling:** `StandardScaler`
- **Class imbalance handling:** `class_weight="balanced"`
- **Evaluation strategy:** Train on 12 recordings and test on the separate, held-out Record 106.

### 5. Evaluation

The model was evaluated using accuracy, abnormal-class precision, abnormal-class recall, F1-score, a classification report, and a confusion matrix.

## Model Results

Results obtained on the held-out test recording, Record 106:

| Metric | Result |
|---|---:|
| Accuracy | 90.08% |
| Abnormal precision | 99.08% |
| Abnormal recall | 61.92% |
| Abnormal F1-score | 0.7621 |

The test set contained 2,027 heartbeat segments: 1,507 normal and 520 selected abnormal beats.

### Interpretation

The model achieved high precision for the abnormal class, meaning most beats predicted as abnormal were actually abnormal according to the reference annotations. However, its abnormal recall was 61.92%, indicating that it missed 198 of the 520 abnormal beats.

These results apply to this particular held-out recording and do not establish clinical reliability or guarantee similar performance on other recordings.

## Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- WFDB
- Scikit-learn
- Google Colab 

## Limitations

- The model combines two abnormal beat types into one class.
- Evaluation uses only one held-out test recording.
- Class imbalance and differences between recordings can affect performance.
- The model uses raw ECG segment samples as features.

## References

MIT-BIH Arrhythmia Database — PhysioNet
WFDB Python Documentation
Scikit-learn Documentation
