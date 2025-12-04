# Frequency Division Multiplexing
## AIM

To implement Frequency Division Multiplexing (FDM) for six different message signals using Scilab, generate the multiplexed signal, and perform demultiplexing to recover all the original message signals. The experiment also includes plotting the message signals, multiplexed signal, and demultiplexed signals.
## APPARATUS REQUIRED

  1 Computer System
  2 Scilab Software

## ALGORITHM

  1.Set sampling frequency, time duration, and time vector.
  2.Generate six message signals with different frequencies.
  3.Assign six different carrier frequencies.
  4.Perform DSB-SC modulation by multiplying each message with its carrier.
  5.Add all modulated signals to form the multiplexed FDM signal.
  6.For each channel, multiply the multiplexed signal with the same carrier (demodulation).
  7.Apply a low-pass filter to extract the recovered message.
  8.Plot message signals, multiplexed signal, and recovered s ignals.

  ## THEORY

Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a different carrier frequency. Each message modulates its own carrier, and all modulated signals are added to form the multiplexed signal. Since the carrier frequencies are well separated, the signals do not overlap in the frequency domain.

At the receiver, each signal is recovered by multiplying the multiplexed signal with the corresponding carrier (coherent demodulation) and passing it through a low-pass filter to extract the original baseband message. FDM is widely used in radio broadcasting, telephone systems, and cable TV.

## program
```
clc;
clear;
close;

fs = 20000;
t = 0:1/fs:0.02;

fm = [50,100,150,200,250,300];
m = [];

for i = 1:6
    m(i, :) = sin(2*%pi*fm(i)*t);
end

fc = [1000, 2000, 3000, 4000, 5000, 6000];

fdm = zeros(1, length(t));
for i = 1:6
    c = cos(2*%pi*fc(i)*t);
    s = m(i, :) .* c;
    fdm = fdm + s;
end

scf(1);
clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, m(i, :));

end


scf(2);
clf;
plot(t, fdm);



demod = [];
for i = 1:6
    c = cos(2*%pi*fc(i)*t);
    x = fdm .* c;
    h = ones(1,100)/100;
    y = conv(x, h, 'same');
    demod(i, :) = y;
end

scf(3);
clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, demod(i, :));
end

```
## output waveform
<img width="1918" height="919" alt="Screenshot 2025-12-04 233123" src="https://github.com/user-attachments/assets/6ec39f4a-6b81-4a1f-9b08-e528ce40820e" />

<img width="1916" height="936" alt="Screenshot 2025-12-04 233104" src="https://github.com/user-attachments/assets/7a4daa76-2cd8-43c1-b768-82edb136de64" />

<img width="1919" height="911" alt="Screenshot 2025-12-04 233113" src="https://github.com/user-attachments/assets/ac96a62a-3d3f-4ea2-810b-3ef6bc11e05e" />

## table


## result
Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.


