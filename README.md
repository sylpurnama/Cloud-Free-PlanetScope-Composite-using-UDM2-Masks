# PlanetScope Image Masking with UDM2 in Google Earth Engine

This repository contains a Google Earth Engine (GEE) script to **mask 4 PlanetScope images** using their corresponding **UDM2 quality masks** and generate a clean, cloud-free composite image.

## 📌 Overview

PlanetScope imagery often comes with **UDM2 (Unusable Data Mask)** files that indicate which pixels are usable. This script filters out unwanted pixels (e.g., clouds, haze, or noise) by applying UDM2 masks and then composites the result.

## 🧾 Script Features

- Loads 4 PlanetScope images and 4 associated UDM2 files
- Masks out all non-clear pixels (`b1 != 1`) using UDM2
- Combines the masked images into a single composite (via `.median()`)
- Displays the result on the map in RGB
- Exports the final composite as a GeoTIFF to Google Drive

## 🧪 How It Works

1. **Load Image and UDM2 Assets**

   Each PlanetScope image is paired with its UDM2 file:
   ```js
   {
     image: ee.Image('path/to/image'),
     udm: ee.Image('path/to/udm2')
   }

   var clearMask = udm.select('b1').eq(1);
   image.updateMask(clearMask);

   var composite = imageCollection.median();

   Map.addLayer(composite, {bands: ['b3', 'b2', 'b1'], ...});

   Export.image.toDrive({...});

   

## ▶️ How to Run
Go to Google Earth Engine Code Editor

Paste the script from main.js

Modify asset paths (ee.Image('projects/...')) if needed

Click Run to visualize and export


### 🌈 Image Before Masking  
The original PlanetScope image, before applying the UDM2 cloud mask. Cloudy and hazy areas are still visible.  
![False Color Composite](https://github.com/sylpurnama/Cloud-Free-PlanetScope-Composite-using-UDM2-Masks/blob/main/img%20before.png)

### 🗺️ Image After Masking (Cloud-Free Composite)  
The final composite image after applying UDM2 masks to remove clouds and unusable pixels.  
![LULC Classification](https://github.com/sylpurnama/Cloud-Free-PlanetScope-Composite-using-UDM2-Masks/blob/main/img%20after.png)


## 📂 Output
A cloud-free RGB composite image from 4 masked PlanetScope scenes

Exported as a GeoTIFF at 3-meter resolution


## 📋 Notes
Make sure you have access to the PlanetScope image and UDM2 assets in your GEE account.

UDM2 files must include a b1 band indicating clear pixels (1 = clear).


## 📜 License
This project is licensed under the MIT License. See LICENSE for details.
