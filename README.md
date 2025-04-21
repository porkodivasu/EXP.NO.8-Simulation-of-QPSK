# EXP.NO.8-Simulation-of-QPSK

8.Simulation of QPSK

# AIM
To generate and visualize a Quadrature Phase Shift Keying (QPSK) modulated signal using Python.
# SOFTWARE REQUIRED
personal computer
# ALGORITHMS
Bit Generation:

A random binary sequence is generated with length = 2 × number of symbols.

Symbol Mapping:

Every two bits are grouped and mapped to a phase (0, π/2, π, or 3π/2).

QPSK Signal Generation:

Each symbol is represented as a complex exponential (cos + j·sin) over the symbol period.

The resulting signal is a combination of all symbol segments.

Visualization:

The in-phase and quadrature components are plotted separately.

The real part of the full QPSK waveform is also plotted.

Vertical lines and bit labels show where each symbol starts and its value.

📈 How to Improve or Extend:
If you want to take this further:

Add AWGN noise and simulate demodulation.

Plot the constellation diagram (scatter plot of symbol points).

Compute Bit Error Rate (BER) under noise.
# PROGRAM
import numpy as np 
import matplotlib.pyplot as plt 
# Parameters 
num_symbols = 10  # Number of symbols (reduced for clarity in the plot) 
T = 1.0  # Symbol period 
fs = 100.0  # Sampling frequency 
t = np.arange(0, T, 1/fs)  # Time vector for one symbol 
# Generate random bit sequence 
bits = np.random.randint(0, 2, num_symbols * 2)  # Two bits per QPSK symbol 
symbols = 2 * bits[0::2] + bits[1::2]  # Map bits to QPSK symbols 
# Initialize QPSK signal 
qpsk_signal = np.array([]) 
symbol_times = [] 
# Define the QPSK modulation and phase angles 
symbol_phases = {0: 0, 1: np.pi/2, 2: np.pi, 3: 3*np.pi/2} 
# Generate QPSK signal 
for i, symbol in enumerate(symbols): 
phase = symbol_phases[symbol] 
symbol_time = i * T 
qpsk_segment = np.cos(2 * np.pi * t / T + phase) + 1j * np.sin(2 * np.pi * t / T + phase) 
qpsk_signal = np.concatenate((qpsk_signal, qpsk_segment)) 
symbol_times.append(symbol_time) 
# Time vector for the entire signal 
t_total = np.arange(0, num_symbols * T, 1/fs) 
# Plot real and imaginary parts of the QPSK signal 
plt.figure(figsize=(14, 12)) 
# Plot the in-phase component with symbols 
plt.subplot(3, 1, 1) 
plt.plot(t_total, np.real(qpsk_signal), label='In-phase') 
for i, symbol_time in enumerate(symbol_times): 
plt.axvline(symbol_time, color='red', linestyle='--', linewidth=0.5) 
plt.text(symbol_time + T/4, 0, f'{symbols[i]:02b}', fontsize=12, color='blue') 
plt.title('QPSK Signal - In-phase Component with Symbols') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.grid(True) 
plt.legend() 
# Plot the quadrature component with symbols 
plt.subplot(3, 1, 2) 
plt.plot(t_total, np.imag(qpsk_signal), label='Quadrature', color='orange') 
for i, symbol_time in enumerate(symbol_times): 
plt.axvline(symbol_time, color='red', linestyle='--', linewidth=0.5) 
plt.text(symbol_time + T/4, 0, f'{symbols[i]:02b}', fontsize=12, color='blue') 
plt.title('QPSK Signal - Quadrature Component with Symbols') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.grid(True) 
plt.legend() 
# Plot the resultant QPSK waveform (real part) 
plt.subplot(3, 1, 3) 
plt.plot(t_total, np.real(qpsk_signal), label='Resultant QPSK Waveform', color='green') 
for i, symbol_time in enumerate(symbol_times): 
plt.axvline(symbol_time, color='red', linestyle='--', linewidth=0.5) 
plt.text(symbol_time + T/4, 0, f'{symbols[i]:02b}', fontsize=12, color='blue') 
plt.title('Resultant QPSK Waveform') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.grid(True) 
plt.legend() 
plt.tight_layout() 
plt.show() 

# OUTPUT
 ![Screenshot (55)](https://github.com/user-attachments/assets/3f43c0ca-405c-40e3-9d41-5784e37567be)

# RESULT / CONCLUSIONS
