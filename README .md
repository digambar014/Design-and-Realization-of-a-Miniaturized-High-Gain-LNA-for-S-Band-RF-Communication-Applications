# Design and Realization of a Miniaturized High-Gain LNA for S-Band RF Communication Applications

![Technology](https://img.shields.io/badge/Technology-0.18%20%C2%B5m%20CMOS-blue)
![Band](https://img.shields.io/badge/Band-S--Band%202025%E2%80%932110%20MHz-green)
![Topology](https://img.shields.io/badge/Topology-Cascode%20CS-orange)
![Tool](https://img.shields.io/badge/Tool-Cadence%20Virtuoso-red)
![Status](https://img.shields.io/badge/Status-Post--Layout%20Verified-brightgreen)

A miniaturized, high-gain **Low Noise Amplifier (LNA)** for the **S-Band (2025–2110 MHz)**, designed in **0.18 µm CMOS** using a **cascode common-source topology with inductive source degeneration**. The design was carried out in Cadence Virtuoso and verified through pre-layout and post-layout simulations, including all process corners.

> Minor Project · Department of Electronics & Communication Engineering · GLA University, Mathura · Session 2025–26

---

## Table of Contents

- [Overview](#overview)
- [Key Results](#key-results)
- [Why an LNA?](#why-an-lna)
- [Topology Selection](#topology-selection)
- [Proposed Design](#proposed-design)
- [Design Equations](#design-equations)
- [Simulation Results](#simulation-results)
- [Performance Summary](#performance-summary)
- [Advantages and Limitations](#advantages-and-limitations)
- [Future Scope](#future-scope)
- [Tools Used](#tools-used)
- [Team](#team)
- [Acknowledgement](#acknowledgement)

---

## Overview

A Low Noise Amplifier amplifies very weak RF signals while adding as little noise as possible. It is the first active element after the antenna/band-pass filter in an RF receiver chain, so its noise figure and gain largely decide the sensitivity of the whole receiver. LNAs are critical in satellite communications, GPS receivers, radar and 5G base stations.

This project targets **S-Band (2025–2110 MHz)** and aims for:

| Goal | Target |
|---|---|
| Power gain (S21) | ≥ 45 dB |
| Noise figure (NF) | ≤ 1.2 dB |
| Input match (S11) | ≤ −10 dB |
| Output match (S22) | ≤ −10 dB |
| Reverse isolation (S12) | ≤ −30 dB |
| Stability | Unconditional (K > 1, \|Δ\| < 1) |
| Size | Miniaturized |

## Key Results

| Metric | Result |
|---|---|
| Peak gain (S21) | **53.23 dB** |
| Noise figure | **1.51 – 1.74 dB** (minimum 1.25 dB at 1.6–1.7 GHz) |
| Input match (S11) | −42 to −5 dB (≤ −10 dB at band centre) |
| Output match (S22) | **−12.75 dB** |
| Reverse isolation (S12) | **< −48 dB** |
| Chip area | **0.637 × 0.402 mm²** |
| Supply voltage | 1.8 V |
| Process corners | TT / FF / SS / FS / SF — all pass |

## Why an LNA?

<p align="center"><b>Antenna → BPF → LNA → Mixer → IF BPF → ADC</b> &nbsp;(LO feeds the mixer)</p>

The Friis noise formula shows why the first stage matters most:

```
F_total = F1 + (F2 − 1)/G1 + (F3 − 1)/(G1·G2) + ...
```

- A **high LNA gain (G1)** suppresses the noise contribution of all subsequent stages.
- A **low LNA noise figure (F1)** directly sets the receiver sensitivity.

## Topology Selection

| Parameter | CS | CG | Source Degen. | Inductive Degen. | **Cascode (selected)** |
|---|---|---|---|---|---|
| Gain | High | Moderate | Moderate | High | **Very High** |
| Noise Figure | Mod–High | Low–Mod | Moderate | Very Low | **Low** |
| Input Match | Difficult | Easy | Moderate | Excellent | **Excellent** |
| Stability | Moderate | High | High | High | **Very High** |
| Linearity | Moderate | Good | Good | Very Good | **Excellent** |

**Selected:** Cascode CS with inductive source degeneration for maximum gain, isolation and low noise figure.

## Proposed Design

### Schematic

![Cadence schematic of the proposed LNA](images/schematic.jpg)

*Cadence Virtuoso schematic of the proposed S-Band LNA (0.18 µm CMOS).*

### Design Parameters

| Component | Value |
|---|---|
| M1, M2 (W/L) | 540 µm / 0.18 µm |
| M3 bias (W/L) | 70 µm / 0.18 µm |
| L1 – gate inductor | 7.8 nH |
| L2 – source inductor | 600 pH |
| L3 – tank inductor | 2.5 nH |
| C1 – input capacitor | 1.5 pF |
| C2 – tank capacitor | 2 pF |
| R1 / R2 | 1 kΩ / 10 kΩ |
| Vbias / VDD | 0.6 V / 1.8 V |
| Technology | 0.18 µm CMOS |
| Frequency | 2025 – 2110 MHz |

**Biasing:** current mirror with M3 (70 µm / 0.18 µm), Vbias = 0.6 V and an R1 = 1 kΩ / R2 = 10 kΩ divider. The cascode transistor's gate is held at VDD = 1.8 V.

## Design Equations

**Input matching network (inductive source degeneration)**

```
Re(Zin) = ωT · Ls,        ωT = gm / Cgs
Ls = 600 pH  →  Re(Zin) = 50 Ω  (noiseless real-part match)
f0 = 1 / (2π · √[(Lg + Ls) · Cgs]),   Lg = 7.8 nH  →  f0 in S-Band
```

**Output tank network**

```
f_tank = 1 / (2π · √(L3 · C2)),   L3 = 2.5 nH, C2 = 2 pF
f_tank ≈ 2.06 GHz
```

At resonance the tank presents maximum impedance, giving maximum voltage swing and therefore maximum power gain (S21).

## Simulation Results

### Pre-layout S-parameters

| Gain (S21) | Output match (S22) |
|:---:|:---:|
| ![S21](images/s21.png) | ![S22](images/s22.png) |

| Input match (S11) | Reverse isolation (S12) |
|:---:|:---:|
| ![S11](images/s11.png) | ![S12](images/s12.png) |

### Post-layout simulation

![Post-layout simulation](images/post_layout.png)

Layout is complete, and post-layout simulation confirms design integrity under parasitic effects.

## Performance Summary

| Parameter | Target | Pre-Layout | Post-Layout |
|---|---|---|---|
| Frequency band | 2025–2110 MHz | 2025–2110 MHz | 2025–2110 MHz |
| Peak S21 gain | ≥ 45 dB | 53.23 dB ✅ | ~50 dB |
| Noise figure | ≤ 1.2 dB | 1.51–1.74 dB | ~1.6–1.9 dB |
| S11 input match | ≤ −10 dB | −42 to −5 dB ✅ | ≤ −10 dB ✅ |
| S22 output match | ≤ −10 dB | −12.75 dB ✅ | ≤ −10 dB ✅ |
| S12 isolation | ≤ −30 dB | < −48 dB ✅ | < −45 dB ✅ |
| Chip area | Miniaturized | 0.637 × 0.402 mm² | 0.637 × 0.402 mm² |
| Technology | 0.18 µm CMOS | 0.18 µm CMOS | 0.18 µm CMOS |

## Advantages and Limitations

**Advantages**

- Very high gain (53.23 dB) suppresses noise from downstream stages
- Excellent reverse isolation (< −48 dB)
- Noiseless 50 Ω input matching through inductive degeneration
- Compact 0.637 × 0.402 mm² footprint, suitable for satellite payloads
- Standard CMOS, co-integrable with digital circuits
- Robust across all process corners (TT / FF / SS / FS / SF)

**Limitations**

- NF of 1.51–1.74 dB is slightly above the ≤ 1.2 dB target
- Narrowband: the LC tank restricts operation to the S-Band
- On-chip inductors dominate area and limit Q-factor
- IIP3 / P1dB linearity not yet fully characterized
- Silicon fabrication and measurement still pending
- Post-layout parasitics slightly reduce gain and NF

## Future Scope

1. **Fabrication (MPW):** submit for a Multi-Project Wafer run and perform on-wafer RF testing with a VNA.
2. **Linearity testing:** full IIP3 and P1dB characterization in simulation and silicon.
3. **NF optimization:** improve spiral inductor Q to reach NF ≤ 1.2 dB.
4. **Receiver front-end:** integrate the LNA with a mixer and VCO into a complete RF receiver.
5. **Wideband LNA:** cover full S-Band (2–4 GHz) using a noise-cancelling topology.
6. **0.13 µm migration:** port to a finer process for higher fT, lower NF and smaller area.

## Tools Used

- **Cadence Virtuoso** – schematic capture, simulation and layout
- **0.18 µm CMOS PDK** – device models and process corners

## Repository Structure

```
.
├── README.md
└── images/
    ├── schematic.jpg
    ├── s11.png
    ├── s12.png
    ├── s21.png
    ├── s22.png
    └── post_layout.png
```

## Team

| Name | Roll No. |
|---|---|
| Digambar Singh | 2313200005 |
| Kuldeep | 2313200011 |
| Shyam Baghel | 2313200017 |
| Harish Chaudhary | 2315000889 |

## Acknowledgement

**Project Guide:** Dr. Abhay Chaturvedi, Associate Professor, Department of ECE, GLA University, Mathura, India.

---

<p align="center"><i>Department of Electronics & Communication Engineering · GLA University · Session 2025–26</i></p>
