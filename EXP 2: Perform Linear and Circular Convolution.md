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

// Plot using plot2d3() for discrete signal
figure;
plot2d3(n, y_linear);
xlabel("n");
ylabel("Amplitude");
title("Linear Convolution of x(n) and h(n)");
```

## PROGRAM (Circular Convolution): 
```
clc;
clear;
close;

// Original sequences
x = [3 2 1 2];
h = [1 2 1 2];

N = length(x) + length(h) - 1;   // 7

// Zero padding
x = [x zeros(1, N - length(x))];
h = [h zeros(1, N - length(h))];

// Reverse h
h_rev = h($:-1:1);

y = zeros(1, N);

for n = 1:N
    h_rot = [h_rev(N-n+2:N) h_rev(1:N-n+1)];
    y(n) = sum(x .* h_rot);
end

// Fix the one-sample shift
y = [y(2:$) y(1)];

disp("Circular Convolution Result:");
disp(y);

// Plot
n = 0:N-1;
figure;
plot2d3(n, y);
xlabel("n");
ylabel("Amplitude");
title("Circular Convolution");
```


## OUTPUT (Linear Convolution): 
<img width="700" height="100" alt="image" src="https://github.com/user-attachments/assets/7b0b3f53-6ca4-4fc6-a822-24e7b75f88f7" />

<img width="700" height="300" alt="Screenshot (9)" src="https://github.com/user-attachments/assets/94543eb9-b1b7-4b7b-9246-e889b522e052" />


## OUTPUT (Circular Convolution): 

<img width="700" height="100" alt="Screenshot 2026-02-07 105235" src="https://github.com/user-attachments/assets/911def27-01e3-4ef9-a517-4a3558ff6f8e" />

<img width="700" height="300" alt="Screenshot (11)" src="https://github.com/user-attachments/assets/e4dd6ade-e8e9-49dc-b435-72fa0b37646f" />

## RESULT: 
Linear and circular convolution of the sequences were successfully performed in SCILAB and
The results were plotted.
