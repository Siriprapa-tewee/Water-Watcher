# Water Watcher: AI-Based Riverbank Monitoring and Encroachment Detection

**Water Watcher** is a geospatial AI project that combines satellite remote sensing, Google Earth Engine, and machine learning to monitor changes in river areas and identify potential riverbank encroachment.

The project focuses on the Ping River in Mueang Chiang Mai, Thailand, and explores how satellite imagery can support environmental monitoring and river management.

**1st Place — GEO AI Hackathon, Super AI Engineer Season 6 (2026)**

## Project Overview

Changes in river channels and riverbank land use can result from natural processes, sediment deposition, and human activities. Monitoring these changes through field surveys alone can require substantial time and resources.

Water Watcher uses satellite imagery and geospatial analysis to compare river areas across multiple years, identify potential changes, and classify land-cover types in selected areas using a Random Forest model.

The system is a research prototype intended to support further investigation, rather than replace field verification.

## Objectives

- Monitor changes in river areas using satellite imagery from different years.
- Identify areas where the water surface has changed relative to a baseline year.
- Apply machine learning to classify land-cover types in selected areas.
- Generate geospatial outputs to support environmental monitoring and decision-making.

## Data Sources

- **Study area:** Ping River, Mueang Chiang Mai, Thailand.
- **Satellite imagery:** Sentinel-2 Surface Reflectance Harmonized (`COPERNICUS/S2_SR_HARMONIZED`).
- **Processing platform:** Google Earth Engine.
- **Reference datasets:** Dynamic World and ESA WorldCover.
- **Baseline year:** 2016.
- **Analysis period:** 2017–2026, using selected dry-season imagery from November to February.

The notebook filters satellite imagery by cloud coverage and applies cloud masking during image preprocessing.

## Methodology

### 1. Satellite Data Processing
- Retrieve Sentinel-2 imagery through Google Earth Engine.
- Apply cloud masking and generate composite imagery.
- Prepare water masks for comparing river areas across years.

### 2. River Area Change Analysis
- Use the Normalized Difference Water Index (NDWI) to generate water masks.
- Compare water areas against the 2016 baseline.
- Calculate changes in water-surface area and summarize the results by year.

### 3. Feature Engineering
Prepare spectral bands and indices for land-cover classification, including:

- Red, Green, Blue, and Near-Infrared (NIR)
- Normalized Difference Vegetation Index (NDVI)
- Normalized Difference Built-up Index (NDBI)
- Normalized Difference Water Index (NDWI)
- Brightness Index

### 4. Random Forest Classification
Train a Random Forest classifier to classify selected land-cover samples into four categories:

- **Vegetation**
- **Soil**
- **Building**
- **Pavement**

The notebook uses a train-test split and evaluates the model with classification metrics and a confusion matrix. It also includes stratified five-fold cross-validation.

### 5. Geospatial Visualization
The notebook includes workflows for visualizing river-area changes and land-cover classification results, with additional code for geospatial outputs and a prototype interface.

## Results

### Model Performance

The Random Forest model achieved the following results on the recorded test set:

| Metric | Result |
|---|---:|
| Test samples | 2,269 |
| Overall Accuracy | 88.54% |
| Macro F1-score (5-fold cross-validation) | 0.676 ± 0.005 |

### Classification Performance by Class

| Class | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Vegetation | 0.86 | 0.81 | 0.84 |
| Soil | 0.00 | 0.00 | 0.00 |
| Building | 0.88 | 0.93 | 0.90 |
| Pavement | 0.92 | 0.94 | 0.93 |

The model performed better on the Building and Pavement classes than on Soil. The Soil class had only 19 test samples, and its recorded F1-score was zero. This indicates that the model requires further improvement and validation before it can be relied upon to classify all land-cover categories.

## Technology Stack

- **Programming:** Python
- **Geospatial Processing:** Google Earth Engine, geemap
- **Satellite Data:** Sentinel-2
- **Machine Learning:** scikit-learn, Random Forest
- **Data Analysis:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Prototype Interface:** Gradio

## Potential Applications

Water Watcher explores potential applications in:

- River-area change monitoring.
- Identification of locations requiring further investigation.
- Environmental and land-use monitoring.
- Geospatial decision support for river management.

The results should be treated as preliminary analytical outputs. Satellite-based change detection and land-cover classification alone cannot establish whether a change is illegal encroachment or determine its cause with certainty.

## Limitations and Future Improvements

- Improve the representation of underrepresented classes, particularly Soil.
- Investigate the causes of classification errors using the confusion matrix.
- Validate the classification results against reliable ground-truth data.
- Evaluate the consistency of satellite observations across years and seasons.
- Conduct further spatial validation before using the results for operational decisions.

## Project Recognition

**1st Place — GEO AI Hackathon, Super AI Engineer Season 6 (2026)**

## Project Status

Research prototype. This repository documents the project's implementation in Google Earth Engine and Python, including river-area change analysis, Random Forest classification, and geospatial visualization.
