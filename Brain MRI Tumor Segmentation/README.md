# Brain MRI Tumor Segmentation

A comparative study of **Global Otsu Thresholding** and **Sauvola Adaptive Thresholding** methods for brain MRI tumor segmentation.

## 📋 Project Overview

This project implements and compares two classical image segmentation techniques for detecting brain tumors in MRI scans:

1. **Global Otsu Thresholding** - A global thresholding method that finds the optimal threshold by minimizing intra-class variance
2. **Sauvola Adaptive Thresholding** - A local adaptive thresholding method that computes thresholds based on local statistics

## ✨ Features

- **Two Segmentation Methods**: Implementation of Otsu and Sauvola thresholding algorithms
- **Quantitative Evaluation**: Dice Coefficient and Jaccard Index metrics
- **Comprehensive Visualization**: Side-by-side comparisons with overlay visualizations
- **Batch Processing**: Evaluate multiple MRI samples automatically
- **Statistical Analysis**: Mean, standard deviation, and per-sample performance tracking
- **Google Colab Support**: Ready-to-use notebook for cloud execution

## 📁 Repository Structure

```
DLMI Assignment/
├── tumor_segmentation_comparison.ipynb          # Detailed comparison notebook
├── brain_mri_dataset/                           # Dataset directory
│   ├── images/                                  # MRI images
│   └── masks/                                   # Ground truth masks
└── README.md                                    # This file
```

## 🔧 Requirements

### Python Packages

```
numpy
matplotlib
opencv-python (cv2)
scikit-image
pandas
```

### Installation

**For Local Environment:**
```bash
pip install numpy matplotlib opencv-python scikit-image pandas
```

**For Google Colab:**
```bash
pip install scikit-image
```
*(Other packages are pre-installed in Colab)*

## 📊 Dataset

This project uses the **Brain Tumor Segmentation** dataset from Kaggle.

### Dataset Download

#### Option 1: Kaggle API (Recommended)

1. Install Kaggle API:
   ```bash
   pip install kaggle
   ```

2. Get your Kaggle credentials:
   - Visit https://www.kaggle.com/account
   - Click "Create New API Token" under the API section
   - Download `kaggle.json`

3. Place `kaggle.json`:
   - **Windows**: `C:\Users\<YourUsername>\.kaggle\kaggle.json`
   - **Linux/Mac**: `~/.kaggle/kaggle.json`

4. Download dataset:
   ```bash
   kaggle datasets download -d nikhilroxtomar/brain-tumor-segmentation
   ```

#### Option 2: Manual Download

- Download from: https://www.kaggle.com/datasets/nikhilroxtomar/brain-tumor-segmentation
- Extract to `./brain_mri_dataset/` folder

### Dataset Structure

The dataset should be organized as:
```
brain_mri_dataset/
├── images/
│   ├── image1.tif
│   ├── image2.tif
│   └── ...
└── masks/
    ├── image1.tif
    ├── image2.tif
    └── ...
```

## 🚀 Usage

### Local Jupyter Notebook

1. Clone or download this repository
2. Download the dataset (see Dataset section)
3. Open `tumor_segmentation_comparison.ipynb` or `Brain_MRI_Tumor_Segmentation.ipynb`
4. Update `DATASET_PATH` if needed
5. Run all cells

### Quick Start Example

```python
# Load a single MRI image and its mask
image, mask = mri_data[0]

# Compare segmentation methods
results = compare_methods(image, mask, visualize=True)

# View metrics
print(f"Otsu Dice: {results['otsu_dice']:.4f}")
print(f"Sauvola Dice: {results['sauvola_dice']:.4f}")
```

## 📈 Evaluation Metrics

### Dice Coefficient
Measures overlap between predicted and ground truth masks:

$$\text{Dice} = \frac{2 \times |X \cap Y|}{|X| + |Y|}$$

### Jaccard Index (IoU)
Measures intersection over union:

$$\text{Jaccard} = \frac{|X \cap Y|}{|X \cup Y|}$$

Both metrics range from 0 (no overlap) to 1 (perfect overlap).

## 🔬 Methods

### Global Otsu Thresholding

- **Principle**: Finds optimal global threshold by minimizing intra-class variance
- **Advantages**: 
  - Fast and simple
  - No parameter tuning required
  - Works well with bimodal intensity distributions
- **Disadvantages**: 
  - Single threshold for entire image
  - Sensitive to illumination variations
  - Struggles with weak contrast

### Sauvola Adaptive Thresholding

- **Principle**: Computes local threshold based on mean and standard deviation in a window
- **Formula**: $T(x,y) = \mu(x,y) \times [1 + k \times (\sigma(x,y)/R - 1)]$
- **Advantages**: 
  - Adapts to local intensity variations
  - Better handling of non-uniform illumination
  - Robust to local contrast variations
- **Disadvantages**: 
  - More computationally expensive
  - Requires parameter tuning (window_size, k)
  - May introduce noise in uniform regions

## 📊 Results

The notebooks generate:

1. **Visual Comparisons**: Side-by-side segmentation results
2. **Overlay Visualization**: RGB overlay showing ground truth (Red), Otsu (Green), Sauvola (Blue)
3. **Performance Charts**: Bar charts comparing Dice and Jaccard scores
4. **Per-Sample Analysis**: Line plots showing performance across all samples
5. **Statistical Summary**: Mean ± standard deviation for all metrics
6. **Detailed DataFrame**: Complete results table with per-sample scores

### Sample Output

```
OVERALL PERFORMANCE SUMMARY
======================================================================
Number of samples evaluated: 110

GLOBAL OTSU THRESHOLDING
----------------------------------------------------------------------
  Average Dice Coefficient: 0.XXXX ± 0.XXXX
  Average Jaccard Index:    0.XXXX ± 0.XXXX

SAUVOLA ADAPTIVE THRESHOLDING
----------------------------------------------------------------------
  Average Dice Coefficient: 0.XXXX ± 0.XXXX
  Average Jaccard Index:    0.XXXX ± 0.XXXX
```

## 🎯 Key Insights

- Both methods have distinct strengths for different image characteristics
- Otsu excels in speed and simplicity for bimodal distributions
- Sauvola provides better adaptation to local variations
- Proper preprocessing (normalization, morphological operations) is crucial
- Choice of method depends on specific application requirements

## 📝 Notebooks Description

### 1. Brain_MRI_Tumor_Segmentation.ipynb
Main implementation notebook with core segmentation algorithms.

### 2. tumor_segmentation_comparison.ipynb
Comprehensive comparison with detailed analysis, batch processing, and statistical evaluation.

## 🤝 Contributing

Feel free to fork this repository and submit pull requests for:
- Additional segmentation methods
- Performance optimizations
- Enhanced visualizations
- Bug fixes

## 📄 License

This project is open-source and available for educational and research purposes.

## 📧 Contact

For questions or feedback, please open an issue in this repository.

## 🙏 Acknowledgments

- Dataset: [Brain Tumor Segmentation](https://www.kaggle.com/datasets/nikhilroxtomar/brain-tumor-segmentation) by Nikhil Tomar
- Libraries: NumPy, scikit-image, Matplotlib, OpenCV, Pandas

---

**Note**: This project is for educational and research purposes in the field of medical image processing and computer vision.
