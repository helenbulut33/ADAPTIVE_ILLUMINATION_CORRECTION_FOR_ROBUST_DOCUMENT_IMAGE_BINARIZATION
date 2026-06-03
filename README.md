# 🖨️ Adaptive Illumination Correction for Robust Document Image Binarization

## 📖 About the Project
Document image binarization is a fundamental preprocessing step in document analysis and optical character recognition (OCR) systems. While global thresholding techniques perform well on clean scanned documents, they often fail on camera-captured documents suffering from uneven illumination, shadows, page curvature, and reflections.

This project proposes a robust, lightweight binarization pipeline designed to explicitly model and correct illumination variations before applying adaptive thresholding. By combining morphological background estimation with Contrast Limited Adaptive Histogram Equalization (CLAHE), this method achieves competitive accuracy with lower computational overhead compared to heavier alternatives like Retinex or polynomial surface fitting.

## 🚀 The Proposed Pipeline
The method separates global illumination normalization from per-region local contrast enhancement through the following steps:

* **Grayscale Conversion:** Converting the input document to a single-channel image.
* **Background Estimation:** Using morphological opening with large structuring elements to capture the illumination trend without losing text structures.
* **Illumination Normalization:** Dividing the original grayscale image by the estimated background surface.
* **Local Contrast Enhancement (CLAHE):** Applying region-based contrast enhancement (e.g., 8x8 contextual tiles) to amplify text-to-background contrast while limiting noise.
* **Adaptive Thresholding:** Extracting the final binary image from the normalized output.
* **Post-Processing:** Applying morphological operations to remove residual noise.

## 🔬 Baseline Comparisons
The proposed method is benchmarked against classical binarization techniques:
* **Otsu Thresholding:** A global thresholding technique maximizing between-class variance.
* **Sauvola Adaptive Thresholding:** A local thresholding method adapting to local mean and variance.

## 📊 Datasets & Evaluation
The system is evaluated on both controlled benchmarks and real-world scenarios:
* **DIBCO Dataset:** Publicly available Document Image Binarization Contest images with ground-truth masks.
* **Custom Smartphone Dataset:** Images captured under various real-world lighting conditions (shadows, glare, uneven lighting).

**Performance Metrics:**
* **Pixel-Level:** Precision, Recall, and F-measure (compared against ground-truth masks).
* **OCR-Level:** Character and word recognition accuracy evaluated using **Tesseract OCR**.
* **Computational:** Processing time per image to ensure viability for mobile scanning.

## 🛠️ Built With
* Python 3
* OpenCV
* scikit-image
* Tesseract OCR
