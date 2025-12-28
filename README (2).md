# SEGDA: Spatial Exploratory Geostatistical Data Analysis

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MSBD566](https://img.shields.io/badge/Course-MSBD566-green.svg)](https://www.meharry-medical.edu/)

**LISA Clustering for Climate Justice Analysis in California**

A spatial analysis framework for identifying statistically significant clusters of climate stress and environmental justice burden across California's 58 counties. This project supports evidence-based policy targeting under the federal Justice40 Initiative.

![LISA Cluster Example](figures/figure_07_lisa_clusters.png)

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Data Sources](#data-sources)
- [Methodology](#methodology)
- [Results](#results)
- [Project Structure](#project-structure)
- [Citation](#citation)
- [License](#license)

---

## Overview

### Problem Statement

Traditional approaches to climate infrastructure investment analyze counties independently, ignoring spatial dependencies between neighboring regions. This leads to inefficient resource allocation and fails to identify geographic clusters of compound vulnerability.

### Solution

SEGDA applies **Local Indicators of Spatial Association (LISA)** clustering to detect statistically significant spatial patterns in:

- **Outage Burden Index (OBI)** – Power grid reliability
- **Environmental Justice Burden Index (EJBI)** – Socioeconomic vulnerability
- **Heat Stress Index** – Climate hazard exposure
- **Composite Risk** – Weighted combination of all factors

### Policy Relevance

Results directly support the **Justice40 Initiative** (Executive Order 14008), which mandates that 40% of federal climate investment benefits flow to disadvantaged communities.

---

## Key Features

- 🗺️ **Spatial Clustering**: LISA (Local Moran's I) analysis with significance testing
- 📊 **42 Automated Figures**: Choropleth maps, scatter plots, correlation matrices
- 🔥 **Hot Spot Detection**: Identify HH (High-High) priority intervention areas
- ❄️ **Cold Spot Detection**: Identify LL (Low-Low) resilient regions
- 📈 **Statistical Validation**: Global Moran's I with permutation inference
- 🗃️ **Multiple Data Sources**: NOAA, CAL FIRE, CPUC, CalEnviroScreen 4.0

---

## Installation

### Prerequisites

- Python 3.8 or higher
- pip package manager

### Setup

```bash
# Clone the repository
git clone https://github.com/vlfranklin/segda.git
cd segda

# Create virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Dependencies

```txt
geopandas>=0.12.0
pandas>=1.5.0
numpy>=1.23.0
matplotlib>=3.6.0
seaborn>=0.12.0
scipy>=1.9.0
libpysal>=4.6.0
esda>=2.4.0
splot>=1.1.0
shapely>=2.0.0
```

---

## Quick Start

### Run Complete Analysis

```python
from segda_v5_complete_framework import run_complete_analysis

# Execute full analysis pipeline
data, metrics, figures = run_complete_analysis()

# Results saved to: ./segda_v5_figures/
```

### Generate Specific Figures

```python
from segda_v5_complete_framework import (
    create_figure_06_global_moran,
    create_figure_07_lisa_clusters,
    create_figure_35_lisa_obi
)

# Figure 6: Global Moran's I Scatter Plots
create_figure_06_global_moran(data, output_dir='./figures/')

# Figure 7: LISA Cluster Maps (4-panel)
create_figure_07_lisa_clusters(data, output_dir='./figures/')

# Figure 35: Single LISA Map for OBI
create_figure_35_lisa_obi(data, output_dir='./figures/')
```

---

## Data Sources

| Dataset | Source | Variables | Resolution |
|---------|--------|-----------|------------|
| Climate Hazards | NOAA, CAL FIRE | Heat, Drought, Wildfire | County |
| Grid Reliability | EAGLE-I, CPUC | OBI, SAIDI, SAIFI | County |
| Environmental Justice | CalEnviroScreen 4.0 | EJBI, Pollution Burden | Census Tract → County |
| Boundaries | US Census TIGER | County Polygons | EPSG:4326 |

### Data Access

- **California Open Data Portal**: [data.ca.gov](https://data.ca.gov)
- **CalEnviroScreen 4.0**: [OEHHA](https://oehha.ca.gov/calenviroscreen)
- **CPUC Reliability Reports**: [cpuc.ca.gov](https://www.cpuc.ca.gov)

---

## Methodology

### LISA Clustering (Local Moran's I)

LISA detects statistically significant spatial clusters by comparing each county's value to its neighbors.

#### Cluster Classification

| Cluster | Definition | Interpretation | Policy Action |
|---------|------------|----------------|---------------|
| **HH** | High surrounded by High | Hot Spot | Priority Intervention |
| **LL** | Low surrounded by Low | Cold Spot | Resilient Area |
| **HL** | High surrounded by Low | Spatial Outlier | Targeted Action |
| **LH** | Low surrounded by High | Spatial Outlier | Best Practice Model |
| **NS** | p > 0.05 | Not Significant | Insufficient Evidence |

#### Spatial Weights

- **Method**: k-Nearest Neighbors (k=8)
- **Indexing**: KD-tree for efficient computation
- **Inference**: 999 permutations for p-value estimation

### Mathematical Framework

**Local Moran's I Statistic:**

$$I_i = \frac{(x_i - \bar{x})}{\sum_j(x_j - \bar{x})^2 / n} \sum_j w_{ij}(x_j - \bar{x})$$

Where:
- $x_i$ = value at location $i$
- $\bar{x}$ = mean of all values
- $w_{ij}$ = spatial weight between locations $i$ and $j$

---

## Results

### Global Moran's I Statistics

| Variable | Moran's I | Z-Score | p-value | Significance |
|----------|-----------|---------|---------|--------------|
| OBI | 0.417 | 4.23 | < 0.001 | *** |
| EJBI | 0.630 | 6.15 | < 0.001 | *** |
| Heat Stress | 0.887 | 8.54 | < 0.001 | *** |
| Composite Risk | 0.512 | 5.02 | < 0.001 | *** |

*All variables show statistically significant positive spatial autocorrelation.*

### LISA Cluster Counts

| Variable | HH (Hot Spots) | LL (Cold Spots) | HL | LH | NS |
|----------|----------------|-----------------|----|----|-----|
| OBI | 8 | 12 | 3 | 3 | 32 |
| EJBI | 11 | 15 | 2 | 2 | 28 |
| Heat Stress | 14 | 18 | 2 | 1 | 23 |
| Composite Risk | 10 | 14 | 2 | 3 | 29 |

### Key Findings

1. **Central Valley Hot Spots**: Fresno, Kern, Tulare, Kings form contiguous HH clusters for heat stress (I = 0.887)

2. **Coastal Cold Spots**: San Francisco, Marin, San Mateo, Santa Cruz form LL clusters across all variables

3. **EJ-Climate Alignment**: 11 HH counties for EJBI overlap with heat stress hot spots, confirming compound burdens

4. **Spatial Outlier**: Imperial County appears as HL outlier for OBI—high outage burden despite low-burden neighbors

---

## Project Structure

```
segda/
├── README.md
├── requirements.txt
├── LICENSE
├── segda_v5_complete_framework.py    # Main analysis script
├── data/
│   ├── eaglei_transformed.csv        # EAGLE-I outage data
│   ├── California_EPA_clean.csv      # CalEnviroScreen data
│   └── tl_2023_us_county/            # TIGER shapefiles
├── figures/
│   ├── figure_06_global_moran.png    # Global Moran's I
│   ├── figure_07_lisa_clusters.png   # LISA 4-panel maps
│   ├── figure_35_lisa_obi.png        # Single OBI LISA map
│   └── ...                           # 42 total figures
├── outputs/
│   ├── cluster_assignments.csv       # County cluster labels
│   ├── moran_statistics.csv          # Statistical results
│   └── priority_counties.csv         # Justice40 targets
└── docs/
    ├── MSBD566_Midterm_Report.pdf
    └── MSBD566_Presentation.pptx
```

---

## Figures

### Figure 6: Global Moran's I Spatial Autocorrelation

![Global Moran's I](figures/figure_06_global_moran.png)

*Moran scatter plots showing positive spatial autocorrelation for all four variables.*

### Figure 7: LISA Cluster Analysis

![LISA Clusters](figures/figure_07_lisa_clusters.png)

*Four-panel choropleth maps showing LISA clusters for OBI, EJBI, Heat Stress, and Composite Risk.*

---

## Usage Examples

### Custom Analysis

```python
import geopandas as gpd
from libpysal.weights import KNN
from esda.moran import Moran, Moran_Local

# Load data
gdf = gpd.read_file('data/california_counties.shp')

# Create spatial weights
w = KNN.from_dataframe(gdf, k=8)
w.transform = 'r'  # Row-standardize

# Global Moran's I
moran = Moran(gdf['obi'], w)
print(f"Moran's I: {moran.I:.3f}, p-value: {moran.p_sim:.4f}")

# Local Moran's I (LISA)
lisa = Moran_Local(gdf['obi'], w)
gdf['lisa_cluster'] = lisa.q  # 1=HH, 2=LH, 3=LL, 4=HL
gdf['lisa_sig'] = lisa.p_sim < 0.05
```

### Export Results

```python
# Export cluster assignments
results = gdf[['NAME', 'obi', 'ejbi', 'heat_stress', 'lisa_cluster', 'lisa_sig']]
results.to_csv('outputs/cluster_assignments.csv', index=False)

# Export priority counties (HH clusters)
priority = gdf[gdf['lisa_cluster'] == 1][['NAME', 'obi', 'ejbi']]
priority.to_csv('outputs/priority_counties.csv', index=False)
```

---

## References

1. Anselin, L. (1995). Local Indicators of Spatial Association—LISA. *Geographical Analysis*, 27(2), 93-115.

2. California Office of Environmental Health Hazard Assessment. (2021). *CalEnviroScreen 4.0*.

3. U.S. Department of Energy. (2024). *EAGLE-I Power Outage Database*.

4. White House. (2021). *Executive Order 14008: Tackling the Climate Crisis at Home and Abroad*.

---

## Citation

If you use SEGDA in your research, please cite:

```bibtex
@software{franklin2025segda,
  author = {Franklin, Victoria Love},
  title = {SEGDA: Spatial Exploratory Geostatistical Data Analysis},
  year = {2025},
  publisher = {GitHub},
  url = {https://github.com/vlfranklin/segda}
}
```

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- **Course**: MSBD566 – Predictive Modeling and Analytics
- **Institution**: Meharry Medical College, School of Applied Computational Sciences
- **Instructor**: [Instructor Name]

---

## Contact

**Victoria Love Franklin**

- GitHub: [@vlfranklin](https://github.com/vlfranklin)
- Email: vfranklin@mmc.edu

---

<p align="center">
  <i>Supporting equitable climate investment through spatial data science.</i>
</p>
