# Experimental-verification-of-various-Fiber-losses--Propagation-Loss-Bend-Loss
# Propagation and Bending Losses in Plastic Fiber

## AIM
To measure propagation loss & bending losses for two different wavelengths in plastic Fiber provided with the kit.

---

## SOFTWARE REQUIRED
- GOOGLE COLAB

---

## THEORY
Optical Fibers are available in different varieties of materials. These materials are usually selected by taking into account their absorption characteristics for different wavelengths of light.  

Since the signal in Optical Fiber is transmitted in the form of light (different in nature from electrons), one has to consider the interaction of matter with radiation to study the losses in fiber.  

- **Propagation Loss:**  
  - As light propagates from one end of Fiber to another, part of it is absorbed in the material (absorption loss).  
  - Some light is reflected back or scattered due to impurity particles, contributing to signal loss.  
  - Plastic Fibers typically have higher loss (~180 dB/Km).  

- **Bending Loss:**  
  - Losses occur when the angle of incidence condition is violated, causing refraction.  
  - Smaller radius of curvature → higher loss.  
  - Other losses occur due to coupling at LED and photo detector ends.  

---

## PROCEDURE

1. Import the required Python libraries: NumPy, Pandas, and Matplotlib for numerical calculations, tabular data display, and graph plotting.
2. Set the signal frequency to 1000 Hz and initialize the propagation loss parameters, including fiber lengths, input amplitudes, and output amplitudes.
3. Initialize the bending loss parameters, including bending diameters, input amplitudes, and output amplitudes.
4. Calculate the propagation loss for each fiber length using the formula:
              LOSS(dB)=20Log Vin/Vout
5. Calculate the bending loss for each bending diameter using the same formula.
6. Display the propagation loss results in a table containing fiber length, input voltage, output voltage, and calculated loss in decibels.
7. Display the bending loss results in a table containing bending diameter, input voltage, output voltage, and calculated loss in decibels.
8. Generate a time array based on the selected frequency to represent the input and output signals as sinusoidal waveforms.
9. Plot the input and output voltage waveforms for different fiber lengths to analyze propagation loss. Use solid lines for input signals and dashed lines for output signals.
10. Plot the input and output voltage waveforms for different bending diameters to analyze bending loss. Use solid lines for input signals and dashed lines for output signals.
11. Add suitable titles, axis labels, grid lines, and legends to both graphs for clear visualization.
12. Display the graphs and compare the input and output amplitudes to understand how propagation length and bending diameter affect signal loss.

**Formula:**  
<img width="758" height="50" alt="image" src="https://github.com/user-attachments/assets/3ec6183f-3031-4862-bb34-9f59c7e29fa3" />

Where:  
- \(a\) = attenuation (nepers/meter)  
- \(L1\) = fiber length for V1  
- \(L2\) = fiber length for V2  

This \(a\) is for **660nm wavelength**.  

---

### For 950nm Wavelength
1. Set switch **SW9 → TX2 position**.  
2. Set Jumper **JP7 → +12V position**.  
3. Remove fiber from SFH756V (660nm) & SFH350V.  
4. Insert 1m fiber between **SFH450V (950nm)** & **SFH350V**.  
5. Observe detected signal at ANALOG OUT.  
6. Measure peak value = **V1**.  
7. Replace 1m fiber with 3m fiber. Measure peak value = **V2**.  

**Formula:**  
<img width="758" height="50" alt="image" src="https://github.com/user-attachments/assets/56fbe9d6-9bff-460b-b04b-d2a73d0c3cd1" />


This \(a\) is for **950nm wavelength**.  
8. Compare attenuation values for 660nm and 950nm.  

---

## MEASUREMENT OF BENDING LOSSES
1. Remove fiber from SFH450V (950nm) & SFH350V.  
2. Insert 1m fiber between **SFH756V (660nm)** & **SFH350V**.  
3. Bend fiber in a loop and measure amplitude of received signal.  
4. Reduce loop diameter gradually to ~2 cm (not less than 1 cm).  
5. Record output voltage readings.  
6. Plot graph: **Received signal amplitude vs. Loop diameter**.  

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Change these values whenever you want
frequency = 1000

# Propagation loss values
length = [1, 2, 3, 4]
input_amp = [5.0, 5.0, 5.0, 5.0]
output_amp = [4.5, 4.2, 3.9, 3.6]

# Bending loss values
diameter = [30, 25, 20, 15]
bend_input = [5.0, 5.0, 5.0, 5.0]
bend_output = [4.8, 4.5, 4.0, 3.2]

# Calculate propagation loss
prop_loss = [
    20 * np.log10(i / o)
    for i, o in zip(input_amp, output_amp)
]

# Calculate bending loss
bend_loss = [
    20 * np.log10(i / o)
    for i, o in zip(bend_input, bend_output)
]

# Display propagation table
print("PROPAGATION LOSS")
display(pd.DataFrame({
    "Length (m)": length,
    "Input (V)": input_amp,
    "Output (V)": output_amp,
    "Loss (dB)": np.round(prop_loss, 2)
}))

# Display bending table
print("BENDING LOSS")
display(pd.DataFrame({
    "Diameter (mm)": diameter,
    "Input (V)": bend_input,
    "Output (V)": bend_output,
    "Loss (dB)": np.round(bend_loss, 2)
}))

# PROGRAM
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Change these values whenever you want
frequency = 1000

# Propagation loss values
length = [1, 2, 3, 4]
input_amp = [5.0, 5.0, 5.0, 5.0]
output_amp = [4.5, 4.2, 3.9, 3.6]

# Bending loss values
diameter = [30, 25, 20, 15]
bend_input = [5.0, 5.0, 5.0, 5.0]
bend_output = [4.8, 4.5, 4.0, 3.2]

# Calculate propagation loss
prop_loss = [
    20 * np.log10(i / o)
    for i, o in zip(input_amp, output_amp)
]

# Calculate bending loss
bend_loss = [
    20 * np.log10(i / o)
    for i, o in zip(bend_input, bend_output)
]

# Display propagation table
print("PROPAGATION LOSS")
display(pd.DataFrame({
    "Length (m)": length,
    "Input (V)": input_amp,
    "Output (V)": output_amp,
    "Loss (dB)": np.round(prop_loss, 2)
}))

# Display bending table
print("BENDING LOSS")
display(pd.DataFrame({
    "Diameter (mm)": diameter,
    "Input (V)": bend_input,
    "Output (V)": bend_output,
    "Loss (dB)": np.round(bend_loss, 2)
}))

# Generate graphs
t = np.linspace(0, 4 / frequency, 1000)

plt.figure(figsize=(10, 5))
for i in range(4):
    plt.plot(t, input_amp[i] * np.sin(2*np.pi*frequency*t),
             label=f"Input {length[i]} m")
    plt.plot(t, output_amp[i] * np.sin(2*np.pi*frequency*t),
             "--", label=f"Output {length[i]} m")

plt.title("Propagation Loss")
plt.xlabel("Time (s)")
plt.ylabel("Voltage (V)")
plt.grid(True)
plt.legend(ncol=2)
plt.show()

plt.figure(figsize=(10, 5))
for i in range(4):
    plt.plot(t, bend_input[i] * np.sin(2*np.pi*frequency*t),
             label=f"Input {diameter[i]} mm")
    plt.plot(t, bend_output[i] * np.sin(2*np.pi*frequency*t),
             "--", label=f"Output {diameter[i]} mm")

plt.title("Bending Loss")
plt.xlabel("Time (s)")
plt.ylabel("Voltage (V)")
plt.grid(True)
plt.legend(ncol=2)
plt.show()
```

## TABULATION

### Propagation Loss
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/86d90141-096b-44f2-9ee8-3d197c85ff71" />


### Bending Loss
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/58b5e847-a5ad-440e-8c2f-995f1dc611ae" />


## GRAPH
<img width="917" height="467" alt="image" src="https://github.com/user-attachments/assets/85c88e8d-8f05-45fe-b6cf-4a46d1db7a92" />
<img width="911" height="476" alt="image" src="https://github.com/user-attachments/assets/cd4570dc-1fca-4056-8ac1-d67ca894a4ed" />


## RESULT
- Propagation loss and bending losses for **660nm** and **950nm** wavelengths were measured.  
- Attenuation values compared and bending loss characteristics plotted.  
