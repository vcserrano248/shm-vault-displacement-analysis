# Infrastructure Analysis Report
## Long-Term Monitoring of Heritage Masonry Vaults
### Second Monitoring Cycle — April 2025 to February 2026

> 11-month continuous SHM campaign on three heritage ceramic vault structures. 12 laser displacement sensors, 15-minute sampling interval, ~40,000 observations. All identifiers anonymized. For pipeline and methodology documentation, see [README.md](README.md).

---

## Table of Contents

| Section | Content |
|---------|---------|
| [1. Monitoring Setup](#1-monitoring-setup) | Structure, sensor layout, measurement context |
| [2. Data Quality](#2-data-quality) | Valid data per sensor, cleaning outcomes |
| [3. Zone A — Vault 1](#3-zone-a--vault-1) | Displacement behavior, findings, correlation |
| [4. Zone B — Vault 2](#4-zone-b--vault-2) | Displacement behavior, findings, correlation |
| [5. Zone C — Vault 3](#5-zone-c--vault-3) | Displacement behavior, findings, correlation |
| [6. System-Level Comparison](#6-system-level-comparison) | Cross-zone amplitude and dispersion |
| [7. Environmental Correlation](#7-environmental-correlation) | Temperature, humidity, pressure drivers |
| [8. Structural Diagnosis & Alert Framework](#8-structural-diagnosis--alert-framework) | Conclusions, thresholds, recommendations |

---

## 1. Monitoring Setup

### Structure

**Gaussian ceramic vaults** — thin-shell reinforced ceramic arch systems. Load transfer is primarily compressive through the arch, making horizontal spread (lateral wall movement) and diagonal deformation (arch crown displacement) the two critical measurement axes. Three structurally independent vault structures were instrumented at the same site.

| Zone | Structure | Sensors | Diagonal axis | Horizontal axis |
|------|-----------|---------|--------------|----------------|
| Zone A | Vault 1 | S01–S04 | S01, S03 | S02, S04 |
| Zone B | Vault 2 | S05–S08 | S05, S07 | S06, S08 |
| Zone C | Vault 3 | S09–S12 | S09, S11 | S10, S12 |

- **Diagonal sensors:** laser aimed from spring line to arch crown — measures arch deformation under thermal and mechanical loading
- **Horizontal sensors:** laser aimed across vault width at wall level — measures lateral spread of the supporting walls
- **Installation distances:** 12.74 m diagonal axis, 24.80 m horizontal axis
- **Sensor placement:** midpoint of the second arch from the edge of each structure

Environmental variables recorded in parallel at site level: Temperature (°C), Relative Humidity (%), Atmospheric Pressure (hPa).

### Monitoring Period

| Parameter | Value |
|-----------|-------|
| Start | April 1, 2025 |
| End | February 28, 2026 |
| Duration | 11 months |
| Sampling interval | 15 minutes |
| Total timestamps | 3,463 |
| Excluded period | March 2025 — sensor installation and calibration |

---

## 2. Data Quality

A three-phase sequential cleaning pipeline was applied independently to each sensor (geometric filter → Chauvenet Criterion → IQR filter). Full methodology in [README.md](README.md).

![Raw data summary — all sensors before cleaning](assets/tables/table_00_raw_data_summary.png)
*Raw timestamp count per sensor before any cleaning. Gaps in Zone B and S09 are visible here as reduced total counts.*

![Valid records per sensor after cleaning](assets/tables/table_01_valid_records.png)
*Percentage of valid records retained after the full cleaning pipeline. Green = excellent (>90%), yellow = acceptable (>70%), red = reference only (<30%).*

![Clean data statistical summary](assets/tables/table_02_clean_summary.png)
*Key statistics per sensor on clean data: mean displacement, standard deviation, coefficient of variation, and IQR band. Relative displacement values (movement from structural minimum reference).*

**Data quality summary by zone:**

| Zone | Data quality | Primary issue | Impact on analysis |
|------|-------------|---------------|-------------------|
| Zone A | Excellent — 91–97% valid | None | Full confidence in all statistical conclusions |
| Zone B | Acceptable — 58–86% valid | Dec 2025 connectivity outage (all 4 sensors affected simultaneously) | Maximum displacement values are conservative floor estimates — summer peak during outage not captured |
| Zone C (S10, S11, S12) | Good — 76–96% valid | Minor connectivity gaps | Reliable for primary analysis |
| S09 (Zone C diagonal) | Reference only — 28.18% valid | Sustained connectivity failure | Excluded from primary conclusions; retained for directional symmetry checks only |

The December 2025 Zone B outage was identified as a connectivity failure rather than a structural event: all four Zone B sensors show simultaneous data gaps while Zone A and Zone C sensors continue recording normally during the same period.

---

## 3. Zone A — Vault 1

Zone A is the most structurally stable zone. Highest data quality in the system, lowest standard deviations, and the most rhythmically predictable displacement pattern across all four sensors.

### Representative sensor: S01 (Diagonal)

![S01 Temporal Evolution](outputs/figures/S01/S01_03_temporal_evolution.png)
*10-month absolute displacement record for S01. Reference lines: Q1–Q3 band (green) = structural baseline range under normal daily conditions; Median (purple) = central tendency; P5/P95 (yellow) = operational limits. The signal shows a continuous thermal cycle with consistent nocturnal return to the P5 level.*

![S01 Displacement Distribution](outputs/figures/S01/S01_02_displacement_distribution.png)
*Relative displacement frequency distribution for S01. The bell-shaped histogram with a well-defined central peak indicates stable, unimodal behavior — the structure consistently occupies a narrow displacement range under normal conditions. Percentile bands confirm P95 as a well-defined operational boundary.*

![S01 Absolute Values Histogram](outputs/figures/S01/S01_03_absolute_values_histogram.png)
*Distribution of raw absolute laser distance readings. The narrow spread (approx. 5.6 mm total range over 11 months across ~3,300 valid records) confirms the sensor is operating within a predictable, tight mechanical envelope.*

### Zone A statistics

| Metric | S01 (Diag.) | S02 (Hor.) | S03 (Diag.) | S04 (Hor.) |
|--------|:-----------:|:----------:|:-----------:|:----------:|
| Max displacement (mm) | 5.62 | 6.33 | 9.75 | 7.29 |
| Mean displacement (mm) | 2.36 | 2.60 | 4.61 | 2.51 |
| Std. Dev. (mm) | 1.07 | 1.21 | 1.85 | 1.55 |
| CV (%) | 45.5 | 46.6 | 40.0 | 62.0 |
| IQR band (mm) | 1.62–2.74 | 1.92–3.00 | 3.25–5.91 | 1.38–3.20 |

### Zone A findings

- **S01 and S02** show the lowest standard deviations in the entire system (1.07–1.21 mm). These are the most predictable measurement points — the arch and wall at this position behave as a mechanically stable unit.
- **S03 (diagonal)** is the structural outlier within Zone A: mean displacement of 4.61 mm and IQR amplitude of 2.66 mm are substantially higher than the zone average. S03 absorbs significantly more deformation energy at its measurement point — consistent with a geometric asymmetry or local reduction in stiffness at that arch position. This is a monitoring priority within Zone A despite overall zone stability.
- All four sensors return to their P5 baseline between 04:00–06:00 AM throughout the monitoring period without exception, confirming elastic behavior with no permanent deformation.

### Zone A correlation

![Zone A Correlation Matrix](outputs/tables/04_correlation_matrix_zone_a.png)
*Pearson correlation coefficients for Zone A sensors vs. each other and vs. environmental variables. Strong inter-sensor correlation (r > 0.75) confirms the four sensors respond to thermal loading as a mechanically coherent unit. Temperature dominates all sensors (r = 0.61–0.83). S03's lower temperature correlation relative to its peers is consistent with a local constraint that partially decouples its thermal response.*

---

## 4. Zone B — Vault 2

Zone B shows higher mean displacements than Zone A and greater sensitivity to rapid thermal changes. Despite December 2025 data gaps, the available sample supports reliable trend analysis for all four sensors.

### Representative sensor: S08 (Horizontal)

S08 was selected as Zone B representative because it records the second-highest mean displacement in the entire system while maintaining the lowest coefficient of variation of any sensor (CV = 28.3%) — an unusual combination that reflects a structurally significant mechanical role.

![S08 Temporal Evolution](outputs/figures/S08/S08_03_temporal_evolution.png)
*S08 temporal record. Despite the high absolute displacement (mean 5.24 mm), the signal is highly rhythmic — the structure expands substantially under thermal loading but returns to the same baseline every morning. This consistency, visible across the full 10-month record including the winter-to-summer transition, confirms the lateral wall at this position is absorbing thermal expansion elastically without progressive deformation.*

![S08 Displacement Distribution](outputs/figures/S08/S08_02_displacement_distribution.png)
*S08 displacement distribution. The compact, symmetric histogram (IQR amplitude of only 1.91 mm despite a max of 10.19 mm) reflects the highly rhythmic nature of the signal — the vast majority of records cluster tightly around the mean, with the P95–P99 tail representing summer thermal peaks.*

### Zone B statistics

| Metric | S05 (Diag.) | S06 (Hor.) | S07 (Diag.) | S08 (Hor.) |
|--------|:-----------:|:----------:|:-----------:|:----------:|
| Max displacement (mm) | 10.33 | 7.26 | 7.13 | 10.19 |
| Mean displacement (mm) | 4.26 | 2.74 | 3.48 | 5.24 |
| Std. Dev. (mm) | 1.99 | 0.98 | 1.25 | 1.48 |
| CV (%) | 46.9 | 35.7 | 36.0 | 28.3 |
| IQR band (mm) | 2.87–5.44 | 2.08–3.08 | 2.53–3.98 | 4.29–6.19 |

### Zone B findings

- **S08** is the primary thermal expansion absorption point in Zone B. Its high mean displacement combined with extreme rhythmic consistency (lowest CV in the system) indicates this wall position deflects substantially but elastically under every thermal cycle — it has found a stable mechanical equilibrium.
- **S06** provides the stability counterpoint: low mean (2.74 mm), lowest std dev in Zone B (0.98 mm), and the most compact IQR (1.00 mm amplitude). Occasional isolated spikes visible in the temporal series are statistically isolated events (outside P99) — likely sensor transmission artifacts rather than structural events, given no simultaneous response in adjacent sensors.
- **S05 maximum of 10.33 mm** should be read as a conservative floor: the December 2025 outage covered several days of summer thermal loading. Actual peak displacement during that period may have been marginally higher.

### Zone B correlation

![Zone B Correlation Matrix](outputs/tables/04_correlation_matrix_zone_b.png)
*Pearson correlation for Zone B. Temperature dominates diagonal sensors strongly (r = 0.80–0.88). S06 shows a markedly weaker temperature correlation (r = 0.31) compared to all other horizontal sensors in the system — consistent with its multimodal distribution suggesting this sensor position operates across multiple equilibrium states, possibly influenced by variable thermal gradients or localized operational loading at that vault position.*

---

## 5. Zone C — Vault 3

Zone C is the most mechanically active zone. It contains the sensor with the highest total displacement (S11: 10.64 mm), the highest coefficient of variation (S11: 75.0%), and the only multimodal displacement distribution in the system. Operational loads superimpose on the thermal cycle at this vault, producing a more complex mechanical environment than Zones A and B.

### Representative sensor: S11 (Diagonal)

S11 was selected as Zone C representative because it is the most structurally significant monitoring point in the entire system — highest variability, most complex signal, highest priority for ongoing surveillance.

![S11 Temporal Evolution](outputs/figures/S11/S11_03_temporal_evolution.png)
*S11 temporal record. Unlike the smooth sinusoidal patterns of Zones A and B, S11 shows irregular amplitude variation and a morning displacement spike consistently appearing between 08:00–10:30 AM. This spike is superimposed on the thermal expansion baseline and does not correlate with the other diagonal sensors, indicating a localized operational mechanical load rather than a structural or thermal event.*

![S11 Displacement Distribution](outputs/figures/S11/S11_02_displacement_distribution.png)
*S11 displacement distribution. The flat, spread histogram with no dominant central peak reflects the high variability (CV = 75%) and multi-state behavior of this sensor. The structure at this position occupies the full 0–10.64 mm range with roughly equal frequency — structurally significant as it indicates this arch position operates at or near its elastic limit under combined thermal and operational loading.*

![S11 Absolute Values Histogram](outputs/figures/S11/S11_03_absolute_values_histogram.png)
*S11 absolute value distribution. The bimodal shape confirms the two operating states: a lower-displacement state (thermal contraction at night and winter) and a higher-displacement state (thermal expansion plus operational loading during active hours). The separation between the modes corresponds to the operational load contribution.*

### Zone C statistics

| Metric | S09 (Diag.)* | S10 (Hor.) | S11 (Diag.) | S12 (Hor.) |
|--------|:-----------:|:----------:|:-----------:|:----------:|
| Max displacement (mm) | 14.08 | 5.43 | **10.64** | 6.95 |
| Mean displacement (mm) | 5.76 | 2.46 | 3.20 | 2.09 |
| Std. Dev. (mm) | 2.11 | 0.96 | **2.40** | 1.32 |
| CV (%) | 36.6 | 39.1 | **75.0** | 63.2 |
| IQR band (mm) | 4.29–7.17 | 2.00–3.00 | 1.30–4.70 | 1.25–2.82 |

*S09: reference node only — 28.18% valid data due to sustained connectivity failure

### Zone C findings

- **S11** is the highest-priority monitoring point in the system. CV of 75% is the only instance classified as Highly Volatile — more than double the system average. The bimodal distribution and morning spike pattern indicate this arch is under combined thermal and operational mechanical loading. While elastic behavior is confirmed (daily baseline return observed), this sensor requires priority surveillance to detect any progressive shift in its operating range.
- **S10** provides the structural counterpoint: std dev of 0.96 mm and a perfectly compact IQR of exactly 1.00 mm amplitude. The lateral wall at this position is stable — S11's high variability on the diagonal axis is not driving lateral wall instability at the same vault section.
- The **08:00–10:30 AM displacement spike in S11** is the most structurally interesting pattern in the dataset. It appears consistently, it is not present in S03, S05, or S07 (other diagonal sensors), and it precedes the daily temperature peak. This is consistent with operational loading — machinery startup or large door openings at the vault — superimposed on the early-morning solar heating ramp. Investigation against operational records is recommended.

### Zone C correlation

![Zone C Correlation Matrix](outputs/tables/04_correlation_matrix_zone_c.png)
*Zone C Pearson correlation. S10 and S12 (horizontal sensors) show moderate temperature correlation (r = 0.61–0.72), consistent with the rest of the system. S11's lower temperature correlation (r = 0.56) reflects the operational loading component that partially decouples its behavior from the purely thermal pattern. S09 results are reported for reference only given the data quality limitations.*

---

## 6. System-Level Comparison

### Total Displacement Amplitude

![Total Displacement Comparison — All Sensors](outputs/tables/03_total_displacement_comparison.png)
*Maximum total displacement amplitude (mm) recorded per sensor over the full monitoring period. Zone B and Zone C diagonal sensors reach the highest amplitudes (>10 mm), while Zone A remains more contained (<10 mm). This reflects differences in thermal inertia and local structural stiffness between the three vaults — Zone A provides greater thermal buffering at the measurement positions.*

### Behavioral Dispersion

![Standard Deviation Comparison — All Sensors](outputs/tables/03_std_dev_comparison.png)
*Standard deviation of displacement per sensor — a measure of how consistently the structure occupies a given displacement state. S11 (Zone C diagonal) shows the highest dispersion in the system (2.40 mm), confirming it as the most mechanically reactive point. Zone A sensors cluster below 1.85 mm — highest predictability in the system. Diagonal sensors consistently show higher dispersion than their horizontal counterparts within the same zone, reflecting the greater energy absorbed by the arch deformation axis relative to the wall spread axis.*

### Cross-Zone Behavior by Axis

**Horizontal sensors — lateral wall spread:**

![Horizontal Sensors Correlation Matrix](outputs/tables/04_correlation_matrix_horizontal_sensors.png)
*Cross-zone Pearson correlation for all six horizontal sensors. Strong inter-sensor correlation (r > 0.64 for most pairs) confirms all three vaults expand laterally in synchrony — the thermal signal drives wall spread uniformly across the site regardless of zone. This validates the three structures as mechanically coherent under thermal loading despite being structurally independent.*

**Diagonal sensors — arch deformation:**

![Diagonal Sensors Correlation Matrix](outputs/tables/04_correlation_matrix_diagonal_sensors.png)
*Cross-zone Pearson correlation for all six diagonal sensors. More heterogeneous than horizontal sensors. S01's low cross-correlation with the other diagonal sensors is consistent with the local stiffness anomaly identified in Zone A. S03, S05, S07, and S11 form a moderately correlated group — they respond to temperature but with zone-specific amplification factors reflecting different geometric properties and structural stiffness at each vault's arch measurement point.*

---

## 7. Environmental Correlation

### Temperature — Dominant Mechanical Driver

![Temporal overlay — Diagonal sensors vs Temperature](outputs/tables/04_temporal_vs_temperature_diagonal.png)
*Normalized temporal comparison: all six diagonal sensors vs. temperature, scaled to the same range. The high co-movement across the full 10-month record confirms temperature as the primary displacement driver system-wide. The thermal hysteresis pattern — displacement peaks lagging several hours behind temperature peaks — is visible in both spring/autumn and summer records, validating the thermal inertia of the masonry mass.*

![Temporal overlay — Horizontal sensors vs Temperature](outputs/tables/04_temporal_vs_temperature_horizontal.png)
*Same analysis for horizontal sensors. The lateral wall spread response to temperature is tighter and more synchronous than the diagonal arch response, consistent with a shorter thermal diffusion path through the wall section compared to the arch geometry.*

**Temperature correlation summary:**

| Zone | Sensor | Axis | Pearson r vs Temp | Interpretation |
|------|--------|------|:-----------------:|----------------|
| A | S01 | Diag. | +0.83 | Strong positive — primary thermal responder in zone |
| A | S02 | Hor. | +0.78 | Strong positive |
| A | S03 | Diag. | +0.61 | Moderate — local stiffness constraint moderates response |
| A | S04 | Hor. | +0.76 | Strong positive |
| B | S05 | Diag. | +0.88 | Strong positive — highest temperature sensitivity in system |
| B | S06 | Hor. | +0.31 | Weak — multi-state behavior, additional load influences |
| B | S07 | Diag. | +0.80 | Strong positive |
| B | S08 | Hor. | +0.77 | Strong positive |
| C | S10 | Hor. | +0.72 | Strong positive |
| C | S11 | Diag. | +0.56 | Moderate — operational loading decouples thermal response |
| C | S12 | Hor. | +0.61 | Moderate positive |

**Summer behavior:** During sustained high-temperature periods (January–February 2026), the structure does not fully cool to its winter minimum overnight. The daily displacement amplitude remains unchanged — indicating constant structural stiffness — but the absolute baseline shifts temporarily upward. This is an expected seasonal behavior of thermally massive masonry, not a structural anomaly.

### Humidity — Statistical Artifact, Not Mechanical Driver

![Temporal overlay — Diagonal sensors vs Humidity](outputs/tables/04_temporal_vs_humidity_diagonal.png)
*Diagonal sensors vs. humidity overlay. The systematic inverse co-movement (displacement up, humidity down) is not a hygroscopic mechanical effect — it is a statistical consequence of the temperature-humidity inverse relationship. When temperature rises and the structure expands, ambient humidity simultaneously drops. Temperature is the underlying cause; humidity is a collinear proxy variable. No independent mechanical contribution from humidity was detected.*

### Atmospheric Pressure — Confirmed No Influence

![Temporal overlay — Horizontal sensors vs Pressure](outputs/tables/04_temporal_vs_pressure_horizontal.png)
*Horizontal sensors vs. atmospheric pressure overlay. Near-zero correlation across all sensors (r ≈ −0.10) confirms pressure has no measurable mechanical effect on the structure — the technically expected result for rigid masonry at this scale. The absence of spurious correlation also validates sensor calibration stability: instrumental drift would produce a false pressure correlation.*

---

## 8. Structural Diagnosis & Alert Framework

### Diagnosis

> **The three vault structures are operating within normal elastic parameters. All observed displacements are thermally cyclic, reversible, and consistent with the expected mechanical behavior of ceramic masonry under seasonal temperature variation. No evidence of permanent deformation, progressive stiffness degradation, or anomalous structural response was detected during the monitoring period.**

Three independent lines of evidence support this conclusion:

**1. Elastic recovery:** Every sensor returns to its minimum baseline between 04:00–06:00 AM daily throughout the full 10-month record, including during sustained summer heat periods. The structure recovers its contracted position at every nocturnal cooling cycle without residual displacement.

**2. Constant stiffness:** Daily displacement amplitude (peak-to-valley range) remained stable across all 11 months. Progressive stiffness degradation would manifest as growing amplitude for the same thermal input. This was not observed in any sensor.

**3. Temperature predictability:** Pearson r = 0.7–0.9 across most sensors. A structure undergoing progressive damage would show increasing deviation from the temperature-driven pattern as new load paths or crack propagation alter the mechanical response. The correlation remained stable throughout the monitoring period.

### Zone-Level Status Summary

| Zone | Stability classification | Maximum displacement | Primary risk point | Status |
|------|------------------------|---------------------|-------------------|--------|
| Zone A | High | 9.75 mm (S03) | S03 — diagonal, above zone average | ✅ Normal operation |
| Zone B | Moderate | 10.33 mm (S05) | Dec 2025 data gap — peak not captured | ✅ Normal, monitor data continuity |
| Zone C | Lower | 10.64 mm (S11) | S11 — highly volatile, operational loading superimposed | ✅ Normal, priority surveillance |

### Alert Threshold Framework

Thresholds are derived from the empirical displacement distributions — not regulatory defaults. Each sensor has individual thresholds based on its own historical data.

| Alert level | Trigger | Required action |
|-------------|---------|----------------|
| 🟡 **Yellow — Elastic limit** | Displacement exceeds P95 for that sensor | Verify nocturnal return to baseline in next 04:00–06:00 AM window |
| 🔴 **Red — Structural anomaly** | Displacement exceeds mean + 3σ (approx. >11.5 mm on critical axes) | Immediate inspection — cause is non-thermal or structural stiffness has changed |
| ⚠️ **Hysteresis** | Sensor fails to return to its P5 baseline by 06:00 AM | Potential permanent deformation — structural assessment required |
| 📊 **Variability drift** | CV of Zone A sensors increases >15% above historical values | Loss of mechanical homogeneity at the most stable zone — investigate cause |

### Recommendations

**Priority surveillance — monitor first:**
S03 (Zone A diagonal), S05 (Zone B diagonal), S11 (Zone C diagonal) — highest amplitude points in the system, and the first sensors to reflect any change in structural stiffness or load distribution.

**Data continuity — restore before next summer cycle:**
Zone B connectivity requires confirmation before the next peak thermal season (Dec 2025–Feb 2026). A summer peak during an outage would leave the maximum displacement record without its most critical observations. S09 (Zone C diagonal) requires hardware inspection — 28.18% valid data over 11 months indicates a persistent installation or connectivity problem.

**Operational loading investigation (Zone C):**
The 08:00–10:30 AM displacement spike on S11 should be correlated with operational records (machinery startup times, door opening schedules) to confirm the source and verify that the superimposed mechanical load remains within design parameters for the arch section. If the operational load magnitude can be quantified, a combined thermal + operational load envelope can replace the current thermal-only alert thresholds for this sensor.

**Annual cycle validation:**
At the start of each winter minimum, verify that all sensors return to the same baseline as the previous winter. A permanent upward shift in the nocturnal minimum — even by 0.5–1.0 mm — would indicate progressive deformation that the daily elastic recovery check would not detect.

---

*Generated from analysis pipeline: `01_data_ingestion` → `02_data_cleaning` → `03_statistical_analysis` → `04_correlation_analysis` → `05_sensor_individual_analysis`*

*Monitoring period: April 2025 – February 2026 | 12 sensors | 3 structural zones | ~40,000 observations*

*All identifiers anonymized. Methodology and code documentation in [README.md](README.md).*

---

**Veronica C. Serrano**
M.Sc. Civil Engineer — Structures and Materials
[GitHub](https://github.com/vcserrano248) · [Portfolio](https://vcserrano248.github.io)
