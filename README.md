Infinite Impulse Response (IIR) filters are a type of digital filter with feedback, characterized by their recursive nature. They are computationally efficient for achieving high filter orders with fewer coefficients compared to finite impulse response (FIR) filters. This makes them a good choice for filtering tasks in resampling.
Polyphase decomposition is a technique used in multirate signal processing to break a filter into multiple sub-filters (called polyphase components). This decomposition enables efficient implementation of operations like upsampling, downsampling, and resampling by reducing redundant computations.
Aim : To achieve efficient rational sampling rate alteration with IIR filter using polyphase decomposition. 

The given MATLAB code demonstrates a fractional resampling process using an IIR filter along with polyphase decomposition. The steps involve upsampling the signal by a factor L, filtering to prevent aliasing, and then downsampling by a factor M. This method is effective for rational sampling rate conversion (i.e., when L and M are integers).

The plots help to visualize how the signal is modified during each step. The input signal shows the original sine wave, the interpolated and filtered signal shows the smoothed and upsampled version, and the output signal demonstrates the final resampled signal after downsampling.

