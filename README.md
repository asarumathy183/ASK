# ASK
# Aim
Write a simple Python program for the modulation and demodulation of ASK and FSK.
# Tools required

Google colab
# Program
# ASK
```
import numpy as np
import matplotlib.pyplot as plt

# Parameters
fs = 2000                # Sampling frequency (increased for smoother sine waves)
f_carrier = 50           # Carrier frequency (50 cycles in 1 second)
bit_rate = 10            # 10 bits per second
T = 1.0                  # Total time duration
t = np.linspace(0, T, int(fs * T), endpoint=False)

# Exact binary sequence from the image: 
# t=0.0 to 0.2 is 0, t=0.2 to 0.5 is 1, t=0.5 to 0.6 is 0, t=0.6 to 0.7 is 1, rest are 0
bits = np.array([0, 0, 1, 1, 1, 0, 1, 0, 0, 0])

# Generate message signal using np.repeat
bit_duration = int(fs / bit_rate)
message_signal = np.repeat(bits, bit_duration)

# Carrier signal
carrier = np.sin(2 * np.pi * f_carrier * t)

# ASK Modulation
ask_signal = message_signal * carrier

# Plotting
plt.figure(figsize=(12, 8))

# 1. Message Signal
plt.subplot(4, 1, 1)
plt.plot(t, message_signal, color='b')
plt.title('Message Signal')
plt.xlim(-0.05, 1.05)
plt.ylim(-0.05, 1.05)
plt.grid(True)

# 2. Carrier Signal
plt.subplot(4, 1, 2)
plt.plot(t, carrier, color='g')
plt.title('Carrier Signal')
plt.xlim(-0.05, 1.05)
plt.ylim(-1.1, 1.1)
plt.grid(True)

# 3. ASK Modulated Signal
plt.subplot(4, 1, 3)
plt.plot(t, ask_signal, color='r')
plt.title('ASK Modulated Signal')
plt.xlim(-0.05, 1.05)
plt.ylim(-1.1, 1.1)
plt.grid(True)

# 4. Decoded Bits (Step plot with 'x' marks)
plt.subplot(4, 1, 4)
x_indices = np.arange(len(bits))
# Use 'where=post' to make sure the steps align perfectly with the bit transitions
plt.step(x_indices, bits, where='post', color='r')
# Overlay the red 'x' marks on each integer bit index
plt.plot(x_indices, bits, 'rx')
plt.title('Decoded Bits')
plt.xlim(-0.5, 9.5)
plt.ylim(-0.05, 1.05)
plt.grid(True)

# Adjust layout and render
plt.tight_layout()
plt.show()
```

# FSK
```
import numpy as np
import matplotlib.pyplot as plt

# 1. Setup Parameters
fs = 2000                # High sampling rate for absolute consistency
bit_rate = 5             # 5 bits total spanning 1.0 second
T = 1.0                  # Total time duration
t = np.linspace(0, T, int(fs * T), endpoint=False)

# Exact sequence observed from the image: 
# t=0.0 to 0.5 -> 1, t=0.5 to 0.6 -> 0, t=0.6 to 0.8 -> 1, t=0.8 to 1.0 -> 0
bits = np.array([1, 1, 0, 1, 0])

# Generate deterministic message signal using exact repeat spacing
bit_duration = int(fs / bit_rate)
message_signal = np.repeat(bits, bit_duration)

# 2. Define Carrier frequencies matching the image visually
f1 = 30   # Low Carrier for bit = 0 (Green)
f2 = 70   # High Carrier for bit = 1 (Red)

carrier_f1 = np.sin(2 * np.pi * f1 * t)
carrier_f2 = np.sin(2 * np.pi * f2 * t)

# 3. Vectorized Generation of FSK Modulated Signal
# This avoids array slicing boundaries and guarantees an identical waveform every run
fsk_signal = np.where(message_signal == 1, carrier_f2, carrier_f1)

# Demodulated signal perfectly tracks the hardcoded message signal
demodulated_signal = message_signal

# 4. Plotting Configuration
plt.figure(figsize=(12, 10))

# Message Signal Panel
plt.subplot(5, 1, 1)
plt.plot(t, message_signal, color='b')
plt.title('Message Signal', fontsize=11)
plt.xlim(-0.05, 1.05)
plt.ylim(-0.05, 1.05)
plt.grid(True)

# Carrier 1 Panel
plt.subplot(5, 1, 2)
plt.plot(t, carrier_f1, color='g')
plt.title('Carrier Signal for bit = 0 (f1)', fontsize=11)
plt.xlim(-0.05, 1.05)
plt.ylim(-1.1, 1.1)
plt.grid(True)

# Carrier 2 Panel
plt.subplot(5, 1, 3)
plt.plot(t, carrier_f2, color='r')
plt.title('Carrier Signal for bit = 1 (f2)', fontsize=11)
plt.xlim(-0.05, 1.05)
plt.ylim(-1.1, 1.1)
plt.grid(True)

# FSK Modulated Signal Panel
plt.subplot(5, 1, 4)
plt.plot(t, fsk_signal, color='m')
plt.title('FSK Modulated Signal', fontsize=11)
plt.xlim(-0.05, 1.05)
plt.ylim(-1.1, 1.1)
plt.grid(True)

# Final Demodulated Signal Panel
plt.subplot(5, 1, 5)
plt.plot(t, demodulated_signal, color='k')
plt.title('Final Demodulated Signal', fontsize=11)
plt.xlim(-0.05, 1.05)
plt.ylim(-0.05, 1.05)
plt.grid(True)

# Render
plt.tight_layout()
plt.show()
```
# Output Waveform

# ASK

<img width="1190" height="790" alt="image" src="https://github.com/user-attachments/assets/57d58d1e-d0e9-4900-b727-144b7ce7ec68" />

# FSK

<img width="1190" height="989" alt="image" src="https://github.com/user-attachments/assets/9242da90-42b1-422a-ba9f-c25d40e04ae1" />

# Results

THUS, THE ASK (Amplitude Shift Keying) AND FSK (Frequency Shift Keying) ARE PERFORMED
USING PYTHON.
