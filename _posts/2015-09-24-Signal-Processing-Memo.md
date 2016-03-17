---
layout : post
category : Memo
tags : [SignalProcessing, FFT]
---

{% include JB/setup %}

Fast Fourier Transform is a widely used method to perform signal processing. Defined by *Jean Baptiste Joseph Fourier*, any time varying function can be devided in single periodic signals.

FFT Parameters:
- Window: The window is applied to a number of signal samples. The number of samples of each window is divided in bars, or "bins". The number of bins is proportional to the number of samples in the window: it is the *FFT size*.\\
The window size and the FFT size determine the resolution of the representation in frequency and time.
- Frequency range: the maximum frequency range is determined by the *sampling rate*: $F_max = SamplingRate / 2$.