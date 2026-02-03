# EXP 1(C) : Analysis of audio signal for noise removal

# AIM: 

# To analyse an audio signal and remove noise

# APPARATUS REQUIRED:  
PC installed with Python. 

# PROGRAM:
```
# -----------------------------
# 1. Import Libraries
# -----------------------------
import numpy as np
import matplotlib.pyplot as plt
from scipy.io import wavfile
from IPython.display import Audio
from google.colab import files

# -----------------------------
# 2. Upload audio files
# -----------------------------
print("Upload clean audio file:")
uploaded_clean = files.upload()
clean_file = list(uploaded_clean.keys())[0]

print("Upload noise audio file:")
uploaded_noise = files.upload()
noise_file = list(uploaded_noise.keys())[0]

# -----------------------------
# 3. Read audio files
# -----------------------------
Fs_clean, clean_audio = wavfile.read(clean_file)
Fs_noise, noise_audio = wavfile.read(noise_file)

# Ensure mono audio
if clean_audio.ndim > 1:
    clean_audio = clean_audio[:, 0]
if noise_audio.ndim > 1:
    noise_audio = noise_audio[:, 0]

# Normalize both
clean_audio = clean_audio / np.max(np.abs(clean_audio))
noise_audio = noise_audio / np.max(np.abs(noise_audio))

# Make both audio same length
min_len = min(len(clean_audio), len(noise_audio))
clean_audio = clean_audio[:min_len]
noise_audio = noise_audio[:min_len]

# -----------------------------
# 4. Mix audio with noise
# -----------------------------
noise_level = 0.3  # adjust noise intensity (0-1)
noisy_audio = clean_audio + noise_level * noise_audio
noisy_audio = noisy_audio / np.max(np.abs(noisy_audio))  # normalize

# Play noisy audio
print("Playing noisy audio:")
Audio(noisy_audio, rate=Fs_clean)

# Plot noisy audio
plt.figure(figsize=(12,3))
plt.plot(noisy_audio)
plt.title("Noisy Audio")
plt.xlabel("Sample index")
plt.ylabel("Amplitude")
plt.grid()
plt.show()

# -----------------------------
# 5. Remove noise using FFT thresholding
# -----------------------------
N = len(noisy_audio)
X = np.fft.fft(noisy_audio)

# Simple thresholding (frequency-domain filtering)
threshold = 0.1 * np.max(np.abs(X))
X_filtered = np.where(np.abs(X) > threshold, X, 0)

# Inverse FFT to get denoised signal
denoised_audio = np.fft.ifft(X_filtered).real
denoised_audio = denoised_audio / np.max(np.abs(denoised_audio))  # normalize

# Play denoised audio
print("Playing denoised audio:")
Audio(denoised_audio, rate=Fs_clean)

# Plot denoised audio
plt.figure(figsize=(12,3))
plt.plot(denoised_audio)
plt.title("Denoised Audio")
plt.xlabel("Sample index")
plt.ylabel("Amplitude")
plt.grid()
plt.show()
```
# RESULT: 

<img width="1027" height="316" alt="NOISY" src="https://github.com/user-attachments/assets/bea6400e-cf6d-4640-9c66-872f97b37090" />

<img width="1027" height="316" alt="DENOISED" src="https://github.com/user-attachments/assets/484e2d1f-a32f-4b58-b190-ce0ec2521f5a" />

