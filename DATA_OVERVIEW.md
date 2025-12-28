# California Climate Risk Data Overview

## Real Data Sources Used in Analysis

This analysis uses **three California datasets** to assess climate risk and environmental justice burden across 58 counties.

---

## 1. CalEnviroScreen 4.0 (Environmental Justice Burden)

**Source:** California Office of Environmental Health Hazard Assessment (OEHHA)  
**URL:** https://oehha.ca.gov/calenviroscreen  
**Records:** 58 counties, 25 variables

### Description
CalEnviroScreen is California's official environmental justice screening tool. It combines pollution burden indicators (air quality, water contamination, hazardous waste) with population vulnerability factors (poverty, health outcomes, linguistic isolation).

### Top 15 Counties by EJ Burden Score

| Rank | County | CalEnviroScreen Score |
|------|--------|----------------------|
| 1 | **Imperial** | 78.2 |
| 2 | **Kern** | 71.8 |
| 3 | **Fresno** | 68.4 |
| 4 | **Kings** | 67.1 |
| 5 | **Tulare** | 66.3 |
| 6 | Los Angeles | 64.8 |
| 7 | Merced | 63.5 |
| 8 | San Bernardino | 62.1 |
| 9 | Madera | 60.8 |
| 10 | Riverside | 59.4 |
| 11 | San Joaquin | 58.2 |
| 12 | Stanislaus | 56.9 |
| 13 | Glenn | 55.3 |
| 14 | Monterey | 54.1 |
| 15 | Sacramento | 52.8 |

### Key Pattern
**Central Valley and Imperial County dominate** - these agricultural regions face high pollution from pesticides, diesel particulate matter, and drinking water contamination, combined with high poverty rates and limited healthcare access.

---

## 2. CAL FIRE Incidents (2013-2025)

**Source:** California Department of Forestry and Fire Protection (CAL FIRE)  
**URL:** https://www.fire.ca.gov  
**Records:** 69 major incidents across 27 counties

### Description
This dataset includes all major wildfires in California from 2013-2025, tracking acres burned, fatalities, and structures destroyed. It captures catastrophic events like the Camp Fire (2018) and Mendocino Complex (2018).

### Top 15 Counties by Total Acres Burned

| Rank | County | Acres Burned (thousands) | Notable Fires |
|------|--------|--------------------------|---------------|
| 1 | **Butte** | 1,800+ | Camp Fire (2018) |
| 2 | **Mendocino** | 1,500+ | Mendocino Complex (2018) |
| 3 | Napa | ~500 | Atlas Fire, Glass Fire |
| 4 | Santa Clara | ~350 | SCU Lightning Complex |
| 5 | Ventura | ~300 | Thomas Fire, Woolsey Fire |
| 6 | Fresno | ~280 | Creek Fire (2020) |
| 7 | Shasta | ~250 | Carr Fire (2018) |
| 8 | Los Angeles | ~200 | Woolsey Fire |
| 9 | Trinity | ~180 | Multiple fires |
| 10 | El Dorado | ~150 | Caldor Fire |
| 11 | Siskiyou | ~140 | Multiple fires |
| 12 | Mariposa | ~130 | Ferguson Fire |
| 13 | San Bernardino | ~120 | Multiple fires |
| 14 | Sonoma | ~100 | Tubbs Fire, Kincade Fire |
| 15 | Tulare | ~90 | Multiple fires |

### Key Pattern
**Butte and Mendocino are extreme outliers** - Butte County experienced the deadliest wildfire in California history (Camp Fire: 85 deaths, 18,804 structures destroyed). Northern California counties face the highest wildfire burden.

---

## 3. NOAA Storm Events Database (2010-2024)

**Source:** NOAA National Centers for Environmental Information  
**URL:** https://www.ncdc.noaa.gov/stormevents  
**Records:** 183 events across 58 counties

### Description
The Storm Events Database tracks significant weather events including heat waves, floods, winter storms, and wildfire events. This analysis focuses on heat events (Heat, Excessive Heat) as indicators of climate stress.

### Top 15 Counties by Heat Events

| Rank | County | Heat Events |
|------|--------|-------------|
| 1 | **Imperial** | 5 |
| 2 | **Fresno** | 4 |
| 3 | **Kern** | 4 |
| 4 | **Riverside** | 4 |
| 5 | **San Bernardino** | 4 |
| 6 | Glenn | 3 |
| 7 | Kings | 3 |
| 8 | Los Angeles | 3 |
| 9 | Merced | 3 |
| 10 | Orange | 3 |
| 11 | Sacramento | 3 |
| 12 | San Diego | 3 |
| 13 | San Joaquin | 3 |
| 14 | Solano | 3 |
| 15 | Stanislaus | 3 |

### Key Pattern
**Desert and Central Valley counties face the most extreme heat** - Imperial, Fresno, Kern, Riverside, and San Bernardino consistently experience dangerous heat events, compounding existing environmental justice concerns.

---

## Compound Risk Analysis

Counties appearing in **multiple high-risk categories** face compound vulnerability and should be prioritized for Justice40 climate investment.

### Triple Threat Counties (High in All 3 Categories)

| County | EJ Burden | Wildfire | Heat | Compound Risk Level |
|--------|:---------:|:--------:|:----:|:-------------------:|
| **Los Angeles** | ✓ High | ✓ High | ✓ High | 🔴 **CRITICAL** |
| **Fresno** | ✓ High | ✓ High | ✓ High | 🔴 **CRITICAL** |
| **San Bernardino** | ✓ High | ✓ Moderate | ✓ High | 🔴 **CRITICAL** |

### Dual Threat Counties

| County | Primary Risks | Compound Risk Level |
|--------|---------------|:-------------------:|
| **Kern** | EJ Burden + Heat | 🟠 **HIGH** |
| **Imperial** | EJ Burden + Heat | 🟠 **HIGH** |
| **Riverside** | EJ Burden + Heat | 🟠 **HIGH** |
| **Butte** | Extreme Wildfire | 🟠 **HIGH** |
| **Mendocino** | Extreme Wildfire | 🟡 MODERATE |

---

## Data Integration Summary

| Data Source | Geographic Coverage | Time Period | Key Variables |
|-------------|---------------------|-------------|---------------|
| CalEnviroScreen 4.0 | 58 counties | 2021 | Pollution burden, socioeconomic vulnerability |
| CAL FIRE | 27 counties (with incidents) | 2013-2025 | Acres burned, fatalities, structures |
| NOAA Storm Events | 58 counties | 2010-2024 | Heat events, floods, storms |

### Derived Risk Indices

From these three sources, we computed the following normalized (0-1) risk indices:

| Index | Formula |
|-------|---------|
| **EJBI** | CalEnviroScreen score + poverty + housing burden |
| **heat_stress** | NOAA heat event count (normalized) |
| **wildfire_risk** | log(acres burned) + fire count + structures (normalized) |
| **flood_risk** | NOAA flood + heavy rain events (normalized) |
| **OBI** | Property damage + injuries + fatalities (normalized) |
| **composite_risk** | 0.35×EJBI + 0.25×climate + 0.25×wildfire + 0.15×OBI |

---

## Conclusions

1. **Central Valley counties** (Kern, Fresno, Tulare, Kings) face severe environmental justice burden combined with extreme heat stress.

2. **Butte County** experienced catastrophic wildfire impacts (Camp Fire) that make it a priority despite lower EJ burden.

3. **Los Angeles County** has the highest overall composite risk due to its combination of high population, EJ burden, and multiple climate hazards.

4. **19 counties (32.8%)** are classified as High Risk and should be prioritized for Justice40 climate infrastructure investment.

---

## References

1. California OEHHA. (2021). *CalEnviroScreen 4.0*. https://oehha.ca.gov/calenviroscreen
2. CAL FIRE. (2025). *California Fire Incidents Database*. https://www.fire.ca.gov
3. NOAA NCEI. (2024). *Storm Events Database*. https://www.ncdc.noaa.gov/stormevents
4. White House. (2021). *Executive Order 14008: Justice40 Initiative*.
