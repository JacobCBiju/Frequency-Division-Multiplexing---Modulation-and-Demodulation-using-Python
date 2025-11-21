# Frequency-Division-Multiplexing---Modulation-and-Demodulation-using-Python

__Aim__:

To generate an FDM signal by multiplexing multiple baseband message signals on different carrier frequencies, transmit (sum) them, optionally add channel noise, then recover each message by bandpass filtering and coherent demodulation in Python (Google Colab). Observe time & frequency domain signals and measure recovery quality.


__Apparatus Required__:

Google Colab (or any Python environment)

Python libraries: numpy, matplotlib, scipy (scipy.signal)


__Theory__:

FDM places different message signals in separate, non-overlapping frequency bands by modulating each message onto a distinct carrier frequency. The multiplexed signal is the sum of all modulated channels. At the receiver, bandpass filters (or tuned filters) isolate each channel; then each isolated carrier is demodulated (coherently multiplied by a synchronized carrier) and low-pass filtered to recover the original baseband.

__Procedure__:

1 — Imports and parameters

2 — Create message signals and carriers

3 — Modulate each message (standard AM DSB-SC) and form FDM signal

4 — Frequency domain (spectrum) of FDM signal

5 — (Optional) Add AWGN noise to FDM signal

6 — Receiver: isolate each channel with bandpass filter

7 — Demodulate each isolated channel (coherent) and low-pass filter to recover baseband

__Program__:

t = linspace(0, 1, 1000);
freqs = [5, 5.5, 6, 6.5, 7, 7.5];

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = sin(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

demux_signals = zeros(6, length(t));
for i = 1:6
    demux_signals(i, :) = fdm_signal .* sin(2 * %pi * freqs(i) * t);
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
title("FDM Signal");

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end
__Output_:

<img width="762" height="696" alt="image" src="https://github.com/user-attachments/assets/b7dd9df8-f85f-4e42-be6e-5099b1e3ed82" />

<img width="758" height="714" alt="image" src="https://github.com/user-attachments/assets/b710b12e-10be-433c-9904-7f3682144d34" />

<img width="757" height="716" alt="image" src="https://github.com/user-attachments/assets/54b31ba7-bf14-48ca-a7d6-d93c97428ab1" />

__Result__:

FDM was successfully simulated. The six input signals were combined into one composite signal and later recovered correctly through demultiplexing using Scilab.
