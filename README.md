# Chamarajanagar GeoAI — Agricultural Change Detection & Predictive Analysis

A multi-temporal **GeoAI and Earth Observation framework for agricultural and vegetation change analysis** in Chamarajanagar District, Karnataka, India, using Sentinel-2 satellite data, Google Earth Engine, Python, raster analytics, and machine learning.

The project combines **remote sensing, GIS, temporal analysis, spatial statistics, and predictive machine learning** to identify vegetation changes between 2019 and 2023 and estimate the future NDVI trend.

---
## Large Raster Dataset

The original high-resolution NDVI change raster is approximately **264 MB**, exceeding GitHub's individual file-size limit.

Therefore, the original raster is stored externally in Google Drive rather than directly inside the repository.

### Download the full NDVI change raster

[Download `NDVI_Change_2019_2023.tif` from Google Drive](https://drive.google.com/file/d/15e0vtQX0BRv48HZmsn2H-TaHj1T-C2B8/view?usp=sharing)

File information:

* **File:** `NDVI_Change_2019_2023.tif`
* **Size:** ~264.41 MB
* **Format:** GeoTIFF
* **Period:** 2019–2023
* **Resolution:** 10 m
* **Source:** Google Earth Engine

The `gee_exports/README.md` file also provides access to this dataset.

---

## Project Overview

Agricultural landscapes are continuously influenced by rainfall variability, drought, land-use conversion, agricultural expansion, vegetation degradation, and changing environmental conditions.

This project develops a geospatial workflow to analyze these changes across **Chamarajanagar District** using multi-temporal Sentinel-2 observations.

The workflow consists of two major components:

1. **Earth Observation & Change Detection**

   * Sentinel-2 image processing
   * Cloud masking
   * Seasonal NDVI generation
   * Multi-year vegetation analysis
   * NDVI change detection
   * Significant change-zone identification

2. **Python & GeoAI Analysis**

   * Raster analysis
   * Statistical analysis
   * Vegetation increase/decrease quantification
   * Spatial visualization
   * Temporal machine learning
   * Future NDVI prediction

---

## Study Area

**Chamarajanagar District, Karnataka, India**

The district boundary is used as the Area of Interest (AOI) for all satellite-based analysis.

The project uses the district boundary shapefile stored in:

```text
shapefile/
```

---

## Objectives

* Analyze multi-temporal vegetation dynamics from 2019–2023.
* Generate seasonal Sentinel-2 NDVI composites.
* Detect spatial vegetation changes across the study area.
* Identify significant vegetation increase and decrease zones.
* Quantify the spatial extent of vegetation change.
* Generate statistical summaries and visualizations.
* Develop a machine-learning-based temporal NDVI prediction model.
* Estimate future vegetation conditions based on historical NDVI trends.
* Establish a reproducible GeoAI workflow integrating Google Earth Engine and Python.

---

## Technology Stack

### Remote Sensing & Geospatial Processing

* Google Earth Engine
* Sentinel-2 Surface Reflectance
* NDVI
* GeoTIFF
* Shapefile
* Raster analysis

### Python & GeoAI

* Python
* Google Colab
* NumPy
* Pandas
* Rasterio
* GeoPandas
* Matplotlib
* Scikit-learn

### Version Control

* Git
* GitHub

---

## Workflow

```text
Chamarajanagar District Boundary
              ↓
       Google Earth Engine
              ↓
       Sentinel-2 Data
              ↓
      Cloud Masking
              ↓
   Seasonal Image Composite
              ↓
       NDVI Generation
              ↓
     2019 ─ 2020 ─ 2021 ─ 2022 ─ 2023
              ↓
       NDVI Change Detection
              ↓
   Significant Change Identification
              ↓
       GeoTIFF Export
              ↓
       Python / Google Colab
              ↓
      Raster & Statistical Analysis
              ↓
  Increase / Decrease / Stable Areas
              ↓
       Visualization & CSV
              ↓
    Temporal Machine Learning
              ↓
       Future NDVI Prediction
```

---

## 1. Sentinel-2 Data Processing

Sentinel-2 Surface Reflectance imagery was accessed through Google Earth Engine.

The imagery was:

* filtered spatially using the Chamarajanagar AOI;
* filtered temporally for the agricultural/vegetation season;
* filtered based on cloud percentage;
* subjected to cloud masking;
* combined into median seasonal composites.

Dataset used:

```text
COPERNICUS/S2_SR_HARMONIZED
```

---

## 2. NDVI Generation

NDVI was calculated from the Sentinel-2 Near Infrared and Red bands.

```text
NDVI = (NIR - RED) / (NIR + RED)
```

For Sentinel-2:

```text
NIR = B8
RED = B4
```

NDVI was generated for:

```text
2019
2020
2021
2022
2023
```

The resulting annual layers were used to analyze temporal vegetation dynamics.

---

## 3. NDVI Change Detection

The primary change-detection analysis compares the beginning and ending years:

```text
NDVI Change = NDVI 2023 − NDVI 2019
```

Interpretation:

| NDVI Change | Interpretation               |
| ----------- | ---------------------------- |
| Positive    | Vegetation increase          |
| Near zero   | Relatively stable vegetation |
| Negative    | Vegetation decrease          |

A threshold of:

```text
|NDVI Change| > 0.15
```

was used to identify significant vegetation change zones.

---

## 4. Python Raster Analysis

The exported GeoTIFF results were analyzed in Google Colab using Python.

The analysis included:

* raster loading using Rasterio;
* invalid-value handling;
* NDVI change visualization;
* minimum and maximum change;
* mean NDVI change;
* standard deviation;
* vegetation increase/decrease/stable classification;
* area calculation;
* percentage calculation.

---

## 5. Agricultural Change Statistics

The NDVI change raster was categorized into:

```text
Vegetation Increase
Vegetation Decrease
Stable Area
```

The corresponding pixel counts were converted into area estimates using the Sentinel-2 spatial resolution.

The resulting statistics were saved as:

```text
outputs/agricultural_change_summary.csv
```

---

## 6. Visualization Outputs

The project generates several analytical outputs, including:

### NDVI Change Map

```text
outputs/NDVI_Change_Map.png
```

### NDVI Change Distribution

```text
outputs/NDVI Change Distribution (2019–2023).png
```

### Agricultural Change Distribution

```text
outputs/Agricultural Change Distribution (2019–2023).png
```

These outputs provide both spatial and statistical representations of vegetation dynamics.

---

## 7. Predictive GeoAI

The project extends the descriptive change-detection workflow into predictive analysis.

Yearly district-level mean NDVI values were extracted from Google Earth Engine and used as a temporal dataset.

The machine-learning workflow uses:

```text
Input Feature:
Year

Target:
Mean NDVI
```

A **Linear Regression** model was trained using historical yearly NDVI values.

The model learns the temporal relationship between year and mean NDVI and is then used to estimate a future NDVI value.

Conceptually:

```text
Historical NDVI
      ↓
Temporal ML Model
      ↓
Learned NDVI Trend
      ↓
Future Year
      ↓
Predicted NDVI
```

This provides a predictive component to the GeoAI workflow rather than limiting the project to retrospective change detection.

---

## Repository Structure

```text
Chamrajnagar_GeoAI_Project/
│
├── data/
│   ├── Chamrajnagar_GeoAI_Documentation.docx
│   └── Chamrajnagar_GeoAI_Documentation.pdf
│
├── gee_exports/
│   ├── README.md
│   ├── Significant_Change_Zones.tif
│   └── projection change.tif
│
├── notebooks/
│   ├── Chamrajnagar_GeoAI_Analysis.ipynb
│   └── chamrajnagar_geoai.ipynb
│
├── outputs/
│   ├── NDVI_Change_Map.png
│   ├── NDVI Change Distribution (2019–2023).png
│   ├── Agricultural Change Distribution (2019–2023).png
│   └── agricultural_change_summary.csv
│
├── shapefile/
│   ├── chamarajnagar_shp.shp
│   ├── chamarajnagar_shp.shx
│   ├── chamarajnagar_shp.dbf
│   ├── chamarajnagar_shp.prj
│   └── chamarajnagar_shp.cpg
│
├── .gitignore
├── LICENSE
└── README.md
```

## Main Outputs

The repository provides:

* Multi-temporal NDVI analysis
* NDVI change raster
* Significant vegetation change zones
* Vegetation change statistics
* Hectare-based area estimates
* NDVI distribution analysis
* Agricultural change distribution visualization
* Python notebooks
* Google Earth Engine workflow
* Temporal machine-learning prediction
* Project documentation

---

## Reproducibility

The workflow is divided between Google Earth Engine and Python.

### Google Earth Engine

Used for:

* satellite data access;
* image filtering;
* cloud masking;
* seasonal compositing;
* NDVI generation;
* change detection;
* statistical extraction;
* raster and CSV export.

### Google Colab / Python

Used for:

* GeoTIFF processing;
* statistical analysis;
* visualization;
* area calculation;
* tabular output generation;
* machine-learning analysis;
* future NDVI prediction.

This separation allows the project to use Google Earth Engine for large-scale satellite processing and Python for flexible GeoAI and statistical analysis.

---

## Limitations

The current predictive model is based on a relatively short annual time series from 2019–2023.

Therefore, future NDVI predictions should be interpreted as **trend-based estimates rather than operational agricultural forecasts**.

NDVI changes may also be influenced by factors other than agricultural land-use change, including:

* rainfall variability;
* drought;
* seasonal differences;
* irrigation;
* vegetation phenology;
* land-cover conversion;
* cloud and atmospheric effects.

Additional environmental and agricultural variables would improve future predictive modelling.

---

## Future Scope

The framework can be extended with:

* Random Forest-based LULC classification
* crop/non-crop classification
* XGBoost
* Support Vector Machine
* spatial clustering
* pixel-level temporal trend analysis
* Mann–Kendall trend analysis
* Sentinel-1 SAR integration
* rainfall and climate variables
* soil and terrain variables
* crop-specific classification
* deep-learning-based crop mapping
* interactive WebGIS dashboard
* automated agricultural change monitoring

These extensions can further develop the project into a comprehensive **spatial agricultural intelligence system**.

---

## Project Status

**Current status:** Completed core multi-temporal change-detection and predictive GeoAI workflow.

```text
Remote Sensing          ✓
Google Earth Engine     ✓
NDVI Time Series        ✓
Change Detection        ✓
Raster Analysis         ✓
Spatial Statistics      ✓
Visualization           ✓
Machine Learning        ✓
Future NDVI Prediction  ✓
GitHub Repository       ✓
```

---

## Author

**Himanshu Bhanja**

M.Sc. Agricultural Analytics

---

## Repository

[View the complete project on GitHub](https://github.com/HimanshuBhanja/Chamrajnagar_GeoAI_Project)
