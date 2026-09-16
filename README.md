# FIR-FILTER-DESIGN
# EXP 4 b: Design-of-FIR-Digital-Filter-using-Hamming-Window

# AIM 1:  To perform Design-of-LOWPASS FIR-Digital-Filter-using-Hamming-Window using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```// Design of Lowpass FIR Digital Filter using Hamming Window
clear;
clc;
clf;

// 1. Simple Filter Specifications
N = 11;                  // Filter length (odd)
wc = 0.4 * %pi;          // Cutoff frequency in radians
alpha = (N - 1) / 2;     // Center of symmetry (alpha = 5)

// 2. Impulse Response hd(n) for Ideal LPF
n = 0:(N - 1);
hd = zeros(1, N);

for i = 1:N
    m = n(i) - alpha;
    if m == 0 then
        hd(i) = wc / %pi;
    else
        hd(i) = sin(wc * m) / (%pi * m);
    end
end

// 3. Apply Hamming Window: w(n) = 0.54 - 0.46 * cos(2*pi*n / (N-1))
w_ham = 0.54 - 0.46 * cos(2 * %pi * n / (N - 1));
h = hd .* w_ham;

// 4. Frequency Response (DTFT)
w = linspace(0, %pi, 1000);
H = zeros(1, length(w));

for k = 1:length(w)
    H(k) = sum(h .* exp(-%i * w(k) * n));
end

mag = abs(H);                         // Linear Magnitude
mag_dB = 20 * log10(mag + %eps);      // Magnitude in dB
norm_w = w / %pi;                     // Normalized frequency (0 to 1)

// 5. Plotting

// Subplot 1: Linear Magnitude Response
subplot(2, 1, 1);
plot(norm_w, mag, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR LPF using Hamming Window (Linear)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude', 'fontsize', 2);
xgrid(1);

// Subplot 2: Decibel (dB) Magnitude Response
subplot(2, 1, 2);
plot(norm_w, mag_dB, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR LPF using Hamming Window (dB)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude in dB', 'fontsize', 2);
xgrid(1);
```

# OUTPUT: 

<img width="610" height="460" alt="image" src="https://github.com/user-attachments/assets/0e22b57a-da77-4c4b-b552-b9b13b12e888" />

# RESULT: 

Thus design of low pass FIR digital filter using-Hamming-Window waveforms were plotted and output was verified.

# AIM 2: To perform DESIGN OF HIGH PASS FIR DIGITAL FILTERS using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```
// Design of Highpass FIR Digital Filter using Hamming Window
clear;
clc;
clf;

// 1. Simple Filter Specifications
N = 11;                  // Filter length (odd)
wc = 0.5 * %pi;          // Cutoff frequency in radians
alpha = (N - 1) / 2;     // Center of symmetry (alpha = 5)

// 2. Impulse Response hd(n) for Ideal HPF
n = 0:(N - 1);
hd = zeros(1, N);

for i = 1:N
    m = n(i) - alpha;
    if m == 0 then
        hd(i) = 1 - (wc / %pi);
    else
        hd(i) = -sin(wc * m) / (%pi * m);
    end
end

// 3. Apply Hamming Window: w(n) = 0.54 - 0.46 * cos(2*pi*n / (N-1))
w_ham = 0.54 - 0.46 * cos(2 * %pi * n / (N - 1));
h = hd .* w_ham;

// 4. Frequency Response (DTFT)
w = linspace(0, %pi, 1000);
H = zeros(1, length(w));

for k = 1:length(w)
    H(k) = sum(h .* exp(-%i * w(k) * n));
end

mag = abs(H);                         // Linear Magnitude
mag_dB = 20 * log10(mag + %eps);      // Magnitude in dB
norm_w = w / %pi;                     // Normalized frequency (0 to 1)

// 5. Plotting

// Subplot 1: Linear Magnitude Response
subplot(2, 1, 1);
plot(norm_w, mag, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR HPF using Hamming Window (Linear)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude', 'fontsize', 2);
xgrid(1);

// Subplot 2: Decibel (dB) Magnitude Response
subplot(2, 1, 2);
plot(norm_w, mag_dB, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR HPF using Hamming Window (dB)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude in dB', 'fontsize', 2);
xgrid(1);
```

# OUTPUT: 
<img width="610" height="460" alt="image" src="https://github.com/user-attachments/assets/5e04b8da-7534-4baf-b93e-eed062eea788" />


# RESULT: 
Thus design of HIGH pass FIR digital filter using-Hamming-Window waveforms were plotted and output was verified.

# AIM 3: To perform DESIGN OF BAND PASS FIR DIGITAL FILTERS using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```// Design of Bandpass FIR Digital Filter using Hamming Window
clear;
clc;
clf;

// 1. Simple Filter Specifications
N = 11;                  // Filter length (odd)
wc1 = 0.3 * %pi;         // Lower cutoff frequency
wc2 = 0.7 * %pi;         // Upper cutoff frequency
alpha = (N - 1) / 2;     // Center of symmetry (alpha = 5)

// 2. Impulse Response hd(n) for Ideal BPF
n = 0:(N - 1);
hd = zeros(1, N);

for i = 1:N
    m = n(i) - alpha;
    if m == 0 then
        hd(i) = (wc2 - wc1) / %pi;
    else
        hd(i) = (sin(wc2 * m) - sin(wc1 * m)) / (%pi * m);
    end
end

// 3. Apply Hamming Window: w(n) = 0.54 - 0.46 * cos(2*pi*n / (N-1))
w_ham = 0.54 - 0.46 * cos(2 * %pi * n / (N - 1));
h = hd .* w_ham;

// 4. Frequency Response (DTFT)
w = linspace(0, %pi, 1000);
H = zeros(1, length(w));

for k = 1:length(w)
    H(k) = sum(h .* exp(-%i * w(k) * n));
end

mag = abs(H);                         // Linear Magnitude
mag_dB = 20 * log10(mag + %eps);      // Magnitude in dB
norm_w = w / %pi;                     // Normalized frequency (0 to 1)

// 5. Plotting

// Subplot 1: Linear Magnitude Response
subplot(2, 1, 1);
plot(norm_w, mag, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR BPF using Hamming Window (Linear)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude', 'fontsize', 2);
xgrid(1);

// Subplot 2: Decibel (dB) Magnitude Response
subplot(2, 1, 2);
plot(norm_w, mag_dB, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR BPF using Hamming Window (dB)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude in dB', 'fontsize', 2);
xgrid(1);
```

# OUTPUT: 
<img width="610" height="460" alt="image" src="https://github.com/user-attachments/assets/645b709c-c04e-4cb0-b2fe-f16ab8eb70d3" />


# RESULT: 
Thus design of BAND pass FIR digital filter using-Hamming-Window waveforms were plotted and output was verified.

# AIM 4: To perform DESIGN OF BAND STOP FIR DIGITAL FILTER using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```// Design of Bandstop FIR Digital Filter using Hamming Window
clear;
clc;
clf;

// 1. Simple Filter Specifications
N = 11;                  // Filter length (odd)
wc1 = 0.3 * %pi;         // Lower cutoff frequency (stopband start)
wc2 = 0.7 * %pi;         // Upper cutoff frequency (stopband end)
alpha = (N - 1) / 2;     // Center of symmetry (alpha = 5)

// 2. Impulse Response hd(n) for Ideal Bandstop Filter (BSF)
n = 0:(N - 1);
hd = zeros(1, N);

for i = 1:N
    m = n(i) - alpha;
    if m == 0 then
        hd(i) = 1 - ((wc2 - wc1) / %pi);
    else
        hd(i) = (sin(wc1 * m) - sin(wc2 * m)) / (%pi * m);
    end
end

// 3. Apply Hamming Window: w(n) = 0.54 - 0.46 * cos(2*pi*n / (N-1))
w_ham = 0.54 - 0.46 * cos(2 * %pi * n / (N - 1));
h = hd .* w_ham;

// 4. Frequency Response (DTFT)
w = linspace(0, %pi, 1000);
H = zeros(1, length(w));

for k = 1:length(w)
    H(k) = sum(h .* exp(-%i * w(k) * n));
end

mag = abs(H);                         // Linear Magnitude
mag_dB = 20 * log10(mag + %eps);      // Magnitude in dB
norm_w = w / %pi;                     // Normalized frequency (0 to 1)

// 5. Plotting

// Subplot 1: Linear Magnitude Response
subplot(2, 1, 1);
plot(norm_w, mag, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR BSF using Hamming Window (Linear)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude', 'fontsize', 2);
xgrid(1);

// Subplot 2: Decibel (dB) Magnitude Response
subplot(2, 1, 2);
plot(norm_w, mag_dB, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR BSF using Hamming Window (dB)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude in dB', 'fontsize', 2);
xgrid(1);
```

# OUTPUT: 
<img width="610" height="460" alt="image" src="https://github.com/user-attachments/assets/a66119f0-dab0-49c9-baf9-a08c877a0451" />


# RESULT: 
Thus design of BAND STOP FIR digital filter using-Hamming-Window waveforms were plotted and output was verified.
