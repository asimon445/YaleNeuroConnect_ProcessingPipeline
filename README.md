# YaleNeuroConnect_ProcessingPipeline

This repository contains the fMRI data processing pipeline utilized by the YaleNeuroConnect study. The shell scripts provided will only function properly if you have installed FSL, BioImage Suite, and SPM12, and added each of those softwares to your path. 


Below are the preprocessing steps, and the order in which you should run the scripts:
1. Convert DICOM to BIDS
Skull stripping of the structural scans was done using optiBET (FSL)
SPM12 was used for motion correction. 
Nonlinear registration of the MPRAGE to the MNI template was performed using BioImage Suite
Linear registration of the functional to the structural images was done through a combination of FSL and BioImage Suite. 

The remaining preprocessing steps were performed in BioImage Suite, including regression of mean time courses in white matter, cerebrospinal fluid, and grey matter; high-pass filtering to correct linear, quadratic, and cubic drift; regression of 24 motion parameters; and low-pass filtering (Gaussian filter, σ = 1.55)40. 


Functional connectivity: The Shen2681 atlas was applied to the preprocessed data, parcellating it into 268 functionally coherent nodes. The mean time courses of each node pair were correlated, and the correlation coefficients were Fisher transformed, generating eight (for the eight in-scanner runs) 268 × 268 connectivity matrices per subject.
![image](https://github.com/user-attachments/assets/659f6451-ff09-4694-8cff-b671f42220e8)
