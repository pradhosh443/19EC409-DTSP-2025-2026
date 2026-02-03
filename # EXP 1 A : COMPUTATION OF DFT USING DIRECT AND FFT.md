# EXP 1 A : COMPUTATION OF DFT USING DIRECT AND FFT

# AIM: 

# To Obtain DFT and FFT of a given sequence in SCILAB. 

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
// DISCRETE FOURIER TRANSFORM 
```
clc;
clear;
close;
x = [1 1 1 1 0 0 0 0];
N = length(x);
X = zeros(1, N);

for k = 0:N-1
    for n = 0:N-1
        X(k+1) = X(k+1) + x(n+1)*exp(-%i*2*%pi*k*n/N);
    end
end

k = 0:N-1;

mag = abs(X);
phase = atan(imag(X), real(X));
figure(1)

subplot(3,1,1)
plot(k, mag, '-o')
xlabel("Frequency index k")
ylabel("|X(k)|")
title("Magnitude Spectrum")
xgrid()

subplot(3,1,2)
plot(k, phase, '-o')
xlabel("Frequency index k")
ylabel("Phase (radians)")
title("Phase Spectrum")
xgrid()
subplot(3,1,3)
plot(k, mag, '-o')
xlabel("Frequency index k")
ylabel("Magnitude")
title("Frequency Spectrum")
xgrid()
```
// FAST FOURIER TRANSFORM
```
clc;
clear;
close;

x = [1 1 1 1 0 0 0 0];
N = length(x);
n = 0:N-1;

X = fft(x);

mag = abs(X);
phase = atan(imag(X), real(X));

x_ifft = ifft(X);

k = 0:N-1;

figure(1)

subplot(4,1,1)
plot(n, x, '-o')
xlabel("n")
ylabel("x(n)")
title("Input Sequence")
xgrid()

subplot(4,1,2)
plot(k, mag, '-o')
xlabel("Frequency index k")
ylabel("|X(k)|")
title("Magnitude Spectrum")
xgrid()

subplot(4,1,3)
plot(k, phase, '-o')
xlabel("Frequency index k")
ylabel("Phase (radians)")
title("Phase Spectrum")
xgrid()
subplot(4,1,4)
plot(n, real(x_ifft), '-o')
xlabel("n")
ylabel("x(n)")
title("Inverse FFT of X(k)")
xgrid()
```
# OUTPUT: 
<img width="1551" height="833" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/72e52247-315f-46c4-83a8-456684c10d7d" />

<img width="1548" height="839" alt="Screenshot (5)" src="https://github.com/user-attachments/assets/9ed602e8-a4af-40c3-9d17-777dd68a93cd" />

# RESULT:
The DFT and FFT of the given input sequence were computed and the magnitude and phase spectra were plotted successfully.
