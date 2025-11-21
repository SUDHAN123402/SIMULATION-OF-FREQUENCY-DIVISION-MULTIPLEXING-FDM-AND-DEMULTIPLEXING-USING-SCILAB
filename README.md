# SIMULATION-OF-FREQUENCY-DIVISION-MULTIPLEXING-FDM-AND-DEMULTIPLEXING-USING-SCILAB
## AIM:

To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.

## EQUIPMENTS Needed

Computer with Scilab installed

## ALGORITHM

1.Define six different frequencies to generate six sine wave signals.
2.Generate the time vector to represent time samples.
3.Compute six sine signals for each frequency over the time vector.
4.Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.
5.Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.
6.Plot original signals, multiplexed signal, and demultiplexed signals for verification.

## PROCEDURE

Refer Algorithms and write code for the experiment.
• Open SCILAB in System
• Type your code in New Editor
• Save the file
• Execute the code
• If any Error, correct it in code and execute again
• Verify the generated waveform using Tabulation and Model Waveform

## PROGRAM
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

fs = 100000
t = np.arange(0, 0.01, 1/fs)

# Message & carrier frequencies
fm = [100, 200, 300, 400]
fc = [5000, 10000, 15000, 20000]

# Message signals
m = [0.5*np.sin(2*np.pi*f*t) for f in fm]

# Modulated DSB-SC signals
s = [m[i] * np.cos(2*np.pi*fc[i]*t) for i in range(4)]

# FDM combined
fdm = sum(s)

# Low-pass filter
def lpf(x, cutoff):
    b,a = butter(5, cutoff/(fs/2), 'low')
    return filtfilt(b,a,x)

# Demodulation + LPF recovery
rec = [ lpf(fdm * (2*np.cos(2*np.pi*fc[i]*t)), fm[i]*2) for i in range(4) ]

# ----------------- PLOTTING -----------------
plt.figure(figsize=(13,13))

# FDM
plt.subplot(8,1,1); plt.plot(t, fdm, 'k'); plt.title("FDM - Multiplexed Signal")

# CH0
plt.subplot(8,1,2); plt.plot(t, s[0], 'r'); plt.title("CH0 - Modulated Signal")
plt.subplot(8,1,3); plt.plot(t, rec[0], 'r'); plt.title("CH0 - Recovered Signal")

# CH1
plt.subplot(8,1,4); plt.plot(t, s[1], 'g'); plt.title("CH1 - Modulated Signal")
plt.subplot(8,1,5); plt.plot(t, rec[1], 'g'); plt.title("CH1 - Recovered Signal")

# CH2
plt.subplot(8,1,6); plt.plot(t, s[2], 'b'); plt.title("CH2 - Modulated Signal")
plt.subplot(8,1,7); plt.plot(t, rec[2], 'b'); plt.title("CH2 - Recovered Signal")

# CH3 (Recovered Only)
plt.subplot(8,1,8); plt.plot(t, rec[3], 'm'); plt.title("CH3 - Recovered Signal")

plt.tight_layout()
plt.show()
```

## TABULATION:
![WhatsApp Image 2025-11-21 at 23 16 43](https://github.com/user-attachments/assets/cb582403-e437-4ed9-a046-cff0cc2f32c1)


## GRAPH:
<img width="1289" height="1289" alt="image" src="https://github.com/user-attachments/assets/55ef2c9d-a331-443d-b571-fffb137e2a2e" />

## RESULT:
Thus the Frequency division multiplexing is done experimentally and output is verified


