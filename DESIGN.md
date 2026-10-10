# DESIGN.md — Proposed Product and UI/UX Design

**Challenge 9 — Harmonization of MODIS and VIIRS Hot Spots (NASA Space Apps 2026)**

> **Status:** All components described here are **proposed / planned**. None are claimed to exist yet.

---

## 1. Design Goal

Make the sensor-transition artefact in MODIS/VIIRS hotspot records immediately visible, and then make it disappear, so a viewer understands within seconds that the apparent jump in fire counts is caused by the instrument and not by the world.

## 2. Target Users

- **Hackathon judges and general viewers** who need to grasp the problem and the fix quickly (demo audience).
- **Fire-monitoring and response users** who need to know whether activity at a place and time is unusual (responder-facing brief).
- **Analysts working with long hotspot records** who need to compare activity across decades and understand the method (methods panel).

## 3. Core User Experience

The proposed experience centres on one question: *"Is what I see in the record real fire activity, or an instrument effect?"* The user sees a long-term series over South Asia, flips between raw and harmonised views, then explores the burning-activity calendar and map, and finally reads a short brief and the methods behind it.

## 4. Killer Demo Experience

A single toggle over **South Asia, 2003–2026**:

- **Raw view:** counts appear to triple at the sensor transition.
- **Harmonised view:** the step disappears and the real seasonal signal is visible underneath.

This is the most important moment of the product and the anchor of the pitch video. The Build Guide also asks that the pitch mention the operational urgency: Suomi-NPP data stops being available from NASA on 1 November 2026, and MODIS shuts down from late 2026.

## 5. Raw vs Harmonised Toggle

**RAW ↔ HARMONISED** is the primary interaction and should be the most prominent control.

Proposed behaviour:

- One control switches the same chart (and, where applicable, the calendar and map) between raw and harmonised data.
- The time axis, region, and layout stay fixed so that only the data changes.

What the user should understand from comparing the two views:

1. In **raw**, there is a sharp step at the sensor transition that looks like a sudden rise in fire activity.
2. That step is caused by the finer sensor detecting more and smaller fires.
3. In **harmonised**, the step is gone and the recurring seasonal pattern can be read across the whole record.

The toggle is planned to work by 15:00 on Day 1.

## 6. Time-Series Visualisation

- A long-record series (2003–2026) for South Asia, showing raw and harmonised versions.
- The sensor-transition point should be identifiable so the user can connect the step to the instrument change.
- The harmonised view should let the seasonal signal stand out.

## 7. Burning-Activity Calendar

- A calendar view of burning activity that lets users see seasonal timing across the record.
- It should respond to the raw/harmonised toggle so the same artefact-versus-signal story carries through.
- Planned for Day 1 afternoon.

## 8. Map

- An interactive map of hotspot activity, planned alongside the calendar.
- The map provides the spatial context for the regional series and calendar.
- Planned for Day 1 afternoon.

## 9. Seasonal Baseline / Anomaly View

- A seasonal baseline that describes typical activity for a place at a time of year.
- An anomaly view answering: **"Is today unusual for this place at this time of year?"**
- Planned for Day 1 evening. This is the first feature to drop under time pressure (see section 15).

## 10. Methods Panel

- An in-product explanation of how harmonisation is done: common-grid clustering, same-day overlap clustering, detection-difference modelling, and sensor-overlap validation.
- Its purpose is to make the result trustworthy and inspectable.
- Planned for Day 2 morning.

## 11. Responder-Facing Brief

- A short, action-oriented summary aimed at responders, built from the harmonised series and (if available) the anomaly view.
- Its purpose is to turn charts into something usable in an operational setting.
- Planned for Day 2 morning.

## 12. High-Level User Flow

1. Open the app on the South Asia, 2003–2026 view.
2. See the raw series and the apparent jump at the sensor transition.
3. Toggle to harmonised and see the artefact disappear and the seasonal signal emerge.
4. Explore the burning-activity calendar and the map.
5. (If included) Check the seasonal baseline and anomaly view.
6. Read the methods panel to understand and trust the result.
7. Read the responder-facing brief.

## 13. Visual Hierarchy

1. **Primary:** the raw/harmonised toggle and the time series it controls.
2. **Secondary:** the burning-activity calendar and the map.
3. **Tertiary:** seasonal baseline / anomaly view.
4. **Supporting:** methods panel and responder-facing brief.

## 14. Design Priorities

1. Harmonisation correctness comes before presentation (Build Guide: "get it right before anything else").
2. The toggle must work by 15:00 on Day 1.
3. Keep the raw-versus-harmonised contrast unmistakable.
4. Keep supporting views consistent with the toggle state.
5. Keep the demo recordable by 18:30 on Day 1.

## 15. Fallback / Scope Reduction Design

If time is short, reduce in this order:

1. **One region instead of a subcontinent** — the same toggle experience over a single region.
2. **Five years instead of twenty** — a shorter record that still contains the sensor transition.
3. **Drop the anomaly engine, keep harmonisation** — remove the seasonal baseline/anomaly view; the toggle, series, and remaining views stay.

The raw ↔ harmonised toggle is never a candidate for removal.
