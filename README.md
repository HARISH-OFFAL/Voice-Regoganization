# Audio Gender Clustering Using MFCC and Pitch

## Overview

This project performs **unsupervised clustering of audio files** to predict gender (male/female) using Python. It uses:

* **MFCC (Mel-Frequency Cepstral Coefficients)** for audio feature extraction.
* **KMeans clustering** from `scikit-learn`.
* **Pitch estimation** to automatically label clusters as male or female.

The script processes all `.wav` files in a dataset folder and outputs the predicted gender for each file.

---

## Features

* Automatic **MFCC feature extraction**.
* **Pitch-based labeling** of KMeans clusters.
* Works with `.wav` audio files.
* Handles multiple files in a directory.
* Outputs cluster number and predicted gender.

---

## Requirements

* Python 3.x
* Libraries:

```bash
pip install librosa numpy scikit-learn
```

---

## Usage

1. Place your `.wav` audio files in a folder, e.g., `C:\Users\haris\Downloads\Audio Data`.
2. Update the `dataset_path` variable in the script to point to your folder:

```python
dataset_path = "C:\\Users\\haris\\Downloads\\Audio Data"
```

3. Run the script:

```bash
python audio_gender_clustering.py
```

4. Output will show:

```
Found 10 audio files.
Features shape: (10, 13)
Pitches shape: (10,)
Results:
File: male1.wav - Cluster: 0 - Predicted: Male
File: female1.wav - Cluster: 1 - Predicted: Female
...
```

---

## How It Works

1. **Feature Extraction**:

   * Each audio file is loaded (first 5 seconds, sampled at 16kHz).
   * 13 MFCC features are computed and averaged.

2. **Pitch Estimation**:

   * The fundamental frequency (F0) is estimated using `librosa.pyin`.
   * Average pitch is used to differentiate male vs. female clusters.

3. **Clustering**:

   * KMeans clusters the MFCC features into 2 groups.
   * The cluster with lower average pitch is labeled **Male**, higher pitch is **Female**.

---

## Notes

* This is an **unsupervised method**: cluster numbers (0/1) may vary across runs. Pitch-based labeling corrects this.
* For best results, audio files should be clear and of at least 3–5 seconds.
* If you have many files, the script may take time to process; consider **parallel feature extraction** for speed.

---

## Example Folder Structure

```
Audio Data/
├── male1.wav
├── male2.wav
├── female1.wav
├── female2.wav
└── female3.wav
```

---

## Optional Improvements

* Use additional audio features (chroma, spectral contrast) for better clustering.
* Implement parallel processing for faster feature extraction.
* Extend to classify more than two categories (e.g., children, adults).
