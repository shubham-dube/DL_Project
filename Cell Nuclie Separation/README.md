# Cell Nuclei Separation: Marker-Controlled Watershed

## 📌 Project Overview
In biological image analysis, a common challenge is segmenting dense clusters of cells where nuclei are touching or overlapping. Standard thresholding techniques fail to separate these connected components, treating them as a single object. 

This project tackles this problem by implementing the **Watershed algorithm**. Specifically, it compares a standard, unconstrained watershed approach (which notoriously leads to over-segmentation) against a robust **Marker-Controlled Watershed** pipeline to successfully separate touching nuclei.

## 🎯 Objectives
* **Task:** Separate touching nuclei in microscopy images.
* **Methods:** Standard Watershed vs. Marker-controlled Watershed.
* **Dataset:** Data Science Bowl 2018 (Nuclei Segmentation) via Kaggle.
* **Compare:** Segmentation results with and without markers.
* **Learning:** Understand the causes of over-segmentation and how morphological distance transforms and local maxima act as spatial constraints.

## 🗄️ Dataset
* **Source:** Data Science Bowl 2018. We utilize a Kaggle mirror for easy API access: [Data Science Bowl 2018 (Skooch Mirror)](https://www.kaggle.com/datasets/skooch/data-science-bowl-2018).
* **Contents:** Thousands of segmented nuclei images across various microscopy modalities.

## ⚙️ Methodology

### 1. Preprocessing & Binarization
* Convert the image to grayscale.
* Apply **Otsu's Thresholding** to separate the foreground (nuclei) from the background. 

### 2. Standard Watershed (Without Markers)
* The watershed algorithm is applied directly to the image gradient or distance map without spatial constraints.
* **Result:** Severe over-segmentation due to image noise creating false local minima.

### 3. Marker-Controlled Watershed
* **Distance Transform:** Calculates the Euclidean distance from every foreground pixel to the nearest background pixel.
* **Peak Detection:** Finds the coordinates of the local maxima in the distance map. These represent the true centers of the individual nuclei.
* **Labeling:** Assigns a unique ID to each discovered peak (marker).
* **Watershed:** The algorithm floods the topographic surface starting *only* from the defined markers, preventing the formation of false boundaries and successfully splitting touching cells.

## 🚀 Setup and Installation
1. Clone the repository:
   ```bash
   git clone [https://github.com/](https://github.com/shubham-dube/DL_Project)
   cd DL_Project
   ```

2. Install dependencies:

```bash
pip install opencv-python numpy matplotlib scikit-image scipy kaggle
```
3. Ensure your kaggle.json API token is properly configured in your ~/.kaggle/ directory.

## 💻 Usage
Run the fully self-contained Jupyter Notebook:

```bash
jupyter notebook nuclei_separation_watershed.ipynb
```

## 📊 Results & Key Learnings
The standard watershed algorithm treats every microscopic intensity fluctuation as a separate catchment basin, shattering the nuclei into fragments. By calculating the Euclidean Distance Transform and extracting local peaks, we create definitive "seeds." The marker-controlled watershed then guarantees that only one segmented object is created per seed, perfectly slicing touching nuclei along their intersecting valleys.