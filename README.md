Infinite Impulse Response (IIR) filters are a type of digital filter with feedback, characterized by their recursive nature. They are computationally efficient for achieving high filter orders with fewer coefficients compared to finite impulse response (FIR) filters. This makes them a good choice for filtering tasks in resampling.
Polyphase decomposition is a technique used in multirate signal processing to break a filter into multiple sub-filters (called polyphase components). This decomposition enables efficient implementation of operations like upsampling, downsampling, and resampling by reducing redundant computations.
Aim : To achieve efficient rational sampling rate alteration with IIR filter using polyphase decomposition. 

The given MATLAB code demonstrates a fractional resampling process using an IIR filter along with polyphase decomposition. The steps involve upsampling the signal by a factor L, filtering to prevent aliasing, and then downsampling by a factor M. This method is effective for rational sampling rate conversion (i.e., when L and M are integers).

The plots help to visualize how the signal is modified during each step. The input signal shows the original sine wave, the interpolated and filtered signal shows the smoothed and upsampled version, and the output signal demonstrates the final resampled signal after downsampling.

Matlab Code -

# Multi-rate-Sampling---polyphase-decomposition

clc;
clear all;
% Step 1: Define Upsampling and Downsampling Factors
L = 2; % Upsampling factor
M = 3; % Downsampling factor

% Step 2: Create an Example Input Signal
fs = 1000;                                         % Original sampling frequency in Hz
t = 0:1/fs:1-1/fs;                              % 1 second duration
input_signal = sin(2*pi*50*t);        % 50 Hz sine wave as input

% Step 3: Design a Low-Pass Filter
cutoff_frequency = min(1/L, 1/M);        % Cutoff frequency for anti-aliasing
[b, a] = butter(4, cutoff_frequency);     % 4th-order Butterworth filter

% Step 4: Polyphase Decomposition of Filter
% Decompose the filter coefficients into L  branches
polyphases = cell(1, L);
for i = 1:L
    polyphases{i} = b(i:L:end);
end

% Step 5: Interpolate the Input Signal (Upsample by inserting zeros between samples)
interpolated_signal = zeros(1, L * length(input_signal));
interpolated_signal(1:L:end) = input_signal;

% Step 6: Apply Polyphase Filtering
filtered_signal = zeros(size(interpolated_signal));
for i = 1:L
    % Extract the appropriate branch and filter
    branch_signal = interpolated_signal(i:L:end);
    filtered_signal(i:L:end) = filter(polyphases{i}, a, branch_signal);
end

% Step 7: Downsample the Signal
output_signal = filtered_signal(1:M:end);

% Step 8: Plot the Results
figure;
subplot(3, 1, 1);
plot(t, input_signal);
title('Input Signal');
xlabel('Time (s)');
ylabel('Amplitude');

subplot(3, 1, 2);
plot(linspace(0, 1, length(filtered_signal)), filtered_signal);
title('Interpolated and Filtered Signal');
xlabel('Time (s)');
ylabel('Amplitude');

subplot(3, 1, 3);
plot(linspace(0, 1, length(output_signal)), output_signal, '-x');
title('Output Signal');
xlabel('Time (s)');
ylabel('Amplitude');

