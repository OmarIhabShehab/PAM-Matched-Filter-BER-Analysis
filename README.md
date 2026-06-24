# 📡 Matched Filter Design & BER Analysis of M-PAM Systems

<div align="center">

![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)
![MATLAB](https://img.shields.io/badge/Tool-MATLAB-orange?style=flat-square)
![Simulink](https://img.shields.io/badge/Tool-Simulink-red?style=flat-square)
![Course](https://img.shields.io/badge/Course-CIE%20237-brightgreen?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)

**Optimal matched filter receiver design and BER/SER performance analysis of 2-PAM and 4-PAM systems over AWGN channels — implemented in MATLAB and validated in Simulink.**

</div>

---

## 📁 Project Structure

```
PAM-Matched-Filter-BER/
│
├── MATLAB/                # MATLAB simulation scripts
├── Simulink/              # Simulink models (.slx files)
├── Report/                # Full technical report (PDF)
└── README.md
```

---

## 📌 Abstract

This project presents a comprehensive study of optimal receiver design for M-ary Pulse Amplitude Modulation (M-PAM) systems over AWGN channels. The matched filter — derived as the optimal linear receiver maximizing SNR at the sampling instant — is analyzed for both **2-PAM** and **4-PAM** using three pulse shaping techniques: rectangular, triangular, and raised cosine. Performance is evaluated via BER, SER, bandwidth efficiency, and noise robustness. MATLAB simulations and Simulink models are cross-validated against theoretical BER expressions, showing excellent agreement.

---

## ⚙️ System Overview

### Transmission Chain
```
Random Bits → PAM Mapping → Upsample → Pulse Shaping → AWGN Channel
                                                              ↓
Detected Bits ← Decision Device ← Sampler ← Matched Filter ←
```

### System Parameters

| Parameter | Value |
|---|---|
| Symbols per run (N) | 30,000 |
| Samples per symbol (Sps) | 8 |
| Raised cosine roll-off (α) | 0.35 |
| Pulse span | 6 symbol periods |
| Eb/N₀ range | −4 dB to 12 dB (2 dB steps) |
| Modulation orders | M = 2, M = 4 |

---

## 📐 Theoretical Background

### M-PAM Constellation
Each group of k = log₂(M) bits is mapped to one of M amplitude levels with normalized average symbol energy.

### Matched Filter
The optimal linear filter maximizing output SNR at sampling time Tₛ:
- **Impulse response:** h(t) = p(Tₛ − t)
- **Peak SNR:** 2Eₛ/N₀ (independent of pulse shape)
- **Implementation:** Linear convolution with time-reversed pulse + sampling at peak

### Pulse Shapes

| Pulse | Spectral Properties | ISI |
|---|---|---|
| Rectangular | Sinc spectrum, high sidelobes | ISI-free at symbol rate |
| Triangular | Faster spectral decay | Moderate ISI |
| Raised Cosine (α=0.35) | Nyquist zero-ISI criterion ✅ | Zero ISI |

### BER Formulas

| Modulation | BER Expression |
|---|---|
| 2-PAM | Pb(e) = Q(√(2Eb/N₀)) |
| 4-PAM | Pₛ(e) = (3/2)Q(√(4Eb/N₀/5)), BER ≈ Pₛ(e)/2 |

---

## 📊 Results Summary

### 2-PAM BER Performance
- All three pulse shapes closely track the theoretical Q-function bound
- Raised cosine achieves tightest agreement with theory
- At Eb/N₀ = 8 dB → BER ≈ 10⁻³–10⁻⁴

### 4-PAM BER Performance
- Requires **5–7 dB higher Eb/N₀** than 2-PAM for equivalent BER
- Consistent with theoretical penalty of 10·log₁₀(5) ≈ 7 dB
- Raised cosine outperforms rectangular and triangular pulses

### MATLAB vs Simulink
- Strong quantitative BER agreement across all configurations
- Minor discrepancies at high SNR due to Monte Carlo variance (N = 30,000)

---

## 🔬 Key Conclusions

- ✅ Matched filter confirmed as optimal AWGN receiver — BER tracks Q-function bounds across all pulse shapes
- ✅ Raised cosine (α = 0.35) yields best BER — Nyquist ISI-free property eliminates inter-symbol contamination
- ✅ 4-PAM doubles spectral efficiency but requires ~7 dB SNR penalty vs 2-PAM
- ✅ MATLAB and Simulink cross-validated — both methodologies consistent

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| MATLAB | Analytical simulation, BER/SER curves, pulse design |
| Simulink | Block-diagram implementation & cross-validation |
| Signal Processing Toolbox | Filter design & analysis |

---

## 🚀 How to Run

### MATLAB
```matlab
% Run main simulation script
run('main_simulation.m')
% Generates BER/SER curves for 2-PAM and 4-PAM
```

### Simulink
```matlab
% Open 2-PAM model
open('CIE237_FINAL_STABLE123.slx')

% Open 4-PAM model
open('CIE237_4PAMS.slx')
```

---

## 👥 Team

| Name | ID | Contribution |
|---|---|---|
| Mustafa Hesham Sallam | 202400624 | MATLAB implementation, theoretical derivations, BER analysis, pulse shaping |
| Omar Ihab Fared Abdo | 202401437 | Simulink models, BER extraction, MATLAB–Simulink comparison, report |

Undergraduate project — Communications & Information Engineering Dept.
**University of Science and Technology, Zewail City**
CIE 237 — Communication Systems | Spring 2026

---

## 📚 References

1. J. G. Proakis and M. Salehi, *Digital Communications*, 5th ed. McGraw-Hill, 2008.
2. S. Haykin, *Communication Systems*, 4th ed. Wiley, 2001.
3. B. P. Lathi and Z. Ding, *Modern Digital and Analog Communication Systems*, 4th ed. OUP, 2009.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
