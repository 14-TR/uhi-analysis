## **Urban Heat Island (UHI) Analysis – Notebook Structure (Updated)**

---

### **1. Project Introduction**

**Context & Importance**

- Brief overview of UHIs and their environmental and social implications.

**Objectives**

- Clearly defined goals and research questions.
- Assess spatial and temporal dynamics of UHI over a **12-year period (2013–2024)** to identify trends and long-term impacts.

---

### **2. Data Sources and Description**

**Google Earth Engine (GEE)**

- Overview of GEE platform and benefits for accessing remote sensing data.

**Satellite Imagery**

- Landsat-8/9 and Sentinel-2 accessed directly via GEE for multi-year analysis.

**Vegetation Index Calculation (NDVI)**

- Methodology using GEE built-in functions: `normalizedDifference()` for NDVI from NIR/Red bands.

**Land Surface Temperature (LST)**

- Derived from Landsat thermal bands (ST\_B10) using scaling and offset methods in GEE.

**Socioeconomic Data**

- U.S. Census demographic data at census tract/block group levels for regression analysis.

---

### **3. Data Preparation**

**Acquisition & Preprocessing**

- **Satellite imagery**: Direct acquisition via GEE; atmospheric correction; clipped to study area.
- **Interactive AOI Selection**: Defined via geemap tools; converted to GEE geometry.
- **Temporal Selection**: Focused extraction from **2013 to 2024** to align with Landsat-8/9 and Sentinel-2 availability.
- **Time-Series Extraction**:
  - Automated GEE loop exports **NDVI + LST** (2013–2024).
  - Sentinel-2 used for NDVI; Landsat-8/9 used for NDVI + LST.
  - Data type harmonization ensured export success (e.g., `.toFloat()` casting).
  - Real-time debug logs: band metadata, pixel value summaries, export task status.

**Export Monitoring & Automation**

- Real-time task monitoring.
- **OAuth Authentication**: via `client_secrets.json` for Google Drive API access.
- **PyDrive2 Download**: Automates retrieval of GeoTIFFs from GEE export folder to local directory.
- **Folder Content Verification**: Lists downloaded files, confirms year coverage (2013–2024).

**Data Validation & Import**

- Verified and imported GeoTIFFs using `rasterio`.
- Calculated **mean NDVI and LST per year**, masking no-data values.

---

### **4. Analytical Methods**

**NDVI and LST Analysis**

- Derivation of NDVI and LST maps in GEE.
- **Time Series Analysis**:
  - Extracted **mean NDVI and LST (2013–2024)**.
  - Generated **line plots** to visualize long-term trends.
  - Observed gradual NDVI increase; LST variability.

**Anomaly Detection**

- Computed **z-scores** for NDVI and LST across years.
- Detected **2019 LST anomaly** (significant colder deviation |z| > 2).
- Visualized anomalies on a **z-score plot** with threshold lines.

**Planned Analysis – Percent Change Detection**

- Will compute **year-over-year percent change** for NDVI/LST to assess rapid environmental shifts.

**Hotspot Analysis (Getis-Ord Gi\*)**

- (Planned) Identification of spatial UHI clusters.

**Spatial Regression Modeling**

- (Planned) Analyze statistical relationships between LST, NDVI, and socioeconomic data.

---

### **5. Results & Visualization**

**NDVI/LST Time Series Plot**

- Visualizes trends from 2013–2024.
- NDVI increased post-2016; LST fluctuated, **2019 LST dipped sharply**.

**Anomaly Plot**

- Plotted **z-score anomalies** for NDVI/LST.
- **2019 LST** marked as outlier.

**Statistical Indicators**

- Mean NDVI/LST per year.
- **Anomalies flagged for validation**.

**Socioeconomic Impact Assessment**

- (Planned) Overlay UHI trends with Census data.

---

### **6. Discussion & Conclusions**

**Interpretation of Findings**

- NDVI trends suggest increased vegetation post-2016.
- **2019 LST anomaly** potentially linked to climatic event.
- Ongoing analysis to correlate UHI trends with population vulnerability.

**Recommendations**

- Prioritize **green infrastructure** in LST anomaly-prone areas.
- Deploy **urban cooling strategies** informed by spatial UHI trends.

---

### **7. Appendix**

- **Scripts Used**:
  - `uhi-sat-data-processing.ipynb` – GEE export automation
  - `extract-NDVI-LST-time-series.ipynb` – Yearly metric extraction
  - `anomaly-detection.ipynb` – Z-score and anomaly plotting
  - `time-series-plot.ipynb` – NDVI/LST time series visualization
- **Data Validation**:
  - Debug logs: Band names, types, pixel summaries, task confirmation.
  - Download verification: Script listing all exports (2013–2024).
- **Drive Automation**:
  - Auth via `client_secrets.json`, `PyDrive2`, and `files.get` blob download.
- **Planned Modules**:
  - Percent change detection
  - Hotspot analysis
  - Socioeconomic regression
