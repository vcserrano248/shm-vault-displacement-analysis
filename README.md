# Long-Term Structural Displacement Monitoring
## Data Pipeline & Environmental Correlation Analysis for Heritage Masonry Vaults

> **Structural Health Monitoring (SHM) | Python Data Pipeline | Statistical Analysis | Environmental Correlation**

---

## Project Overview

This project presents a complete **data engineering and analysis pipeline** applied to a real-world Structural Health Monitoring (SHM) deployment on a set of heritage masonry vaults. Over a **10-month continuous monitoring period**, 12 laser displacement sensors (distanciometers) recorded structural deformation at 15-minute intervals across three structural zones, generating over 40,000 timestamped observations.

The goal was not simply to process sensor data — it was to **extract engineering-relevant conclusions** from noisy, real-world IoT data: determining whether observed displacements were elastic and thermally driven, identifying zones of higher mechanical stress, and establishing data-driven alert thresholds for structural anomaly detection.

This is the **second reporting cycle** of an ongoing SHM project. The first cycle established a visual baseline; this cycle applies formal statistical methods to validate and extend those findings.

---

## The Structure

The monitored structures are **Gaussian ceramic vaults** — thin-shell reinforced ceramic arch systems characteristic of the work of Uruguayan engineer **Eladio Dieste**. This structural typology is mechanically complex: the arches transfer loads through compression, making their response to thermal expansion and environmental gradients a critical monitoring target.

Three structural zones were instrumented:

| Zone | Sensors | Measurement Axes |
|------|---------|-----------------|
| Zone A | S01 – S04 | Diagonal (arch deformation) + Horizontal (lateral spread) |
| Zone B | S05 – S08 | Diagonal + Horizontal |
| Zone C | S09 – S12 | Diagonal + Horizontal |

Each zone has 2 diagonal sensors (measuring arch vertical deformation) and 2 horizontal sensors (measuring lateral wall spread). Environmental variables — **temperature, relative humidity, atmospheric pressure** — were recorded in parallel for correlation analysis.

---

## Technical Stack

| Tool | Role |
|------|------|
| **Python** | Full pipeline: ingestion, cleaning, analysis, visualization |
| **Pandas / NumPy** | Data manipulation, statistical computation |
| **SciPy** | Statistical modelling |
| **Matplotlib / Seaborn** | All visualizations |
| **scikit-learn** | MinMaxScaler for normalized temporal comparisons |
| **ThingsBoard** | IoT platform (data source — cloud dashboard) |
| **Jupyter Notebooks** | Analysis environment |
| **Excel** | Summary tables for client reporting |

---

## Pipeline Architecture

```
Raw CSVs (monthly, per sensor)
        │
        ▼
01_data_ingestion.ipynb
   → Merge 12 monthly files into unified DataFrame
   → Timestamp parsing and format standardization
   → Export by sector and by individual sensor
        │
        ▼
02_data_cleaning.ipynb  [per sensor — parameterized]
   → Phase 1: Geometric filter — physically impossible values
              (e.g. readings at 6m on a 12m sensor span)
   → Phase 2: IQR method with iterative k-factor selection
              (k iterated until elimination % stabilizes between two consecutive values)
   → Phase 3: Chauvenet Criterion applied where sample requires it
   → Output: validated clean DataFrame per sensor
        │
        ▼
03_statistical_analysis.ipynb
   → Descriptive statistics on clean data (mean, std, CV, IQR, percentiles P1→P99)
   → Movement classification per sensor (amplitude, dispersion, variability)
   → Comparative summary tables across all sensors
        │
        ▼
04_correlation_analysis.ipynb
   → Pearson correlation: each sensor vs Temperature, Humidity, Pressure
   → Correlation matrices per structural zone
   → Cross-sensor correlation (horizontal vs diagonal groups)
   → Normalized temporal overlay plots (sensor + environmental variable)
        │
        ▼
05_sensor_individual_analysis.ipynb  [parameterized — runs for all 12 sensors]
   → Per-sensor: temporal evolution, histogram of real values,
     histogram of relative displacements, percentile bands
   → Final output graphs used in technical report
```

---

## Key Engineering Decisions in the Analysis

These are the choices that required **engineering judgment**, not just code execution:

### 1. Two-phase cleaning strategy
A pure statistical filter (IQR or z-score) applied blindly would discard real structural events. Instead, the pipeline separates:
- **Geometric filter first**: values that violate the physical geometry of the installation are impossible by definition — they are sensor failures, not extreme structural events. Discarded unconditionally.
- **IQR filter second**: applied only to what remains. The multiplier `k` is iterated (k = 1, 2, 3...) and the *stabilization point* — where elimination percentage stops changing significantly between two consecutive k values — defines the valid range. This avoids both over-filtering (losing real peaks) and under-filtering (keeping sensor noise).

### 2. Chauvenet Criterion applied selectively
Not all sensors required Chauvenet. It was applied only where the IQR method left ambiguous edge cases — values that are statistically rare but geometrically plausible. The decision was made sensor-by-sensor based on sample behavior, not applied mechanically to all sensors.

### 3. Relative displacement vs. absolute distance
Sensors measure **absolute distance** (e.g. 12,632 mm). The structural variable of interest is **relative displacement** — how much the reading changes from its minimum reference. All movement analysis is performed on this derived variable, preserving the physical meaning of zero as the structure's most contracted state.

### 4. DI-009 treated as reference-only
Sensor S09 retained only 28% valid data after cleaning, due to persistent connectivity failures. Rather than excluding it entirely or weighting it equally, it was kept in the analysis with explicit flagging as a **reference node** — useful for directional symmetry checks but not for primary conclusions. This is a data integrity decision, not a filter outcome.

### 5. Alert thresholds derived from data, not assumptions
- **Yellow alert** (elastic limit): displacement exceeds the 95th percentile of the validated historical range for that zone.
- **Red alert** (structural anomaly): displacement exceeds mean + 3σ — a threshold that, if reached, indicates a cause beyond thermal cycling.
- **Hysteresis alert**: structure fails to return to its nocturnal baseline (04:00–06:00 AM window), indicating potential permanent deformation.

---

## Key Results

| Finding | Value |
|---------|-------|
| Dominant driver of displacement | Temperature (Pearson r = 0.7–0.9 for most sensors) |
| Humidity / Pressure influence | Negligible (r < 0.4) — correlation is a statistical artifact of the temp/humidity inverse relationship |
| Maximum recorded displacement | 10.97 mm (Zone C, diagonal axis) |
| Typical daily IQR range | 1.0 – 2.9 mm depending on zone and axis |
| Structural diagnosis | Elastic, thermally cyclic — no permanent deformation detected |
| Daily recovery window | 04:00 – 06:00 AM consistently across all sensors |
| Thermal lag confirmed | Displacement peaks trail temperature peaks → thermal inertia of masonry mass |
| Zone C morning anomaly | Abrupt displacement increase at 08:00–10:30 AM → operational load (machinery startup) superimposed on solar heating |

---

## What This Project Demonstrates

- **End-to-end data pipeline** from raw IoT CSV to structured statistical output and client-ready reporting
- **Domain-informed data cleaning**: decisions are grounded in structural engineering logic, not just statistical thresholds
- **Iterative, documented methodology**: each cleaning and analysis step is explicit and reproducible
- **Physical interpretation of statistical results**: Pearson r, IQR, CV and percentile analysis are always linked back to structural behavior, not presented as abstract numbers
- **Multi-sensor comparative analysis**: 12 sensors, 3 zones, 2 axes — synthesized into coherent zone-level and system-level conclusions
- **Alert system design** derived from empirical data distributions, not regulatory defaults

---

## Data Confidentiality

This project was conducted under a professional engagement. The data published here has been **anonymized**:
- Client and location references removed
- Sensor identifiers relabeled (S01–S12)
- Structural zone labels generalized (Zone A / B / C)
- A representative data sample is provided; full dataset is not public

The analysis methodology, code, and results structure are fully representative of the original work.

---

## Repository Structure

```
structural-displacement-monitoring/
├── README.md
├── data/
│   ├── raw/                        ← Monthly CSVs (anonymized sample)
│   └── processed/
│       └── unified_clean_data.csv  ← Merged and cleaned dataset
├── notebooks/
│   ├── 01_data_ingestion.ipynb
│   ├── 02_data_cleaning.ipynb      ← Parameterized per sensor
│   ├── 03_statistical_analysis.ipynb
│   ├── 04_correlation_analysis.ipynb
│   └── 05_sensor_individual_analysis.ipynb
└── outputs/
    └── tables/                     ← Summary Excel tables
```

---

## Author

**Catalina V. Serrano**
Civil Engineer — MSc Structural Engineering
Data Analysis | SHM | Python Pipelines | Applied Engineering

[GitHub](https://github.com/vcserrano248) · [Portfolio](https://vcserrano248.github.io)
