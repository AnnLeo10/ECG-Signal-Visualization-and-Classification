# ECG Signal Visualization and Classification
ECG signal visualization and heartbeat classification using Python, WFDB, and machine learning on the MIT-BIH Arrhythmia Database.
A clinical data science experimenet using Python, the MIT-BIH Arrhythmia Database, ECG waveform visualization, and machine learning.

## Project Overview

Electrocardiography (ECG) records the electrical activity of the heart. This project visualizes ECG signals over different time intervals and explores the classification of annotated heartbeats using Logistic Regression.

The project combines signal analysis, data preprocessing, supervised machine learning, and model evaluation.

## Objectives

- Load and inspect a public ECG dataset.
- Visualize ECG waveforms over 5, 10, and 20 seconds.
- Extract heartbeat segments using expert annotations.
- Build a binary heartbeat classification model.
- Evaluate the model using accuracy, precision, recall, F1-score, and a confusion matrix.

## Dataset

**MIT-BIH Arrhythmia Database**

Source: [PhysioNet — MIT-BIH Arrhythmia Database](https://physionet.org/content/mitdb/1.0.0/)

This experiment uses record 100, which contains two ECG channels: MLII and V5.

- Sampling frequency: 360 Hz
- Number of samples: 650,000 per channel
- Recording duration: approximately 30.09 minutes

The dataset provides expert annotations for heartbeat events.

## Tools and Technologies

- Python
- WFDB
- NumPy
- Pandas
- Matplotlib
- Scikit-learn
- Logistic Regression Model

## Methodology

1. Load ECG record 100 using WFDB.
2. Inspect the sampling frequency, channels, and recording duration.
3. Plot the first 5, 10, and 20 seconds of the MLII signal.
4. Load expert heartbeat annotations.
5. Extract 0.7-second ECG segments around selected annotated beats.
6. Label normal beats as `0` and selected abnormal beats as `1`.
7. Split the data into training and testing sets using stratification.
8. Train a standardized Logistic Regression model with balanced class weights.
9. Evaluate the model on the test set.


## Model Performance

The model was evaluated on a held-out test set containing 455 heartbeat segments.

| Metric | Result |
|---|---:|
| Accuracy | 99.78% |
| Precision | 87.50% |
| Recall | 100.00% |
| F1-score | 93.33% |


## Limitations

- The experiment uses only one ECG recording.
- The dataset is highly imbalanced, with only 34 selected abnormal beats among 2,271 extracted segments.
- Only seven abnormal beats appear in the test set.
- Heartbeat segments from the same recording may share recording-specific characteristics across the training and test sets.
- The results are preliminary and do not establish clinical reliability.

This project is intended for educational and research purposes only.

