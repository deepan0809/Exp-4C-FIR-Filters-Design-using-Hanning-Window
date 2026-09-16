# EXP 4 C : Design-of-FIR-Filters-using-Hanning-window
#          DESIGN OF FIR DIGITAL FILTERS USING HANNING WINDOW
# AIM: 
          
  To generate design of FIR digital filters using HANNING window using SCILAB 

# APPARATUS REQUIRED: 

  PC Installed with SCILAB 

# PROGRAM for LPF,HPF,BPF, BSF
```
clc;
clear;
close;

N = 21;
M = 10;

fc = 0.3;
f1 = 0.2;
f2 = 0.5;

w = 0.5 - 0.5*cos(2*%pi*(0:N-1)/(N-1));
w = w(:);

hLP = zeros(N,1);

for k = 1:N
    if k == M+1 then
        hLP(k) = 2*fc;
    else
        hLP(k) = sin(2*%pi*fc*(k-M-1)) / ...
                 (%pi*(k-M-1));
    end
end

hLP = hLP .* w;

hHP = zeros(N,1);

for k = 1:N
    if k == M+1 then
        hHP(k) = 1 - 2*fc;
    else
        hHP(k) = -sin(2*%pi*fc*(k-M-1)) / ...
                 (%pi*(k-M-1));
    end
end

hHP = hHP .* w;

hBP = zeros(N,1);

for k = 1:N
    if k == M+1 then
        hBP(k) = 2*(f2-f1);
    else
        hBP(k) = (sin(2*%pi*f2*(k-M-1)) - ...
                  sin(2*%pi*f1*(k-M-1))) / ...
                 (%pi*(k-M-1));
    end
end

hBP = hBP .* w;

hBS = zeros(N,1);

for k = 1:N
    if k == M+1 then
        hBS(k) = 1 - 2*(f2-f1);
    else
        hBS(k) = (sin(2*%pi*f1*(k-M-1)) - ...
                  sin(2*%pi*f2*(k-M-1))) / ...
                 (%pi*(k-M-1));
    end
end

hBS = hBS .* w;

disp("Low Pass Filter:");
disp(hLP);

disp("High Pass Filter:");
disp(hHP);

disp("Band Pass Filter:");
disp(hBP);

disp("Band Stop Filter:");
disp(hBS);

nfft = 1024;

// Create zero-padded signals
xLP = zeros(nfft,1);
xHP = zeros(nfft,1);
xBP = zeros(nfft,1);
xBS = zeros(nfft,1);

xLP(1:N) = hLP;
xHP(1:N) = hHP;
xBP(1:N) = hBP;
xBS(1:N) = hBS;

// Forward FFT
HLP = fft(xLP,1);
HHP = fft(xHP,1);
HBP = fft(xBP,1);
HBS = fft(xBS,1);

// Keep first half
HLP = abs(HLP(1:nfft/2+1));
HHP = abs(HHP(1:nfft/2+1));
HBP = abs(HBP(1:nfft/2+1));
HBS = abs(HBS(1:nfft/2+1));

f = (0:nfft/2)'/nfft;

clf();

subplot(2,2,1);
plot(0:N-1,hLP);
xlabel("n");
ylabel("h(n)");
title("FIR LPF - Hanning Window");
xgrid();

subplot(2,2,2);
plot(0:N-1,hHP);
xlabel("n");
ylabel("h(n)");
title("FIR HPF - Hanning Window");
xgrid();

subplot(2,2,3);
plot(0:N-1,hBP);
xlabel("n");
ylabel("h(n)");
title("FIR BPF - Hanning Window");
xgrid();

subplot(2,2,4);
plot(0:N-1,hBS);
xlabel("n");
ylabel("h(n)");
title("FIR BSF - Hanning Window");
xgrid();

scf(2);
clf();

subplot(2,2,1);
plot(f,HLP);
xlabel("Frequency / pi");
ylabel("Magnitude");
title("LPF Frequency Response");
xgrid();

subplot(2,2,2);
plot(f,HHP);
xlabel("Frequency / pi");
ylabel("Magnitude");
title("HPF Frequency Response");
xgrid();

subplot(2,2,3);
plot(f,HBP);
xlabel("Frequency / pi");
ylabel("Magnitude");
title("BPF Frequency Response");
xgrid();

subplot(2,2,4);
plot(f,HBS);
xlabel("Frequency / pi");
ylabel("Magnitude");
title("BSF Frequency Response");
xgrid();

```
# OUTPUT for LPF,HPF,BPF, BSF

<img width="1917" height="1198" alt="image" src="https://github.com/user-attachments/assets/3c014a4f-2a4d-40d2-8d51-0cb57ad01298" />

<img width="1917" height="1198" alt="image" src="https://github.com/user-attachments/assets/719ba1c1-5965-4cc1-a131-6ba42077018a" />

# RESULT

The design of FIR filters using Hanning Window is successfully completed using SCILAB.
