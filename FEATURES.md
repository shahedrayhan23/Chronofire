# FEATURES.md — Proposed Feature Specification

**Challenge 9 — Harmonization of MODIS and VIIRS Hot Spots (NASA Space Apps 2026)**

> **Status:** Every feature below is **Planned / Proposed**. None is claimed to be implemented.

---

## Core Features

### MODIS hotspot processing — *Planned*
- **What:** Processing of MODIS hotspot detections (1 km) from the FIRMS archive.
- **Why:** MODIS forms the long historical part of the record.

### VIIRS hotspot processing — *Planned*
- **What:** Processing of VIIRS hotspot detections (375 m) from the FIRMS archive, including NOAA-20 / NOAA-21 as shown in the architecture.
- **Why:** VIIRS is the finer sensor; it detects more and smaller fires and is the source of the step change.

### Common-grid clustering — *Planned*
- **What:** Cluster overlapping detections, including same-day detections, onto a common grid. The grid definition must be agreed before the build.
- **Why:** Puts both sensors on a comparable footing.

### Detection-difference modelling — *Planned*
- **What:** Model the difference in detections between the finer and coarser sensor.
- **Why:** Enables removal of the instrument-driven step change.

### Harmonised time series — *Planned*
- **What:** A series that can be compared consistently across decades, with the sensor artefact removed.
- **Why:** This is the central output of the project.

### Raw vs harmonised comparison — *Planned*
- **What:** Side-by-side or toggled comparison of raw and harmonised series.
- **Why:** Shows that the step is an artefact of the instrument, not of the world.

---

## Visualisation Features

### Time-series chart — *Planned*
- **What:** Long-record series for South Asia, 2003–2026.
- **Why:** Primary view for seeing the artefact and the real seasonal signal.

### Raw/harmonised toggle — *Planned*
- **What:** A single control switching between raw and harmonised views. Target: working by 15:00 on Day 1.
- **Why:** The killer demo. Raw counts appear to triple at the transition; harmonised shows the artefact gone and the seasonal signal visible.

### Burning-activity calendar — *Planned*
- **What:** Calendar view of burning activity.
- **Why:** Makes seasonal timing readable across the record.

### Map — *Planned*
- **What:** Interactive map of hotspot activity.
- **Why:** Adds spatial context to the regional series and calendar.

---

## Scientific / Analytical Features

### Sensor-overlap validation — *Planned*
- **What:** Validation of the harmonisation using the period where both sensors observe. The overlap period must be identified before the build. Planned for Day 2 morning.
- **Why:** Provides evidence that the harmonisation works.

### Seasonal baseline — *Planned*
- **What:** A baseline of typical activity for a place at a time of year. Planned for Day 1 evening.
- **Why:** Reference for judging whether current activity is unusual.

### Anomaly detection — *Planned*
- **What:** Answers "Is today unusual for this place at this time of year?" using the seasonal baseline.
- **Why:** Turns the series into an operationally relevant signal. It is the first feature to be dropped if time is short.

---

## Operational Features

### Responder-facing brief — *Planned*
- **What:** A short brief aimed at responders. Planned for Day 2 morning.
- **Why:** Makes the output usable in an operational context.

### Methods panel — *Planned*
- **What:** In-product explanation of the methods, including grid, clustering, and overlap validation. Planned for Day 2 morning.
- **Why:** Makes the result transparent and trustworthy.

---

## Data Features

### FIRMS archive CSV ingestion — *Planned*
- **What:** Bulk FIRMS archive CSV downloads for MODIS and VIIRS over the region. Bulk downloads are preferred for long records; the transaction limit is 5,000 per ten minutes.
- **Why:** Long records are impractical to collect within the transaction limit by other means.

### Parquet-based data preparation — *Planned*
- **What:** Convert the archive CSVs to Parquet before the event.
- **Why:** Prepares the data so event time is spent on the harmonisation itself.

### Multi-year historical data — *Planned*
- **What:** A record spanning 2003–2026 where possible (reducible to five years under the scope-reduction plan).
- **Why:** Needed to show the sensor transition and the long-term seasonal signal.

---

## MVP / Must-Have Features

Based on the Build Guide, the minimum viable feature set is:

1. MODIS + VIIRS data
2. Common grid
3. Same-day clustering
4. Detection-difference modelling
5. Raw series
6. Harmonised series
7. Raw/harmonised toggle

## Optional Features

- Calendar
- Map
- Seasonal baseline
- Anomaly engine
- Methods panel
- Responder brief

> **Prioritisation:** If time is limited, the **anomaly engine should be dropped before the core harmonisation functionality**. Scope reduction order: (1) one region instead of a subcontinent, (2) five years instead of twenty, (3) drop the anomaly engine but keep harmonisation.

Note: the Build Guide schedules the methods panel and sensor-overlap validation for Day 2 morning. The MVP list above follows the minimum set specified for the project; validation remains a planned, high-value feature.
