# Frequency-Division-Multiplexing---Modulation-and-Demodulation-using-Python

__Aim__:

To generate an FDM signal by multiplexing multiple baseband message signals on different carrier frequencies, transmit (sum) them, optionally add channel noise, then recover each message by bandpass filtering and coherent demodulation in Python (Google Colab). Observe time & frequency domain signals and measure recovery quality.


__Apparatus Required__:

Google Colab (or any Python environment)

Python libraries: numpy, matplotlib, scipy (scipy.signal)


__Theory__:

FDM places different message signals in separate, non-overlapping frequency bands by modulating each message onto a distinct carrier frequency. The multiplexed signal is the sum of all modulated channels. At the receiver, bandpass filters (or tuned filters) isolate each channel; then each isolated carrier is demodulated (coherently multiplied by a synchronized carrier) and low-pass filtered to recover the original baseband.

__Procedure__:

1 — Imports and parameters

2 — Create message signals and carriers

3 — Modulate each message (standard AM DSB-SC) and form FDM signal

4 — Frequency domain (spectrum) of FDM signal

5 — (Optional) Add AWGN noise to FDM signal

6 — Receiver: isolate each channel with bandpass filter

7 — Demodulate each isolated channel (coherent) and low-pass filter to recover baseband
 __Program__:
 ```python
import numpy as np
import matplotlib.pyplot as plt

Am = 10.3
Fm = 400
B  = 5
Ac = 20.6
Fc = 4000
Fs = 40000

T = np.arange(0, 2/Fm, 1/Fs)

em = Am * np.cos(2 * np.pi * Fm * T)

plt.subplot(3, 1, 1)
plt.plot(T, em)
plt.title("Message Signal")
plt.xlabel("Time")
plt.ylabel("Amplitude")
plt.grid()

ec = Ac * np.cos(2 * np.pi * Fc * T)

plt.subplot(3, 1, 2)
plt.plot(T, ec)
plt.title("Carrier Signal")
plt.xlabel("Time")
plt.ylabel("Amplitude")
plt.grid()

efm = Ac * np.cos((2 * np.pi * Fc * T) + (B * np.sin(2 * np.pi * Fm * T)))

plt.subplot(3, 1, 3)
plt.plot(T, efm)
plt.title("FM Signal")
plt.xlabel("Time")
plt.ylabel("Amplitude")
plt.grid()

plt.tight_layout()
plt.show()

```

__Output__:

<img width="1915" height="1006" alt="Screenshot 2026-04-03 231720" src="https://github.com/user-attachments/assets/5b38920d-e209-43a7-8304-5cbc0e5938c1" />


__Result__:

Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.
