# EXP 1 : Linear and Circular Convolution

## AIM: 

 To perform Linear and Circular Convolution for two given sequence using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (Linear Convolution): 
```
clc;
clear;
close;
// Given sequences
x = [3 2 1 2];
h = [1 2 1 2];

// Linear Convolution
y_linear = convol(x, h);

// Display result
disp("Linear Convolution Result:");
disp(y_linear);

// Time index
n = 0:length(y_linear)-1;

// Plot using plot()
figure;
plot(n, y_linear, 'o-');   // 'o-' joins points with lines
xlabel("n");
ylabel("Amplitude");
title("Linear Convolution of x(n) and h(n)");
xgrid();
```

## PROGRAM (Circular Convolution): 
```
// Given sequences
clc;
clear;
close;

x = [3 2 1 2];
h = [1 2 1 2];

// Required length
N = length(x) + length(h) - 1;   // N = 7

// Zero padding
x_pad = [x zeros(1, N - length(x))];
h_pad = [h zeros(1, N - length(h))];

// Circular Convolution using FFT (SCILAB syntax)
X = fft(x_pad, -1);   // FFT
H = fft(h_pad, -1);   // FFT
y_circular = fft(X .* H, 1);   // IFFT

// Display result
disp("Circular Convolution Result:");
disp(y_circular);

// Time index
n = 0:length(y_circular)-1;

// Plot
figure;
plot(n, y_circular, 'o-');
xlabel("n");
ylabel("Amplitude");
title("Circular Convolution ");
xgrid();
```


## OUTPUT (Linear Convolution): 
<img width="700" height="100" alt="image" src="https://github.com/user-attachments/assets/7b0b3f53-6ca4-4fc6-a822-24e7b75f88f7" />

<img width="700" height="300" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/17c73856-8021-4049-989a-ac1b97dc19fa" />

## OUTPUT (Circular Convolution): 

<img width="700" height="100" alt="Screenshot 2026-02-07 105235" src="https://github.com/user-attachments/assets/911def27-01e3-4ef9-a517-4a3558ff6f8e" />

<img width="700" height="300" alt="Screenshot (7)" src="https://github.com/user-attachments/assets/19bc2d27-0eeb-4b6b-b14d-e529e19c9479" />

## RESULT: 
Linear and circular convolution of the sequences were successfully performed in SCILAB and
The results were plotted.
