# DSB--SC-MODULATION-AND-DEMODULATION-USING-PYTHON

__AIM__:

To generate a Double Sideband Suppressed Carrier (DSB-SC) signal in Python (Google Colab), transmit it (optionally add noise), and recover the message using coherent (synchronous) demodulation with a low-pass filter. Observe time and frequency domain waveforms and measure demodulation performance

__APPARATUS REQUIRED__:

Google Colab (or any Python environment)

Python libraries: numpy, matplotlib, scipy (scipy.signal)

__Theory__:

DSB-SC signal: s(t) = m(t) · cos(2πf_c t)
Coherent demodulation: multiply received s(t) by a synchronized carrier cos(2πf_c t) then low-pass filter (LPF) to remove double-frequency components:

r(t) = s(t)·cos(2πf_c t) = m(t)·cos²(2πf_c t) = 0.5 m(t) + 0.5 m(t)·cos(4πf_c t)
LPF extracts 0.5·m(t) → scale by 2 to recover m(t).

__Procedure__:

1) Import libraries and set parameters
2) Define message and carrier signals
3) Generate DSB-SC signal (modulation)
4) View spectra (FFT) of message and DSB-SC
5) (Optional) Add noise
6) Coherent demodulation (multiply by synchronized carrier)
7) Low-pass filter to recover message
   
__Program:__
```
import numpy as np
import matplotlib.pyplot as plt
Ac = 19.8
fc = 5600
Am = 9.9
fm = 560
fs = 70000
t = np.arange(0, 2/fm, 1/fs)
Wm = 2 * np.pi * fm
Wc = 2 * np.pi * fc
Em = Am * np.sin(Wm * t)
Ec = Ac * np.sin(Wc * t)
Edsbsc = ((Am / 2) * np.cos((Wc - Wm) * t)) - ((Am / 2) * np.cos((Wc + Wm) * t))
plt.figure(figsize=(10, 6))
plt.subplot(3, 1, 1)
plt.plot(t, Em)
plt.grid()
plt.subplot(3, 1, 2)
plt.plot(t, Ec)

plt.grid()
plt.subplot(3, 1, 3)
plt.plot(t, Edsbsc)
plt.grid()
plt.tight_layout()
plt.show()
```
 __Tabulation__:

 ![WhatsApp Image 2025-11-23 at 07 17 51_49f7c3a5](https://github.com/user-attachments/assets/74420b90-4586-4c77-beed-ca77d92e8303)
 ![WhatsApp Image 2025-11-23 at 07 20 02_3ee09a8e](https://github.com/user-attachments/assets/a787e7c5-260c-4ebf-bed1-9b6d815f7e8a)


   __Output__:

![WhatsApp Image 2025-11-23 at 07 19 52_f04985ea](https://github.com/user-attachments/assets/b62002d6-9907-4b7e-aa2e-c9a57f32df26)

   
   __Result__:
   ![WhatsApp Image 2025-11-23 at 07 23 50_43c2b618](https://github.com/user-attachments/assets/5e647092-18bd-4b70-90d7-de829b08d73b)

