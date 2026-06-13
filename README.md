# matlab-dsp-quantization-analysis
MATLAB simulations analyzing ADC quantization noise, SQNR, and FFT spectrum in Digital Signal Processing.

# DSP Quantization & Noise Analysis via MATLAB

This repository contains a comprehensive Digital Signal Processing (DSP) research project that empirically simulates the effects of quantization and quantization noise using MATLAB. The primary objective is to visually and mathematically validate standard DSP theorems regarding Analog-to-Digital Conversion (ADC) across both the time and frequency domains.

---

## Theoretical Overview

In any digital system, continuous analog signals must be digitized into a finite number of discrete levels. This mapping process inevitably introduces a rounding error known as **Quantization Noise** ($e[n] = x[n] - x_q[n]$). 
* **Quantization Step Size ($\Delta$):** Determined by the formula $\Delta = \frac{2A}{2^B}$, where $A$ is the peak amplitude and $B$ is the bit depth.
* **Theoretical SQNR:** The Signal-to-Quantization-Noise Ratio for a full-scale sine wave is mathematically bounded by the formula: $SQNR \approx 6.02B + 1.76 \text{ (dB)}$.

This project verifies these principles through three extensive MATLAB simulations:

---

## Part 1: SQNR vs. Bit Depth Analysis (Sine Wave)
This simulation evaluates the linear relationship between bit resolution and signal fidelity. The input is a standard normalized sine wave (1 kHz frequency, sampled at 44.1 kHz).

**Key Findings:**
* **2-bit Resolution:** The signal is heavily distorted, forming crude square-like waves with massive quantization error.
* **4-bit Resolution:** The waveform begins to smooth out, but discrete steps are still highly visible.
* **SQNR Validation:** The plotted SQNR curve tracks the theoretical $6.02B + 1.76$ equation with absolute precision, practically demonstrating that every additional bit of resolution reduces the quantization noise power by approximately 6 dB.

### 📸 Simulation 1: Time-Domain & SQNR
| SQNR vs. Bit Depth | 2-Bit Quantization & Error | 4-Bit Quantization & Error |
| :---: | :---: | :---: |
| ![SQNR Plot](images/sqnr_sin.png) | ![2-Bit Wave](images/sin_2bit.png) | ![4-Bit Wave](images/sin_4bit.png) |

---

## 📉 Part 2: Staircase Distortion & Mean Squared Error (MSE)
To explicitly visualize the quantization levels, we applied a uniform quantizer to a linear Ramp signal ranging from -1 to +1. 

**Key Findings:**
* **4-bit Quantization:** The ramp is aggressively discretized into precisely 16 distinct voltage levels, producing a harsh "staircase" effect.
* **8-bit Quantization:** With 256 levels, the staircase steps become microscopic, significantly reducing the Mean Squared Error (MSE).
* **16-bit Quantization:** The quantized signal perfectly overlaps the original analog ramp. The calculated MSE aligns perfectly with the uniform distribution variance model $\sigma_e^2 = \frac{\Delta^2}{12}$.

### 📸 Simulation 2: Ramp Signal Distortion
| 4-Bit Ramp Distortion | 8-Bit Ramp Distortion | 16-Bit Ramp Distortion |
| :---: | :---: | :---: |
| ![Ramp 4-bit](images/ramp_4bit.png) | ![Ramp 8-bit](images/ramp_8bit.png) | ![Ramp 16-bit](images/ramp_16bit.png) |

---

## 📻 Part 3: Frequency Domain Analysis (FFT Spectrum)
To understand the nature of quantization noise, we utilized the Fast Fourier Transform (FFT) to transition from the time domain to the frequency domain. This simulation investigates whether quantization error acts as harmonic distortion or true white noise.

**Key Findings:**
* **4-bit Spectrum:** The noise floor is severely elevated (fluctuating between -40 dB and -60 dB). The error energy is concentrated in distinct, spurious harmonic spikes. The measured SNR is $\approx 26.23$ dB (matching the theoretical $25.84$ dB).
* **8-bit Spectrum:** The noise floor drops drastically by roughly 40-50 dB, settling around -90 to -110 dB. The measured SNR jumps to $\approx 49.96$ dB.
* **16-bit Spectrum:** The noise floor plummets below -150 dB and becomes perfectly flat. This proves that at high bit depths, quantization error loses its correlation with the input signal and behaves identically to an ideal, uniformly distributed white noise.

### 📸 Simulation 3: FFT Noise Floor
| 4-Bit FFT Spectrum | 8-Bit FFT Spectrum | 16-Bit FFT Spectrum |
| :---: | :---: | :---: |
| ![FFT 4-bit](images/fft_4bit.png) | ![FFT 8-bit](images/fft_8bit.png) | ![FFT 16-bit](images/fft_16bit.png) |

---


## 🛠️ Tools & Concepts
* **Environment:** MATLAB
* **Core DSP Concepts:** Uniform Quantization, Fast Fourier Transform (FFT), Signal-to-Quantization-Noise Ratio (SQNR), Mean Squared Error (MSE), Sampling Theory, Noise Floor Analysis.
