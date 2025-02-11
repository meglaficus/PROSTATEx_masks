## Description

Lesion masks for the [PROSTATEx](https://wiki.cancerimagingarchive.net/display/Public/SPIE-AAPM-NCI+PROSTATEx+Challenges) prostate MRI dataset.
It comprises prostate MRI exams with PI-RADS score = 2+ lesions. These are classified as clinically significant or not. Only patients with PI-RADS score = 3+ lesions underwent biopsy and are collected in the PROSTATEx 2 dataset, together with the resulting bioptic lesion Gleason Grade.

The original dataset only provided lesion coordinates and an accompanying screenshot for each finding, with several issues due to misplaced coordinates or not clearly identifiable PI-RADS score = 2 lesions. This repository contains the result of a lesion-by-lesion quality check conducted at the [Department of Advanced Biomedical Sciences](http://www.dises.unina.it/en_GB/web/guest/-/768572-dipartimento-di-scienze-biomediche-avanzate) of the [University of Naples "Federico II"](http://www.unina.it/), in the form of lesion masks on axial T2-weighted and ADC images for all correctly identifiable findings in the PROSTATEx/PROSTATEx2 training dataset. As the ground truth was not available for the test sets, the same quality check was not performed on that data.

We encourage the use of this data for radiomics and machine learning investigations in magnetic resonance imaging for prostate cancer, appropriately referencing the repository. Quality checks on the provided masks or other improvements are also welcome as pull requests to the repository.

## Files

### Lesion masks

The files are in compressed NIFTI (.nii.gz) format and collected in separate folders for T2 and ADC images (n = 299 lesions) within the "Files/lesions/Masks/" directory. Each filename contains the following information (separated by underscores):

- "PROSTATEx Patient ID" + "Finding ID" + "Sequence name" + "ROI"

As sometimes multiple axial ADC/T2 image sequences are available for a patient, the repository also includes a list in CSV format containing the correct images for each mask. The list is structured as follows (separated by underscores):

- "PROSTATEx Patient ID" + "Sequence name" + "Sequence number"

The sequence number corresponds to the number at the beginning of the PROSTATEx dataset DICOM image folders for each patient.

Finally, the "PROSTATEx_classes.csv" file contains the ground truths for all lesions included in the dataset, obtained from the orignial PROSTATEx and PROSTATEx2 data. This file is structured as follows (separated by underscores):
- ID column = "PROSTATEx Patient ID" + "Finding ID"
- Clinically Significant column (i.e. Gleason Score > 3+3, Gleason Grade Group/ISUP score > 1) = "True"/"False"
- Gleason Grade Group/ISUP score column = "No Biopsy" or 1-5

Patients who were classified as PI-RADS score = 2 did not undergo biopsy and their lesions are always assumed to be not clinically significant.

Full exam DICOM files are retrievable through the Cancer Imaging Archive at: [https://wiki.cancerimagingarchive.net/display/Public/SPIE-AAPM-NCI+PROSTATEx+Challenges](https://wiki.cancerimagingarchive.net/display/Public/SPIE-AAPM-NCI+PROSTATEx+Challenges)

The **masks are to be used exclusively after conversion of the DICOM files in NIFTI using [dcm2niix](https://github.com/rordenlab/dcm2niix)**.
There is  a known [issue](https://github.com/rcuocolo/PROSTATEx_masks/issues/9) preventing the correct transposition of the annotations to the original DICOM files.

The NIFTI files for ADC and axial T2 volumes employed in the segmentation process are also available in the repository within the "Files/lesions/Images/" directory.

### Original coordinate markers

These 3x3 masks are centered on the original lesion coordinates provided in the PROSTATEx dataset and were employed for the quality control assessment and as the basis for successive whole-lesion segmentation. For the sake of transparency, they are also included in the dataset in the same format as the lesion masks in the "Original_coordinate_markers" folder. This file set includes lesion markers for all axial T2 and ADC images included for each patient.

### Prostate and zonal anatomy masks

The files are in compressed NIFTI (.nii.gz) format within the "Files/prostate/" directory. All segmentations have been performed on axial T2 images (n = 204 exams). Each filename contains the following information (separated by underscores):

- "PROSTATEx Patient ID"

The masks included in the "mask_prostate" directory represent whole-gland masks (binarized). Those included in "mask_pz" and "mask_tz" are limited respectively to the peripheral and rest (transition zone, central zone, anterior stroma) of the gland, also binarized. The background always has a value of 0. All segmentations were performed manually and the masks underwent an automated cluster cleaning to remove eventual imperfections.

As sometimes multiple axial T2 image sequences are available for a patient, the repository also includes a list in CSV format containing the correct images for each mask. The list is structured as follows (separated by underscores):

- "PROSTATEx Patient ID" + "Sequence name" + "Sequence number"

The sequence number corresponds to the number at the beginning of the PROSTATEx dataset DICOM image folders for each patient.

Full exam DICOM files are retrievable through the Cancer Imaging Archive at: [https://wiki.cancerimagingarchive.net/display/Public/SPIE-AAPM-NCI+PROSTATEx+Challenges](https://wiki.cancerimagingarchive.net/display/Public/SPIE-AAPM-NCI+PROSTATEx+Challenges)

The **masks are to be used exclusively after conversion of the DICOM files in NIFTI using [dcm2niix](https://github.com/rordenlab/dcm2niix)**.
There is  a known [issue](https://github.com/rcuocolo/PROSTATEx_masks/issues/9) preventing the correct transposition of the annotations to the original DICOM files.

The NIFTI files for the axial T2 volumes employed in the segmentation process are also available in the repository within the "Files/prostate/Images/" directory.

## Citation

### For the annotations

- R. Cuocolo, A. Stanzione, A. Castaldo, D.R. De Lucia, M. Imbriaco, Quality control and whole-gland, zonal and lesion annotations for the PROSTATEx challenge public dataset, Eur. J. Radiol. (2021) 109647. https://doi.org/10.1016/j.ejrad.2021.109647
-  Cuocolo R, Comelli A, Stefano A, et al (2021) Deep Learning Whole‐Gland and Zonal Prostate Segmentation on a Public MRI Dataset. J Magn Reson Imaging. https://doi.org/10.1002/jmri.27585

### For the PROSTATEx dataset

- Geert Litjens, Oscar Debats, Jelle Barentsz, Nico Karssemeijer, and Henkjan Huisman. "ProstateX Challenge data", The Cancer Imaging Archive (2017). DOI: 10.7937/K9TCIA.2017.MURS5CL
- Litjens G, Debats O, Barentsz J, Karssemeijer N, Huisman H. "Computer-aided detection of prostate cancer in MRI", IEEE Transactions on Medical Imaging 2014;33:1083-1092. DOI: 10.1109/TMI.2014.2303821
- Clark K, Vendt B, Smith K, Freymann J, Kirby J, Koppel P, Moore S, Phillips S, Maffitt D, Pringle M, Tarbox L, Prior F. The Cancer Imaging Archive (TCIA): Maintaining and Operating a Public Information Repository, Journal of Digital Imaging, Volume 26, Number 6, December, 2013, pp 1045-1057. DOI: 10.1007/s10278-013-9622-7

## License

Creative Commons Attribution 4.0 International (CC-BY-4.0). See "LICENSE" file for full details.
