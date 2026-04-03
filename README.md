# CEG3004_Project_MuhammadHafisBinSamat
# Environmental Sound Classification (CEG3004)
# 1. Overview

This project implements an audio classification system for environmental sounds using the ESC-50 dataset. Each audio clip is 5 seconds long and must be classified into one of 50 sound categories.

The key objective is not only to perform well on clean audio, but also to remain reliable under real-world distortions such as noise and limited frequency bandwidth.

# 2. System Pipeline

The system consists of three main stages: preprocessing, feature extraction, and classification.

# 2.1 Audio Preprocessing

Each audio clip is standardised before feature extraction:

Silence Trimming
Removes low-energy segments at the beginning and end of the signal.
Amplitude Normalization
Scales the waveform to ensure consistent loudness across clips.
Fixed-Length Enforcement (5 seconds)
Clips are padded or truncated to maintain a uniform duration.
Pre-emphasis Filtering
A simple high-pass filter is applied to enhance higher frequencies, which improves robustness for band-limited audio.

These steps reduce variability and improve the consistency of the extracted features.

# 2.2 Feature Extraction

A combination of spectral and time-domain features is used to represent each audio clip.

(a) MFCC-Based Features
20 MFCC coefficients
First-order delta (Δ)
Second-order delta (ΔΔ)

These capture the timbral characteristics and short-term dynamics of the sound.

(b) Log-Mel Spectrogram
64 Mel frequency bands
Converted to log scale

This provides a detailed representation of the frequency distribution and is more robust to noise.

(c) Spectral Features
Spectral Centroid → indicates brightness
Spectral Bandwidth → spread of frequencies
Spectral Rolloff → frequency where most energy lies
Spectral Flux → rate of spectral change

These features help distinguish sounds with similar MFCC profiles.

(d) Time-Domain Features
Zero Crossing Rate (ZCR) → measures noisiness
Root Mean Square Energy (RMS) → overall signal energy
(e) Feature Aggregation

Since features are computed over time frames, statistical pooling is applied:

Mean
Standard deviation
Median

Median pooling is included to reduce sensitivity to noise and outliers.

# 2.3 Classification Model

A Support Vector Machine (SVM) with an RBF kernel is used.

Reasons for this choice:

Handles non-linear class boundaries effectively
Performs well with high-dimensional feature vectors
Suitable for moderate-sized datasets

Class imbalance is handled using balanced class weights.

# 3. Results and Analysis

The dataset was split into training and validation sets using an 80/20 split.

Validation Macro F1-score: ~0.61
Observations:
Strong performance on distinct sound classes (e.g., water and natural sounds)
Moderate performance on common environmental sounds
Lower performance on acoustically similar classes (e.g., engine vs helicopter)
Some classes show low recall, indicating confusion between similar patterns

Overall, the model demonstrates stable performance across a wide range of classes.

# 4. Robustness Considerations

The system is designed to perform under:

Clean audio
Noisy audio
Band-limited audio

Robustness is achieved through:

Preprocessing (normalization and trimming)
Use of diverse spectral and time-domain features
Inclusion of median pooling to reduce sensitivity to distortions

# 5. Experiments and Improvements

The following improvements were made over the baseline implementation:

Added log-mel spectrogram features
Introduced spectral features (centroid, bandwidth, rolloff, flux)
Included median pooling for improved robustness
Replaced Logistic Regression with SVM

These changes improved both performance and stability across different conditions.

# 6. How to Run
Open the provided notebook or Python script
Install required dependencies
Run all cells from top to bottom
The following outputs will be generated:
Pr_5_model.joblib
Pr_5_predictions.csv

# 7. Dependencies

The project uses the following Python libraries:

numpy
pandas
librosa
scikit-learn
joblib
matplotlib (optional)
Install dependencies
pip install numpy pandas librosa scikit-learn joblib matplotlib

# 8. Reproducibility

To ensure reproducibility:

A fixed random seed (random_state=42) is used for data splitting
The dataset is automatically downloaded and extracted via the script
Feature extraction and preprocessing steps are deterministic
Model hyperparameters are explicitly defined
Steps to reproduce results
Clone the repository
Open the notebook or Python script
Run all cells sequentially
Outputs generated:
Pr_5_model.joblib
Pr_5_predictions.csv
