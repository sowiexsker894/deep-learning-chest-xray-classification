# Image Processing - Pneumonia Detection in Chest X-rays

## 📋 Course and Team Information
- **Course:** CC235 - Image Processing
- **Professor:** Luis Canaval Sánchez
- **Date:** May 2025

---

![Chest X-ray](imagen_2025-05-07_161158968.png)  
*Example of processed chest X-ray*

## 📌 Abstract

This report develops an open-source preprocessing pipeline for chest X-rays to improve visual quality and facilitate pneumonia detection. It employs the Chest X-Ray Images (Pneumonia) dataset from Kaggle, composed of approximately 5,856 grayscale images. Two complementary approaches are proposed:

### 🔬 Classical Approach
Applies Gaussian filter (optimized σ), 3×3 Median filter, histogram equalization, global threshold segmentation, and morphological operations to define the pulmonary region. On this ROI, intensity histograms, LBP descriptors, and statistics are extracted to feed a linear SVM classifier or logistic regression.

### 🧠 Deep Learning Approach
Uses DenseNet-121 pretrained on ImageNet, adapted with resizing to 224×224 px, data augmentation (rotations, flips, and brightness adjustments) and fine-tuning with Adam to generate a continuous pneumonia probability.

**Keywords:** image processing, chest X-rays, pneumonia, Gaussian filter, DenseNet-121.

---

## 📁 Project Structure

```
CC235-TP-TF-2025-1/
├── Source Code/
│   ├── Modeloclásico (1).ipynb          # Classical model implementation with SVM
│   └── ProcesamientoImagenesFinal_ModeloProfundo (1).ipynb  # DenseNet-121 model
├── Dataset/
│   └── chest_xray/                      # Complete chest X-ray dataset
│       ├── test/                        # Test set
│       ├── train/                       # Training set
│       └── val/                         # Validation set
├── imagenesreadme/
│   ├── imagen_2025-05-07_161158968.png  # Example image
│   └── NEUMONIA .png                    # Reference image
└── README.md                            # Project documentation
```

## 📚 Content

### 1. 📖 Introduction

Medical diagnosis through radiographic imaging constitutes a fundamental pillar in early detection of various pathologies. Among these, pneumonia stands out as one of the main causes of mortality, especially in developing countries (World Health Organization [WHO], 2023).

Chest X-rays present technical limitations such as Gaussian noise, low contrast, and artifacts that hinder the visualization of pulmonary tissues (Litjens et al., 2017). These failures can be eliminated with correct treatment and processing of each image.

### 2. 🎯 Objectives

- Develop an image preprocessing pipeline to improve visual quality of chest X-rays
- Combine classical processing techniques with deep neural networks
- Optimize noise reduction, edge enhancement, and contrast in images

### 3. ✳️ Course Achievement

**General Competency:** Information Management and Critical Thinking (Level 2)  
Analyze a complex computing problem and apply computing principles to identify solutions.

**Specific Competency:** ABET 5 - Multidisciplinary Teamwork (Level 1)  
Ability to work on multidisciplinary team projects, applying scientific principles to practical and innovative solutions.

### 4. 🗺️ Use Case Description

Pneumonia diagnosis through X-rays is affected by technical limitations. This project develops an open-source preprocessing tool that could be integrated into telemedicine platforms, democratizing access to accurate diagnoses in resource-limited contexts.

**Key Questions:**
1. Can our pipeline classify X-rays as normal/pneumonia with effective accuracy?
2. What is the probability of pneumonia given a filtered X-ray?
3. What is the sensitivity of our classifier after preprocessing?

### 5. 🌐 Dataset Description

**Name:** Chest X-Ray Images (Pneumonia)  
**Source:** [Kaggle](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia)  
**Size:** 5,856 images (1.24GB)  
**Format:** JPEG  
**Dataset Structure:**
```
Dataset/
└── chest_xray/
    ├── test/
    │   ├── NORMAL/          # 234 healthy lung images
    │   └── PNEUMONIA/       # 390 pneumonia images
    ├── train/
    │   ├── NORMAL/          # 1,341 healthy lung images
    │   └── PNEUMONIA/       # 3,875 pneumonia images
    └── val/
        ├── NORMAL/          # 8 healthy lung images
        └── PNEUMONIA/       # 8 pneumonia images
```

**Class Distribution:**
- **NORMAL:** 1,583 images (healthy lungs)
- **PNEUMONIA:** 4,273 images (bacterial and viral pneumonia)
- **Total:** 5,856 images

**Dataset Split:**
- **Train:** 5,216 images (89.1%)
- **Test:** 624 images (10.7%)
- **Validation:** 16 images (0.3%)

### 6. ▶️ Modeling

#### 6.1 Classical Model

**Preprocessing:**
1. Gaussian filter for noise reduction
2. 3×3 Median filter to eliminate "salt and pepper noise"
3. Global thresholding for segmentation
4. Morphological operations for refinement

**Classification:** Linear SVM or Logistic Regression

#### 6.2 Deep Learning Model

**Architecture:** Pretrained DenseNet-121  
**Preprocessing:**
- Resizing to 224×224 px
- Data augmentation (rotations, flips, brightness adjustments)
- ImageNet normalization

**Training:**
- Fine-tuning with Adam (lr=1×10⁻⁴)
- Binary cross-entropy as loss function
- 20 epochs with batch size 16

#### 6.3 Answering the Questions

1. **Accuracy:** Calculated using confusion matrix (TP+TN)/Total
2. **Probability:** predict_proba() for classical model, sigmoid output for DenseNet
3. **Sensitivity:** TP/(TP+FN) from confusion matrix

### 7. 📊 Results Publication

#### 7.1 Classical Model

This section details the results obtained from implementing the first approach for classifying chest X-rays as "NORMAL" or "PNEUMONIA". Two traditional classification models were evaluated: linear Support Vector Machine (SVM) and Logistic Regression, after a rigorous preprocessing and feature extraction process.

**Evaluation Metrics:**
- **Accuracy:** Proportion of correct predictions over total
- **Precision:** Of all instances predicted as positive, how many were actually positive
- **Sensitivity (Recall):** Of all actually positive instances, how many were correctly identified
- **F1-Score:** Harmonic mean of precision and sensitivity
- **Area Under ROC Curve (AUC-ROC):** Model's ability to distinguish between classes
- **Confusion Matrix:** Detailed table of true positives, negatives, false positives and negatives

**Results:**
The SVM model obtained marginally superior performance in most key metrics for pneumonia detection, achieving 69% precision compared to 68% for logistic regression.

#### 7.2 Deep Learning Model

In this second approach, a deep learning model based on DenseNet-121 architecture was implemented, using transfer learning technique. To combat the bias observed in classical models, a class weight strategy was applied in the loss function, penalizing PNEUMONIA classification errors more heavily.

The model was trained for 30 epochs, demonstrating stable learning and significant performance improvement. Final evaluation was performed on the same test set of 624 images for direct and fair comparison.

**Outstanding Results:**
- **Overall Performance:** 86.5% accuracy and 0.9377 AUC-ROC
- **Pneumonia Detection:** 87.2% sensitivity for PNEUMONIA class
- **Reliability:** 90.9% precision for PNEUMONIA with 0.89 F1-Score

#### 7.3 Our Models' Response to the Questions

**Can our pipeline classify a chest X-ray as normal or pneumonia with effective accuracy?**

- **Classical Model:** SVM model achieved 69% overall accuracy
- **Deep Learning Model:** DenseNet-121 model achieved 86.5% overall accuracy

**What is the probability that a patient has pneumonia given their filtered X-ray?**

- **Classical Model:** 0.55 AUC-ROC, indicating limited discrimination capability
- **Deep Learning Model:** 0.9377 AUC-ROC, demonstrating outstanding capability

**What is the sensitivity of our normal or pneumonia classifier after applying preprocessing?**

- **Classical Model:** 100% sensitivity but with high false positive rate
- **Deep Learning Model:** 87.2% sensitivity with excellent balance

### 8. ⚜️ Conclusions

The study demonstrated that while traditional techniques offer a classification baseline, deep learning models provide a significantly more robust and accurate solution for pneumonia detection. The DenseNet-121 model conclusively outperformed the classical model (SVM), increasing overall accuracy from 69% to 86.5%.

More importantly, the sensitivity for detecting pneumonia cases —the most critical metric in a clinical context— jumped from a modest level to an excellent 87.2%, demonstrating the clear superiority of the deep learning approach for this task.

The implementation of this solution was carried out using open-source tools and in a Google Colab environment that simulates accessible resource conditions. The high performance and reliability of the final DenseNet-121 model, with an AUC-ROC of 0.9377, validates its great potential to be integrated into real telemedicine platforms.

The comparative analysis of the models did not show complementary performance, but rather revealed a better proposal. The DenseNet-121 model, after being optimized with class weights to correct data bias, consolidated as the definitive tool. Its ability to correctly identify 87.2% of patients with pneumonia, while maintaining high precision of 90.9%, positions it as a powerful support system for medical staff, capable of streamlining pre-diagnosis and improving care in clinical environments.

### 9. 🔆 Bibliographic References

1. Mooney, P. (2018). Chest X-Ray Images (Pneumonia). Kaggle. https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia
2. Litjens, G., et al. (2017). A survey on deep learning in medical image analysis. Medical Image Analysis, 42, 60–88. https://doi.org/10.1016/j.media.2017.07.005
3. World Health Organization. (2023). Pneumonia. https://www.who.int/es/news-room/fact-sheets/detail/pneumonia
