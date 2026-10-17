# VRESEE Video Classification Competition

## 📌 Overview

This repository hosts the **VRESEE Video Classification Challenge**, a deep learning competition based on features extracted from the **VRESEE** videos. Participants are required to design and train **deep learning models** (e.g., 1D-CNN, LSTM/GRU, Transformer) to classify each video into one of **four classes** using the frame-level features extracted from it.

## Difficulty level

Each video is provided as a **sequence of 300 frames with 670 features per frame**, while only **180 labeled training videos** are available. Models must learn temporal patterns from high-dimensional, noisy signals with very little training data, so careful regularization is essential.

## 🏆 Leaderboard

- Leaderboard scores are automatically updated based on accuracy.
- View the live leaderboard:
👉 **[Leaderboard](https://tasneem-mselim.github.io/VRESEE_Competition/)**

---

## 🧠 Task Description

* Each CSV file represents **one video**.
* Each row in a CSV is **one video frame**, and each column is an extracted feature (gaze, eye landmarks, head pose, face landmarks, action units, ...).
* Each video belongs to **one of 4 classes**: `0`, `1`, `2`, `3` (CLASS_MEANING_HERE).

### Objective

Train a model that accurately predicts the class label of **labeled test videos**, using:

* The frame-level features in each video CSV
* The temporal order of the frames

---

## 📊 Dataset Details

The dataset is derived from the **VRESEE** videos. Features were extracted from every video and stored as one CSV file per video. Video ids follow the pattern `person<N>_<clip>` (e.g., `person12_001`), which is also the CSV file name.

| Property          | Value                                |
| ----------------- | ------------------------------------ |
| Samples           | One CSV file per video               |
| Frames per video  | 300 (rows)                           |
| Features          | 670 numeric columns per frame        |
| Classes           | 4 (`0`, `1`, `2`, `3`)               |
| Train videos      | 180 (45 per class)                   |
| Validation videos | 45 (12 / 11 / 11 / 11 per class)     |
| Test videos       | 75 (labels hidden)                   |

### Feature columns

Each CSV contains:

* **Meta columns:** `frame`, `face_id`, `timestamp`, `confidence`, `success`
* **Gaze:** gaze direction vectors and angles
* **Eye landmarks:** 2D / 3D eye region landmarks
* **Head pose:** head location and rotation
* **Face landmarks:** 2D / 3D facial landmarks
* **Action units:** facial action unit intensities and presence

> Column names may contain leading spaces; strip them when loading (`df.columns = df.columns.str.strip()`).

---

### Public Files

##### These files are available in the dataset folder for participants:

```
Dataset/
├── train/
│   ├── 0/   *.csv      (videos of class 0)
│   ├── 1/   *.csv
│   ├── 2/   *.csv
│   └── 3/   *.csv
├── validate/
│   ├── 0/   *.csv
│   ├── 1/   *.csv
│   ├── 2/   *.csv
│   └── 3/   *.csv
└── test/
    ├── prediction.csv  (template: list of test ids, empty labels)
    └── ...   *.csv     (videos to be classified, no labels)
```

1- `train/` — labeled videos, the class is the name of the sub-folder

2- `validate/` — labeled videos for validation and model selection

3- `test/` — unlabeled videos to classify

4- `test/prediction.csv` — template containing the test ids

5- `starter_code.ipynb` — baseline 1D-CNN notebook (Keras)

### Private Files

- Test labels → Hidden ground-truth data used for automatic evaluation

---

## 📝 How to Submit Your Results

Follow the steps below to submit your predictions to the competition leaderboard.

---

### Step 1: Fork the Repository

### Step 2: Navigate to Your Forked Repository

### Step 3: Go to the Submission Folder

### Step 4: Prepare the prediction .csv locally

#### 📝 Submission Format

Participants must submit a CSV file named **`prediction.csv`** with the following format:

```csv
id,label
person12_001,0
person21_001,1
person25_010,3
...
```

#### Rules

* `id` must match the ids in the provided `test/prediction.csv` (the video file name without `.csv`)
* `label` must be an integer in `{0, 1, 2, 3}`
* Every test id must have exactly one label

### Step 5: Place Your Submission in the Submission Folder

Upload your `prediction.csv` to the submission folder in your forked repo.

> Encrypt the submissions, first run:
> `python encrypt_submission.py prediction.csv prediction.enc public_key.pem`
> and upload both `prediction.enc` and `prediction.enc.key` instead of the CSV.

### Step 6: Create a Pull Request

✅ Your submission will be reviewed and evaluated, and the results will be added to the leaderboard.

**Only one submission** is allowed for each participant/team. Subsequent submissions will be automatically rejected.

---

## 📈 Evaluation Metric

Submissions are evaluated using:

* **Accuracy**
* **F1-Score**

Evaluation is performed on a **hidden test set** to prevent data leakage.

---

## ✅ Allowed Methods

* Any **deep learning** architecture (CNN, RNN/LSTM/GRU, Transformer, hybrid models)
* Feature selection, preprocessing, and normalization
* Padding / cropping / resampling of the frame sequences
* Data augmentation
* Hyperparameter tuning

## ❌ Not Allowed

* Using test labels
* Modifying test ids
* Training on test videos
* Using external labels or raw videos of the test set

---

## 🏆 Baseline

A starter notebook (`starter_code.ipynb`) with a simple **1D-CNN** in Keras is provided as the baseline. It reaches only about **38% accuracy on the validation set**, so there is a lot of room for improvement. Participants are encouraged to improve upon it using:

* Deeper or temporal architectures (LSTM, GRU, Transformer)
* Attention mechanisms
* Regularization techniques (dropout, batch norm, early stopping)
* Feature selection to reduce the 670 columns
* Class balancing and data augmentation

---

## 👩‍💻 Organizer

**Tasneem Selim**
If you face issues with the repository or evaluation:
- tasneem.mselim@gmail

---

Good luck, and happy coding 🚀

