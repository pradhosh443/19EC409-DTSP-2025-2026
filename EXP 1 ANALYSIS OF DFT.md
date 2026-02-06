# EXP 1 :  ANALYSIS OF DFT WITH AUDIO SIGNAL

# AIM: 

  To analyze audio signal by removing unwanted frequency. 

# APPARATUS REQUIRED: 
   
   PC installed with SCILAB/Python. 

# PROGRAM: 

// analyze audio signal
```
# ---------------------------------------
# 1. Import required libraries
# ---------------------------------------
import numpy as np
import matplotlib.pyplot as plt
from scipy.io import wavfile
from google.colab import files

# ---------------------------------------
# 2. Upload audio file (.wav)
# ---------------------------------------
uploaded = files.upload()   # Upload a WAV file
filename = list(uploaded.keys())[0]

# ---------------------------------------
# 3. Read audio signal
# ---------------------------------------
Fs, x = wavfile.read(filename)

# If stereo, convert to mono
if x.ndim > 1:
    x = x[:, 0]

# Normalize
x = x / np.max(np.abs(x))

# Use a small segment for DFT (DFT is slow)
N = 1024
x = x[:N]
n = np.arange(N)

# ---------------------------------------
# 4. Plot time-domain signal
# ---------------------------------------
plt.figure(figsize=(12,4))
plt.plot(n/Fs, x)
plt.xlabel("Time (seconds)")
plt.ylabel("Amplitude")
plt.title("Audio Signal (Time Domain)")
plt.grid()
plt.show()

# ---------------------------------------
# 5. Direct DFT computation
# ---------------------------------------
def DFT(x):
    N = len(x)
    X = np.zeros(N, dtype=complex)
    for k in range(N):
        for n in range(N):
            X[k] += x[n] * np.exp(-2j * np.pi * k * n / N)
    return X

X = DFT(x)

# ---------------------------------------
# 6. Frequency axis
# ---------------------------------------
freq = np.arange(N) * Fs / N

# ---------------------------------------
# 7. Magnitude and Phase
# ---------------------------------------
magnitude = np.abs(X)
phase = np.angle(X)

# ---------------------------------------
# 8. Plot magnitude spectrum
# ---------------------------------------
plt.figure(figsize=(12,4))
plt.plot(freq, magnitude)
plt.xlim(0, Fs/2)
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")
plt.title("Magnitude Spectrum (DFT)")
plt.grid()
plt.show()

# ---------------------------------------
# 9. Plot phase spectrum
# ---------------------------------------
plt.figure(figsize=(12,4))
plt.plot(freq, phase)
plt.xlim(0, Fs/2)
plt.xlabel("Frequency (Hz)")
plt.ylabel("Phase (radians)")
plt.title("Phase Spectrum (DFT)")
plt.grid()
<img width="1027" height="393" alt="download (1)" src="https://github.com/user-attachments/assets/f737a338-4911-4320-bb0e-1a4c6942af93" />
plt.show()
```
# OUTPUT: 

<img width="999" height="393" alt="download (2)" src="https://github.com/user-attachments/assets/e2f220be-6f77-4578-9e9e-743515974345" />


<img width="999" height="393" alt="download (1)" src="https://github.com/user-attachments/assets/be5d681b-91bf-49ed-97ad-71c74a134793" />


<img width="999" height="393" alt="download" src="https://github.com/user-attachments/assets/2f7b33fd-f9e0-403d-97e6-f7cf12b1a6ec" />

# RESULTS
Thus, The Analysis of DFT with Audio Signal is Verified.
