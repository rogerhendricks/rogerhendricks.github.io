---
title: "Pacemaker Manufacturer Timing Systems: A Clinical Comparison"
date: 2022-04-01T19:24:49+11:00
lastmod: 2026-05-31T10:36:00+10:00
description: "An in-depth clinical look at atrial-based vs. ventricular-based timing systems across major cardiac device manufacturers including Abbott, Medtronic, Biotronik, and more."
summary: "Understanding how different cardiac device manufacturers handle pacing timing is crucial for optimal device programming. We compare atrial-based vs. ventricular-based timing behaviors across major pacemaker manufacturers."
tags: ["pacemakers", "cardiology", "device-timing", "clinical"]
categories: ["Device Technical"]
showTableOfContents: true
---

Understanding how different cardiac device manufacturers handle pacing timing is critical for optimal programming, troubleshooting, and interpretation of device electrograms (EGMs). At a fundamental level, pacemakers track time to determine when to deliver a pacing pulse or when to inhibit pacing based on intrinsic cardiac activity.

However, manufacturers implement these timing architectures differently—primarily categorizing them into **Atrial-Based Timing** and **Ventricular-Based Timing** schemes. This article presents a clinical comparison of major pacing systems from **Abbott**, **Biotronik**, **Boston Scientific**, **Medtronic**, and **MicroPort**.

---

## Atrial-Based vs. Ventricular-Based Timing

Before diving into manufacturer-specific implementations, let's clarify the key difference between these two paradigms:

> [!NOTE]
>
> - **Atrial-Based Timing (A-A Interval):** The pacemaker calculates pacing intervals based on the atrial cycle. The ventricular channel is essentially "slaved" to the atrial events. This architecture prioritizes preserving intrinsic AV conduction and physiological pacing intervals.
> - **Ventricular-Based Timing (V-V Interval):** The pacemaker calculates pacing intervals based on ventricular events. Atrial pacing is scheduled backward from the preceding ventricular event, meaning the ventricular rate remains highly stable, but AV intervals can vary.

---

## Pacing Timing System Comparison by Manufacturer

The following table summarizes how each major manufacturer handles timing architectures across different pacing modes:

| Manufacturer                            | Timing System Architecture                                                          | Clinical Behavior & Mode Exceptions                                                                                                                                                                                 |
| :-------------------------------------- | :---------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Abbott** (formerly St. Jude)          | **Ventricular-based** in specific dual-chamber states; **Atrial-based** by default. | **Ventricular-based** for `VDD` & `DDI` modes, and during `DDD` when $PV > MTR$.<br>**Atrial-based** for `DOO`, `DDD` modes, or when $PV < MTR$.                                                                    |
| **Biotronik**                           | **Atrial-based** by default for dual-chamber modes.                                 | Uses **Atrial-based** timing for `DDD` mode.<br>**Ventricular-based** timing is used for `DDI` and `VDI` modes, though exceptions apply during specific events like PACs, PVCs, or Ventricular Safety Pacing (VSP). |
| **Boston Scientific**                   | **Atrial-based**                                                                    | Uses **Atrial-based** timing in `DDD` mode to prioritize physiological AV synchrony.                                                                                                                                |
| **Medtronic**                           | **Atrial-based**                                                                    | **Atrial-based** timing is utilized for all devices that support atrial pacing (`DDD`, `DDI`, `DVI`, not `VDI`/`VDIR`). May shorten VA timing to provide consistent A-A intervals.                                  |
| **MicroPort** (formerly Livanova/Sorin) | **Atrial-based** and **Ventricular-based**                                          | **Atrial-based** for `DDD`. **Ventricular-based** for `VDD`, `DDI`, and `DDD` when $PV > MTR$. PVCs reset clocks and add a 500 ms atrial refractory period.                                                         |

---

## Detailed Manufacturer Implementation

### Abbott

Abbott devices exhibit a dynamic shift in timing architecture depending on the active state. By default in standard `DDD` pacing, they utilize **atrial-based** timing. However, when the programmed Max Tracking Rate (MTR) is exceeded, or when in tracking modes like `VDD` or non-tracking modes like `DDI`, the device dynamically transitions to **ventricular-based** timing.

### Biotronik

Biotronik utilizes a highly responsive **atrial-based** timing scheme in `DDD`. However, to prevent inappropriate ventricular tracking of rapid atrial events, it switches to **ventricular-based** timing during `DDI` and `VDI`. Additionally, complex algorithms modify this behavior during premature atrial contractions (PACs), premature ventricular contractions (PVCs), and ventricular safety pacing (VSP).

### Medtronic

Medtronic maintains a highly consistent **atrial-based** timing structure across all dual-chamber modes that include atrial pacing (`DDD`, `DDI`, `DVI`, but not `VDI`/`VDIR`). This maintains stable A-A intervals, keeping the physiological pace intact across mode transitions and reducing the risk of pacemaker-mediated tachycardia (PMT) when paired with modern search AV algorithms. Medtronic devices may shorten the VA timing due to a shortened AV delay to provide a consistent A-A interval, which may cause the V-V interval to be less than the Lower Rate Limit (LRL). This is calculated as `60,000 / (lower rate interval + PAV - measured AV)`.

### MicroPort

MicroPort (formerly Livanova/Sorin) utilizes **atrial-based** timing for `DDD` mode. However, they switch to **ventricular-based** timing if the mode is `VDD`, `DDI`, or `DDD` when PV > MTR. Additionally, PVCs (defined as ventricular events not preceded by an atrial event) will reset all clocks and automatically add a nonprogrammable 500 ms atrial refractory period to prevent pacemaker-mediated tachycardia.

---

## Clinical Glossary

- **PV (P-Wave to Ventricular Pace):** P-wave synchronous ventricular pacing interval.
- **MTR (Max Tracking Rate):** The maximum rate at which the ventricles can be paced in response to sensed atrial activity.
- **VSP (Ventricular Safety Pacing):** A short sensing window triggered by an atrial pace, preventing cross-talk inhibition by pacing the ventricle early if noise is detected.
- **PAC (Premature Atrial Contraction):** An early heartbeat originating in the atria.
- **PVC (Premature Ventricular Contraction):** An early heartbeat originating in the ventricles.
- **LRL (Lower Rate Limit):** The lowest heart rate the pacemaker will allow before delivering a pacing pulse.
- **PAV (Paced AV Delay):** The programmed delay between an atrial paced event and the scheduled ventricular paced event.

---

{{< pacemaker-sim >}}
