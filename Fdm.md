# SIMULATION OF FREQUENCY DIVISION MULTIPLEXING (FDM) AND DEMULTIPLEXING USING SCILAB
### AIM:

To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.

### EQUIPMENTS Needed

Computer with Scilab installed

### ALGORITHM

Define six different frequencies to generate six sine wave signals.

Generate the time vector to represent time samples.

Compute six sine signals for each frequency over the time vector.

Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.

Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.

Plot original signals, multiplexed signal, and demultiplexed signals for verification.

### PROGRAM

```
t = linspace(0, 1, 1000);
fs = 1000; 

freqs = [4, 8, 12, 16, 20, 24];

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = sin(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

order = 50;
cutoff_freq = 8 / (fs/2); 
h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));
for i = 1:6
    mixed = fdm_signal .* sin(2 * %pi * freqs(i) * t);
    demux_signals(i, :) = filter(h, 1, mixed);
end

scf(1);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i, :));
    title('Original Signal f=' + string(freqs(i)));
end

scf(2);
clf;
plot(t, fdm_signal);
title('FDM Signal');

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end

```

### GRAPH:

<img width="1920" height="1200" alt="Screenshot 2025-11-28 162757" src="https://github.com/user-attachments/assets/de50683f-a1a8-4beb-9ab1-8b04cc9eaffd" />
<img width="1920" height="1200" alt="Screenshot 2025-11-28 162742" src="https://github.com/user-attachments/assets/83794927-df76-4770-9d67-839f47649db8" />
<img width="1920" height="1200" alt="Screenshot 2025-11-28 162730" src="https://github.com/user-attachments/assets/d0f7aab9-0da7-4755-ab5f-a5aac948cfca" />



### TABULATION:

![WhatsApp Image 2025-11-28 at 15 52 08_cdcc4e33](https://github.com/user-attachments/assets/8c14a69f-ab6e-4962-8d4a-d88b847a1f52)
![WhatsApp Image 2025-11-28 at 15 52 08_68d4f6cb](https://github.com/user-attachments/assets/73ce9e64-7db2-4a1d-85b9-fc02b8fb5d57)



### RESULTS:

The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in Scilab.
