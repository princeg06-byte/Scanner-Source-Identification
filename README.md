# Scanner Source Identification Using Sensor Pattern Noise 🖨️🔍

Identify the hardware scanner used to digitize an image by analyzing its microscopic hardware fingerprint: **Sensor Pattern Noise (SPN)**. This project extracts noise patterns from high-resolution TIFF images, processes them into a 16-dimensional statistical feature vector, and trains an SVM classifier to identify the source scanner with high accuracy.

## 🌟 Key Highlights

* **High Accuracy:** Achieves **88.44%** accuracy in distinguishing between scanner classes.
* **Hardware-Level Precision:** Successfully differentiates between two physically identical scanner models (HP Scanjet 6300c) based purely on sensor imperfections.
* **Robust Feature Engineering:** Utilizes Wavelet Transforms for denoising and condenses complex 2D noise patterns into a highly efficient 16-dimensional statistical vector.

## 📊 Dataset & Pipeline Overview

The pipeline processes massive, high-resolution TIFF images through a strict methodology:

1. **Patch Extraction:** Avoids memory overload by extracting non-overlapping **1024×768 pixel patches** from the source images.
2. **The Dataset:** Uses 160 images (1200 DPI) across **4 specific scanner classes**, yielding exactly **24,270 distinct patches**.
3. **Data Splitting:** Employs a group-aware split (70% train / 30% test) to prevent data leakage.
4. **Denoising:** Applies a Discrete Wavelet Transform (`db8` wavelet, level 4) to separate the image content from the underlying sensor noise.
5. **Classification:** Evaluated against 1D and 2D correlation baselines before optimizing a **Support Vector Machine (SVM)** to achieve the final accuracy.

## ⚙️ Installation & Setup

1. **Clone the repository:**
```bash
git clone https://github.com/yourusername/scanner-source-identification.git
cd scanner-source-identification

```


2. **Install dependencies:**
The project relies on standard image processing and machine learning libraries.
```bash
pip install opencv-python numpy scipy matplotlib scikit-learn pywavelets pandas pillow seaborn

```


3. **Directory Structure:**
Ensure your dataset is placed correctly relative to the notebook. The code expects the dataset one directory above:
```text
project_root/
├── datasets/
│   └── scanner_dataset/
└── src/
    └── code_notebook.ipynb

```



## 🚀 Usage

Open the Jupyter Notebook and run the cells sequentially:

```bash
jupyter notebook

```

**⚠️ Important Runtime Note:** Because the source images are extremely large, the code explicitly bypasses the default pixel limit. Do not remove the following line from the notebook, or the TIFF files will fail to load:

```python
Image.MAX_IMAGE_PIXELS = None

```

## 📈 Results

* **2D Correlation Baseline:** 67.19%
* **1D Correlation Baseline:** 70.31%
* **SVM Classifier (Final):** **88.44%**

The final output generates a confusion matrix confirming strong diagonal clustering, proving the model successfully maps extracted feature vectors back to the exact physical scanner.

---

*Maintained by Prince*
