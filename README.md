# Multimodal_biometric_verification_dev
Development notebook of multimodal biometric system. Its goal is to verify and allow access to users based on their face picture, signature registration and wrist movement registration. Notebook contains tests of different feature extraction approaches (using both traditionally extracted features and pretrained CNN architectures from tensorflow), dimensionality reduction using both PCA transformation and polynomial approximation supported by gradient descent procedure, tests of different classifiers (KNN, SVM, Naive Bayes). 

## Hardware
- WACOM Intuos Pro M Tablet
- STEVAL-WESU1 bracelet
- laptop webcam
![image](https://user-images.githubusercontent.com/64041095/182466946-dae46c05-3dc1-42b9-9b19-2a1b4629778e.png)

## Dataset
Dataset was created by the author and his friends and contained only 90 samples (90 * (face picture + signature registration + wrist movement registration)) belonging to 6 users. At first, data aquisition was performed on 22 users and resulted in aquiring over 300 samples, but STEVAL-WESU1 unstable bluetooth connection caused problems in most wrist movement registration cases, that's why, after solving problems, aquisition was repeated on smaller scale.

## Feature extraction
### Face
Three approaches to face features extraction have been tested:
1. Simple image rows concatenation + PCA dimensionality reduction 
2. Feature extraction with MobileNetV2 net pretrained on imagenet + PCA dimensionality reduction
3. Feature extraction with VGG16 net pretrained on imagenet + PCA dimensionality reduction
Isolated tests of classifiers trained on face pictures showed that VGG16 achieves the best results, in consequence it was selected to be used in further development. It is worth to highlight, that traditional concatenation + PCA approach visibly underperformed.
### Signature
Set of traditionaly extracted 13 features was used (including e.g. mean stroke length or mean stroke duration) and it's dimensionality was also reduced by PCA.
### Wrist
Two approaches for feature extraction have been tested. First approach using MFCC coefficients and spectral centroid of XYZ gyroscope signals visibly underperformed (f1-score of classification about 0.233 suggested that algorithm was almost guessing). Second approach, using more straightforward parametrisation methods (RMS and Zero-crossing rate), improved the results - f1-score reached 0.653, which still wasn't an outstanding result, although it could be blamed on low repeatability of wrist movement during signing (a behavioral biometric).

