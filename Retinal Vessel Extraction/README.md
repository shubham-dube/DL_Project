# Retinal Vessel Extraction: Niblack vs. Sauvola Thresholding

## 📌 Project Overview
This project focuses on extracting thin blood vessels from retinal fundus images, a critical step in diagnosing and monitoring ocular diseases such as diabetic retinopathy and glaucoma. 

Retinal images typically suffer from uneven illumination, making global thresholding methods ineffective. This project explores and compares two **local adaptive thresholding** techniques—**Niblack** and **Sauvola**—to effectively segment these fine, thin structures against varying backgrounds.

## 🎯 Objectives
* **Task:** Extract thin vessels in fundus images.
* **Methods:** Implement and compare Niblack and Sauvola adaptive thresholding.
* **Dataset:** DRIVE (Digital Retinal Images for Vessel Extraction) dataset mirrors from Kaggle.
* **Evaluation:** Compare the **Sensitivity** (True Positive Rate) of both methods.
* **Key Learning:** Understand local thresholding behavior on thin structures and the trade-off between noise reduction and structural sensitivity.

## 🗄️ Dataset
This project uses a Kaggle mirror of the standard **DRIVE dataset**. 
* **Source:** [Retina Blood Vessel Dataset (Kaggle)](https://www.kaggle.com/datasets/abdallahwagih/retina-blood-vessel)
* **Contents:** Includes original retinal images and expert manual annotations (ground truth masks) used to evaluate our algorithms.

## ⚙️ Methodology

### 1. Preprocessing
To maximize the visibility of the blood vessels before applying thresholding algorithms:
* **Green Channel Extraction:** Blood vessels absorb green light strongly, providing the highest contrast in the green channel of the RGB image.
* **CLAHE (Contrast Limited Adaptive Histogram Equalization):** Applied to enhance the local contrast of the faint vessels.
* **Inversion:** The images are inverted so the dark vessels become bright structures on a dark background, aligning with the expected input for the thresholding algorithms.

### 2. Adaptive Thresholding
* **Niblack's Method:** Calculates a dynamic threshold based on the local mean and standard deviation. Highly sensitive to thin structures but prone to amplifying background noise.
* **Sauvola's Method:** An improvement over Niblack that includes a dynamic range modifier for standard deviation. Effectively suppresses background noise but may miss the absolute faintest capillary tips.

## 🚀 Setup and Installation

### Prerequisites
* Python 3.x
* Jupyter Notebook / Google Colab
* Kaggle API configured (`kaggle.json`)

### Installation
1. Clone the repository:
   ```bash
   git clone [https://github.com/](https://github.com/shubham-dube/DL_Project)
   cd DL_Project

```

2. Install the required dependencies:
```bash
pip install opencv-python scikit-image scikit-learn matplotlib numpy kaggle

```


3. Ensure your `kaggle.json` file is placed in the correct directory (`~/.kaggle/` on Linux/Mac, or `C:\Users\<User>\.kaggle\` on Windows) to allow automatic dataset downloading.

## 💻 Usage

Open the provided Jupyter Notebook to run the pipeline:

```bash
jupyter notebook retinal_vessel_extraction.ipynb

```

The notebook is fully self-contained and will:

1. Download and extract the dataset via the Kaggle API.
2. Run the preprocessing steps.
3. Apply both Niblack and Sauvola thresholding.
4. Calculate and print the Sensitivity metrics.
5. Display a visual comparison of the results.

## 📊 Results & Learnings

* **Sensitivity Trade-off:** Niblack generally achieves a slightly higher sensitivity score due to its aggressive detection of thin structures, at the cost of high background noise (false positives). Sauvola provides a much cleaner, visually precise segmentation (higher precision/specificity) but slightly lower sensitivity, as it occasionally filters out the faintest vessels along with the noise.