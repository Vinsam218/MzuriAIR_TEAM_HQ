# MzuriAIR Team HQ

Working repository for coordinating the MzuriAIR engineering prototype.

## Current release goal

**Milestone 1 — One trustworthy end-to-end telemetry path.**

The watch produces a sample with explicit provenance; an API validates and stores it; an authorized dashboard can retrieve it. The first release is a prototype and research platform, not a clinically validated diagnostic or emergency-response system.

## Current architecture

```text
ESP32-S3 watch firmware
  -> Wi-Fi / HTTPS telemetry
  -> backend API
  -> PostgreSQL database
  -> authenticated web dashboard
  -> Android companion app (later)
```

The watch firmware remains authoritative for its current risk level, AQI, dominant pollutant, reasons and live measurements. The backend should validate and store the transmitted result, not silently recalculate the risk.

## Workstream owners

- **Vinsam — Product and integration:** product scope, telemetry contract, architecture, end-to-end acceptance.
- **Zach — Platform:** backend/API/database, device registration, access control, hub/funding coordination.
- **Nicole — Research and validation:** sensor limitations, test protocols, data provenance, lawful wheeze-dataset research.
- **Trevor — Mechanical/product design:** board measurements, enclosure concept, comfort, sensor placement and charging access.
- **Ephraim — Electrical/hardware:** sensor/pin inventory, power budget, motor-driver feasibility, battery/charging review.

These are proposed role assignments. Confirm ownership and realistic weekly availability before committing dates.

## Milestones

1. **M1 — Specify and de-risk:** agree telemetry fields, define simulated vs measured data, inventory hardware, write test plan.
2. **M2 — Store one sample:** API accepts a valid sample, validates required fields and persists it with timestamps and device identity.
3. **M3 — End-to-end demo:** watch sends telemetry to a reachable backend; dashboard authenticates and displays the latest stored sample.
4. **M4 — Validate and harden:** test reconnects, duplicate/out-of-order samples, missing data, access control, logging and privacy.
5. **M5 — Companion app:** start Android implementation once the API contract is stable.
6. **M6 — Research AI feasibility:** dataset/license review, annotation protocol, baseline evaluation and on-device resource assessment.

## Engineering rules

- Every task has one owner, a due date agreed by the owner, and acceptance criteria.
- Work in small branches and pull requests; request one teammate review before merging.
- Never commit passwords, API keys, Wi-Fi credentials, private health data, raw identifiable audio or real participant location.
- Use synthetic/demo telemetry until the data handling and consent process is ready.
- Every sample must identify whether it is simulated, bench-tested or collected in a real-world study.
- Keep timestamps, sequence numbers, firmware version and sensor status to support debugging and data quality.
- Do not present the prototype as diagnosing asthma or as a clinically validated predictor.
- Do not enable automated emergency-contact alerts until requirements, consent, false-alarm handling, delivery confirmation and safety review are established.

## Weekly rhythm (part-time team)

- **Start of week (15 min):** choose one priority deliverable per person.
- **Midweek (async):** each owner posts blockers and evidence.
- **End of week (30 min):** demo what works, record failed tests, decide the next step.

Report evidence, not activity: screenshots, test logs, sample payloads, measurements, PRs or short demo clips.

## First data contract draft

A telemetry record should include:
- `device_id`, `recorded_at`, `received_at`, `sequence_number`
- `firmware_version`, `data_mode` (simulated / bench / real-world)
- risk state, AQI, dominant pollutant and reason flags as produced by firmware
- available environmental metrics and physiological measurements, each with sensor/status metadata where applicable
- battery, charging and signal status when available

Use server-side UTC timestamps. Do not require continuous GPS for the first milestone; prefer a test-site label or coarse location if location is genuinely needed. Treat audio and physiological data as sensitive, restrict access, and define retention before collecting real participants' data.

## Funding and IP

Track spending with item, purpose, quote, approver, actual cost, receipt and remaining balance. Confirm the hub's funding terms before committing funds. Keep dated invention/contribution records and check university, competition and hub agreements before public disclosure of potentially patentable details.
