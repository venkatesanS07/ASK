# EXP 5 AMPLITUDE SHIFT KEYING
## VENKATESAN S
## 212223060296
## WRITE A SIMPLE ASK PROGRAM USING PHYTON
## AIM
To perform Amplitude Shift Keying{ASK} using Python
## APPARATUS REQUIRED:
Python: A versatile programming language used for scientific computing and signal processing. NumPy: A powerful numerical library in Python for performing array-based operations and mathematical computations. Matplotlib: A plotting library for generating high-quality graphs and visualizations of data, essentialfor demonstrating the sampling process.
## PROGRAM
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter
# Butterworth low-pass filter for demodulation
def butter_lowpass_filter(data, cutoff, fs, order=5):
    nyquist = 0.5 * fs
    normal_cutoff = cutoff / nyquist
    b, a = butter(order, normal_cutoff, btype='low', analog=False)
    return lfilter(b, a, data)
# Parameters
fs = 1000                # Sampling frequency
f_carrier = 50           # Carrier frequency
bit_rate = 10            # Data rate
T = 1                    # Total time duration
t = np.linspace(0, T, int(fs * T), endpoint=False)
# Message signal (binary data)
bits = np.random.randint(0, 2, bit_rate)
bit_duration = fs // bit_rate
message_signal = np.repeat(bits, bit_duration)
# Carrier signal
carrier = np.sin(2 * np.pi * f_carrier * t)
# ASK Modulation
ask_signal = message_signal * carrier
# ASK Demodulation
demodulated = ask_signal * carrier  # Multiply by carrier for coherent detection
filtered_signal = butter_lowpass_filter(demodulated, f_carrier, fs)
decoded_bits = (filtered_signal[::bit_duration] > 0.25).astype(int)
# Plotting
plt.figure(figsize=(12, 8))
plt.subplot(4, 1, 1)
plt.plot(t, message_signal, label='Message Signal (Binary)', color='b')
plt.title('Message Signal')
plt.grid(True)
plt.subplot(4, 1, 2)
plt.plot(t, carrier, label='Carrier Signal', color='g')
plt.title('Carrier Signal')
plt.grid(True)
plt.subplot(4, 1, 3)
plt.plot(t, ask_signal, label='ASK Modulated Signal', color='r')
plt.title('ASK Modulated Signal')
plt.grid(True)
plt.subplot(4, 1, 4)
plt.step(np.arange(len(decoded_bits)), decoded_bits, label='Decoded Bits', color='r', marker='x')
plt.title('Decoded Bits')
plt.tight_layout()
plt.show()
```
## OUTPUT WAVEFORM
![image](https://github.com/user-attachments/assets/f29e540b-f803-4605-aa03-4f9ffbf00d4f)
## Graph
![WhatsApp Image 2025-04-16 at 14 05 12_98dc81f1](https://github.com/user-attachments/assets/98f6372e-686e-49cb-a5e6-6a0fe075ad9f)

## Result
THUS THE ASK (Amplitude Shift Keying) IS PERFORMED USING PYTHON.
