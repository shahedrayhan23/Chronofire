# Harmonization of MODIS and VIIRS Hot Spots

**NASA Space Apps Challenge 2026 — Challenge 9**

> A proposed harmonisation engine and burning-activity calendar that removes the sensor-transition artefact from wildfire hotspot records, so fire activity can be compared consistently across decades.

---

## 1. Challenge Overview

Challenge 9 asks teams to combine and harmonise MODIS hotspot detections at one kilometre resolution with VIIRS detections at 375 metres, so that wildfire activity can be tracked consistently across the whole record.

## 2. Problem Statement

The finer-resolution sensor (VIIRS, 375 m) detects more fires, and smaller fires, than the coarser one (MODIS, 1 km). A raw count series therefore shows a **step change at the sensor transition**. That step is an artefact of the instrument, not a change in real-world fire activity. Without correction, long-term trends and comparisons across the record are misleading.

## 3. Proposed Solution

The project proposes to build:

- A **harmonisation engine** that clusters overlapping detections onto a common grid, models the detection difference between sensors, and produces a time series that can be compared consistently across decades.
- A **burning-activity calendar** (with a map) that presents the harmonised record.

> **Status note:** Everything described in this repository is planned or proposed. No part of the software is claimed to be implemented yet.

## 4. Why MODIS and VIIRS Need Harmonisation

| Aspect | MODIS | VIIRS |
|---|---|---|
| Detection resolution | 1 km | 375 m |
| Sensitivity to small fires | Lower | Higher (detects more fires and smaller ones) |

Because of this difference, a switch from one sensor to the other changes detected counts even when actual burning has not changed. Harmonisation aims to separate the instrument effect from the real signal.

**Timely motivation:** Suomi-NPP data stops being available from NASA on 1 November 2026, and MODIS is shutting down from late 2026. Continuity between sensors is therefore an important operational problem, not only an academic one.

## 5. Killer Demo (Planned)

A single toggle switching between **raw** and **harmonised** series over **South Asia, 2003–2026**:

- **Raw:** counts appear to triple at the sensor transition.
- **Harmonised:** the artefact disappears and the real seasonal signal is visible underneath.

## 6. Key Planned Capabilities

- Grid MODIS and VIIRS detections onto a common grid
- Cluster overlapping same-day detections
- Model the detection difference between sensors
- Build raw and harmonised time series
- Raw/harmonised toggle
- Burning-activity calendar and map
- Seasonal baseline and anomaly view ("Is today unusual for this place at this time of year?")
- Sensor-overlap validation
- Methods panel
- Responder-facing brief

See [FEATURES.md](FEATURES.md) for the full feature specification and [DESIGN.md](DESIGN.md) for the proposed UI/UX.

## 7. High-Level Architecture (Proposed)

```
FIRMS MODIS ──┐
              ├──► parquet (pre-event)
FIRMS VIIRS ──┘        │
 (NOAA-20 / NOAA-21)   │
                       ▼
             src/compute/harmonize.py
     grid · cluster · overlap validation · baseline
                       │
           ┌───────────┼────────────┐
           ▼           ▼            ▼
      raw series   harmonised   anomaly vs
                    series      seasonal baseline
           └───────────┼────────────┘
                       ▼
            map + burning calendar
             raw/harmonised toggle
                       │
                       ▼
         methods panel + responder brief
```

## 8. Data Sources (from the Build Guide)

- **FIRMS MODIS** hotspot archive (1 km)
- **FIRMS VIIRS** hotspot archive (375 m), including NOAA-20 / NOAA-21 as shown in the architecture
- Multi-year FIRMS archive CSVs, to be converted to Parquet before the event
- Bulk archive downloads are the preferred route for long records; the transaction limit is 5,000 per ten minutes

## 9. 48-Hour Development Plan (Summary)

| Phase | Planned work |
|---|---|
| Before event | Pull multi-year FIRMS archive CSVs for MODIS and VIIRS; write to Parquet |
| Day 1 morning | Grid detections, cluster overlapping same-day detections, build raw and harmonised series (harmonisation correctness is the priority) |
| Day 1 afternoon | Calendar view and map; raw/harmonised toggle working by 15:00 |
| Day 1 evening | Seasonal baseline and anomaly question; record by 18:30 |
| Day 2 morning | Methods panel, sensor-overlap validation, responder-facing brief |
| Day 2 noon | Freeze, record, submit |

**Pre-build checklist:** multi-year FIRMS Parquet for both sensors; overlap period identified for validation; grid definition agreed.

## 10. Scope Reduction Strategy

If time is short, cut in this order:

1. One region instead of a subcontinent
2. Five years instead of twenty
3. Drop the anomaly engine, but keep harmonisation

## 11. Project Status

**Documentation / planning stage.** The functionality above is proposed. No implementation, results, metrics, or screenshots exist yet, and none are claimed. Setup and run instructions will be added once an implementation exists.

## Documentation

- [README.md](README.md) — project overview (this file)
- [DESIGN.md](DESIGN.md) — proposed product and UI/UX design
- [FEATURES.md](FEATURES.md) — proposed feature specification
