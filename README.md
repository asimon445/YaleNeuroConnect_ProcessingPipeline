# YaleNeuroConnect_ProcessingPipeline

This repository contains the fMRI data processing pipeline utilized by the YaleNeuroConnect study. The shell scripts provided will only function properly if you have installed FSL, BioImage Suite, and SPM12, and added each of those softwares to your path. 


Below is the order in which you should run the scripts, a description of which preprocessing steps they accomplish, and a step by step guide on how to set them up and run them. 
1. convert_dicom_to_bids.csh -- converts your DICOM files to BIDS.
    Steps:
       a. Edit the script by typing "gedit convert_dicom_to_bids.csh" in your terminal
       b. Edit the dicom names of subjects you want to preprocess. Be sure to ensure that your input/output directories are correct! 
       c. Run it by typing "tcsh -c ./convert_dicom_to_bids.csh" in your terminal.

2. tar_zip.csh -- zips your original DICOM files to save space
   Steps:
       a. Edit the script by typing "gedit tar_zip.csh" in your terminal
       b. Edit the dicom names of subjects you want to preprocess. Be sure to ensure that your input/output directories are correct!
       c. Run it by typing "tcsh -c ./tar_zip.csh" in your terminal.
       d. After it has completed, you can rm -rf the original dicom file (but keep the tgz file!) from the input directory to save disk space (make sure this is done only after the file is completely tar zipped).
       ** Run this step after converting to bids since that requires an untarred file

3. strip_brain.csh -- runs skull stripping by calling on to FSL optimized brain extraction tool (optiBET) to skull strip the T1 weighted MPRAGE
    Steps:
       a. Edit the script by typing "strip_brain.csh" in your terminal
       b. Edit the dicom names of subjects you want to preprocess. Be sure to ensure that your input/output directories are correctly pointing to the directory where the T1 scans are located.
       c. Run it by typing "tcsh -c ./strip_brain.csh" in your terminal.
       ** Visual inspection should be performed to ensure that the skull stripping worked properly

4. batch_bids_unzip_motion_zip.csh

5. 

SPM12 was used for motion correction. 
Nonlinear registration of the MPRAGE to the MNI template was performed using BioImage Suite
Linear registration of the functional to the structural images was done through a combination of FSL and BioImage Suite. 

The remaining preprocessing steps were performed in BioImage Suite, including regression of mean time courses in white matter, cerebrospinal fluid, and grey matter; high-pass filtering to correct linear, quadratic, and cubic drift; regression of 24 motion parameters; and low-pass filtering (Gaussian filter, σ = 1.55)40. 


Functional connectivity: The Shen2681 atlas was applied to the preprocessed data, parcellating it into 268 functionally coherent nodes. The mean time courses of each node pair were correlated, and the correlation coefficients were Fisher transformed, generating eight (for the eight in-scanner runs) 268 × 268 connectivity matrices per subject.
