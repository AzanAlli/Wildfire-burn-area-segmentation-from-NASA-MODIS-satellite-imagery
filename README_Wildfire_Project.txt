
# Wildfire Burn Area Mapping Project

## Overview
This project applies a Convolutional Neural Network (CNN) model (U-Net) to detect wildfire burn areas from MODIS satellite imagery. The goal is to preprocess satellite data, generate binary burn masks, and train a segmentation model.

## Table of Contents
1. Dataset Collection
2. Preprocessing
   - Burn Mask Extraction
   - Pre-burn RGB Image Extraction
   - Visualisation of Outputs
3. Tiling Images and Masks
4. Train/Val/Test Splitting
5. Model Training (U-Net)

## Dataset Collection

- MODIS MCD64A1 (Burned Area) dataset downloaded from NASA Earthdata Search
- MODIS MOD09GA (Surface Reflectance) dataset downloaded for pre-burn imagery.
- Files are saved in Google Drive for us but we have provided the folders for you - you will have to open the 3 zip folders provided and add the folders into the Google Drive for data access:
  - Burn data: /content/drive/MyDrive/WildfireProject raw_hdf
  - Preburn data: /content/drive/MyDrive/WildfireProject preburn_hdf

## Preprocessing

### Burn Mask Extraction from MODIS MCD64A1 HDF Files

- Extracted the Burn Date band from .hdf files.
- Created binary burn masks where burned = 1 and unburned = 0.
- Saved output masks as .tif files into:
  - /content/drive/MyDrive/WildfireProject/tifs

### Visualising Burn Mask GeoTIFF

- Used matplotlib and rasterio to plot the generated burn masks for quick inspection.

### Preburn RGB Image Extraction from MOD09GA

- Extracted Red (Band 1), Green (Band 4), and Blue (Band 3) bands.
- Stacked into true-colour RGB composites.
- Saved output images as .tif into:
  - /content/drive/MyDrive/WildfireProject/preburn_tifs

### Visualising RGB Images

- Displayed RGB satellite images using matplotlib.

## Tiling Images and Masks

### Tiling Burn Mask and Pre-Burn Imagery into 256×256 Patches

- Defined create_tiles() function to slice large .tif images and corresponding masks into 256x256 patches.
- Temporary tiles were saved into:
  - /content/drive/MyDrive/WildfireProject/temp_tiles/images
  - /content/drive/MyDrive/WildfireProject/temp_tiles/masks

## Train/Val/Test Splitting

### Dataset Split and Organisation

- Split all tiles into:
  - 70% Train, 15% Validation, 15% Test
- Organised into final directories:
  - /content/drive/MyDrive/WildfireProject/new_tiles/train/images
  - /content/drive/MyDrive/WildfireProject/new_tiles/train/masks
  - /content/drive/MyDrive/WildfireProject/new_tiles/val/images
  - /content/drive/MyDrive/WildfireProject/new_tiles/val/masks
  - /content/drive/MyDrive/WildfireProject/new_tiles/test/images
  - /content/drive/MyDrive/WildfireProject/new_tiles/test/masks

## Model Training (U-Net)

- Implemented a simple U-Net model in PyTorch.
- Setup:
  - Input: 3-channel RGB images.
  - Output: 1-channel binary burn masks.
- Loss Function: Binary Cross Entropy Loss (BCE)
- Optimiser: Adam
- Trained over 10 epochs.
- Used tqdm for progress bars.

## Notes on Troubleshooting

- Spaces in Folder Paths:
  - Paths like WildfireProject raw_hdf and WildfireProject preburn_hdf contained spaces.
  - Always wrap file paths in quotes and ensure the path is written exactly.

- Module Installation:
  - Had to install missing Python libraries:
    !apt-get install -y gdal-bin python3-gdal
    !pip install rasterio

- Google Drive Mount Issues:
  - Used force_remount=True in Colab if mounting errors appeared.

- Missing Bands:
  - Some burn .hdf files didn't have RGB bands (expected).
  - Only MOD09GA files were used for RGB pre-burn extraction.

---

# End of README

Prepared for Wildfire Burn Mapping Group Project
