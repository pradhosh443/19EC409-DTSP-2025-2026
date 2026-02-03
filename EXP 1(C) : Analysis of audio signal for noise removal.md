# EXP 1(C) : Analysis of audio signal for noise removal

# AIM: 

# To analyse an audio signal and remove noise

# APPARATUS REQUIRED:  
PC installed with Python. 

# PROGRAM:
```
# ---------------------------------------
# 1. Import Libraries
# ---------------------------------------
import numpy as np
import matplotlib.pyplot as plt
from scipy.io import wavfile
from scipy.io.wavfile import WavFileWarning, write
from IPython.display import Audio
from google.colab import files
import warnings
import os

# Suppress WAV warnings
warnings.filterwarnings("ignore", category=WavFileWarning)

# ---------------------------------------
# 2. Upload audio files
# ---------------------------------------
print("Upload clean audio file:")
uploaded_clean = files.upload()
clean_file = list(uploaded_clean.keys())[0]

print("Upload noise audio file:")
uploaded_noise = files.upload()
noise_file = list(uploaded_noise.keys())[0]

# ---------------------------------------
# 3. Read audio files
# ---------------------------------------
Fs_clean, clean_audio = wavfile.read(clean_file)
Fs_noise, noise_audio = wavfile.read(noise_file)

# Ensure mono audio
if clean_audio.ndim > 1:
    clean_audio = clean_audio[:, 0]
if noise_audio.ndim > 1:
    noise_audio = noise_audio[:, 0]

# Normalize
clean_audio = clean_audio / np.max(np.abs(clean_audio))
noise_audio = noise_audio / np.max(np.abs(noise_audio))

# Make same length
min_len = min(len(clean_audio), len(noise_audio))
clean_audio = clean_audio[:min_len]
noise_audio = noise_audio[:min_len]

# ---------------------------------------
# 4. Mix audio with noise
# ---------------------------------------
noise_level = 0.3  # adjust noise intensity
noisy_audio = clean_audio + noise_level * noise_audio
noisy_audio = noisy_audio / np.max(np.abs(noisy_audio))  # normalize

# ---------------------------------------
# 5. Play and save noisy audio
# ---------------------------------------
print("Playing noisy audio:")
Audio(noisy_audio, rate=Fs_clean)

# Save noisy audio
write("noisy_audio.wav", Fs_clean, (noisy_audio * 32767).astype(np.int16))
print("Noisy audio saved as 'noisy_audio.wav'")

# Plot noisy audio waveform
plt.figure(figsize=(12,3))
plt.plot(noisy_audio)
plt.title("Noisy Audio Waveform")
plt.xlabel("Sample index")
plt.ylabel("Amplitude")
plt.grid()
plt.show()

# ---------------------------------------
# 6. Denoise using FFT thresholding
# ---------------------------------------
N = len(noisy_audio)
X = np.fft.fft(noisy_audio)

# Simple frequency thresholding
threshold = 0.1 * np.max(np.abs(X))
X_filtered = np.where(np.abs(X) > threshold, X, 0)

# Inverse FFT
denoised_audio = np.fft.ifft(X_filtered).real
denoised_audio = denoised_audio / np.max(np.abs(denoised_audio))

# ---------------------------------------
# 7. Play and save denoised audio
# ---------------------------------------
print("Playing denoised audio:")
Audio(denoised_audio, rate=Fs_clean)

write("denoised_audio.wav", Fs_clean, (denoised_audio * 32767).astype(np.int16))
print("Denoised audio saved as 'denoised_audio.wav'")

# Plot denoised audio waveform
plt.figure(figsize=(12,3))
plt.plot(denoised_audio)
plt.title("Denoised Audio Waveform")
plt.xlabel("Sample index")
plt.ylabel("Amplitude")
plt.grid()
plt.show()

# ---------------------------------------
# 8. Plot frequency spectra (optional)
# ---------------------------------------
freq = np.fft.fftfreq(N, d=1/Fs_clean)

plt.figure(figsize=(12,4))
plt.plot(freq[:N//2], np.abs(X[:N//2]))
plt.title("Magnitude Spectrum of Noisy Audio")
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")
plt.grid()
plt.show()

plt.figure(figsize=(12,4))
plt.plot(freq[:N//2], np.abs(X_filtered[:N//2]))
plt.title("Magnitude Spectrum of Denoised Audio")
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")
plt.grid()
plt.show()
```
# RESULT: 

<img width="1027" height="316" alt="NOISY" src="https://github.com/user-attachments/assets/bea6400e-cf6d-4640-9c66-872f97b37090" />

<img width="1027" height="316" alt="DENOISED" src="https://github.com/user-attachments/assets/484e2d1f-a32f-4b58-b190-ce0ec2521f5a" />

