# Digital Signal Processing Assignment
## Manual Convolution (Input-Side Algorithm) & Manual DFT Implementation

This project implements the two fundamental pillars of Digital Signal Processing (DSP):

1. Time Domain Processing – Convolution using the Input-Side Algorithm  
2. Frequency Domain Analysis – Discrete Fourier Transform (DFT) implemented manually  

High-level shortcuts such as numpy.convolve() and numpy.fft() are intentionally avoided in order to demonstrate a strong understanding of the mathematical foundations.

------------------------------------------------------------

PART 1: CONVOLUTION (INPUT-SIDE ALGORITHM)

Objective:
- Generate a noisy 50 Hz sine wave sampled at 1000 Hz for 1 second.
- Define a 3-point Moving Average Filter.
- Implement convolution manually using nested loops.
- Compare the noisy signal with the filtered output.

Theory:

Convolution is the process of combining an input signal with a filter (impulse response) to produce a modified output signal.

Mathematically:
y[n] = Σ x[i] · h[n - i]

In the Input-Side Algorithm, each input sample spreads its contribution across the output array by multiplying with the impulse response and shifting accordingly.

Moving Average Filter:
h = [1/3, 1/3, 1/3]

This filter:
- Reduces high-frequency noise
- Smooths the signal
- Preserves overall amplitude (since sum(h) = 1)

Implementation Steps:

1) Generate time vector:
t = np.linspace(0, 1, 1000)

2) Generate clean sine wave:
clean_signal = np.sin(2*np.pi*50*t)

3) Add Gaussian noise:
noise = 0.5 * np.random.normal(size=1000)
noisy_signal = clean_signal + noise

4) Define moving average filter:
h = np.ones(3) / 3

5) Manual Convolution Function:

def manual_convolution(x, h):
    Nx = len(x)
    Nh = len(h)
    y = np.zeros(Nx + Nh - 1)

    for i in range(Nx):
        for j in range(Nh):
            y[i + j] += x[i] * h[j]

    return y

Result:
The filtered signal appears smoother than the noisy signal. High-frequency noise is reduced while preserving the sine wave structure.

------------------------------------------------------------

PART 2: MANUAL DISCRETE FOURIER TRANSFORM (DFT)

Objective:
- Generate a signal containing 60 Hz and 120 Hz components.
- Implement DFT manually using cosine and sine basis functions.
- Compute magnitude spectrum.
- Plot frequency vs amplitude.

Theory:

The Discrete Fourier Transform converts a time-domain signal into its frequency-domain representation.

Real Part:
ReX[k] = Σ x[i] cos(2πki/N)

Imaginary Part:
ImX[k] = - Σ x[i] sin(2πki/N)

Magnitude Spectrum:
MagX[k] = sqrt(ReX[k]^2 + ImX[k]^2)

Manual DFT Implementation:

def calculate_dft(x):
    N = len(x)
    ReX = np.zeros(N)
    ImX = np.zeros(N)

    for k in range(N):
        for i in range(N):
            angle = 2*np.pi*k*i/N
            ReX[k] += x[i] * np.cos(angle)
            ImX[k] -= x[i] * np.sin(angle)

    MagX = np.sqrt(ReX**2 + ImX**2)
    return MagX

Result:
The magnitude spectrum shows clear peaks at:
- 60 Hz
- 120 Hz

This confirms correct frequency detection.

------------------------------------------------------------

Tools Used:
- Python 3.14
- NumPy
- Matplotlib
- Jupyter Notebook

Requirements:
numpy
matplotlib

Install using:
pip install -r requirements.txt

------------------------------------------------------------

Conclusion:

This assignment demonstrates:
- Manual implementation of convolution using the Input-Side Algorithm.
- Manual implementation of the Discrete Fourier Transform.
- Clear understanding of time-domain and frequency-domain analysis in DSP.
