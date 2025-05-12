# Problem 1

# 🪐 Measuring Earth's Gravitational Acceleration Using a Simple Pendulum

## ✨ Motivation

The acceleration due to gravity (**g**) is a fundamental physical constant with a typical value of **9.81 m/s²** near the Earth’s surface. Accurate knowledge of this constant is crucial for applications in physics, engineering, geophysics, and many other fields. One of the simplest and most elegant methods to experimentally measure **g** is using a **simple pendulum**, exploiting the relationship between the period of oscillation and the gravitational field.

This exercise aims to:

* Determine **g** using a pendulum.
* Analyze and propagate uncertainties in the experiment.
* Practice data analysis and visualization using Python.

---

## 🧪 Materials

* A string (1.0–1.5 meters long)
* A small dense weight (e.g., a metal keychain or bag of coins)
* A stopwatch or smartphone timer
* A ruler or tape measure (preferably with mm precision)

---

## ⚙️ Procedure

### 1. Setup

* Tie one end of the string to a support and attach the mass to the other end.
* Measure the length $L$ from the suspension point to the center of the mass. Use a ruler or tape measure.
* Estimate the uncertainty in the length:

  $$
  \Delta L = \frac{\text{Resolution of the ruler}}{2}
  $$

### 2. Data Collection

* Displace the pendulum by less than 15° to minimize non-linear effects.
* Measure the total time for **10 complete oscillations** (back and forth) using a stopwatch.
* Repeat this 10 times to get a set of values $T_{10}^{(i)}$.

### 3. Analyze Data

* Compute the average time for 10 oscillations:

  $$
  \overline{T}_{10} = \frac{1}{n} \sum_{i=1}^{n} T_{10}^{(i)}
  $$
* Compute the standard deviation $\sigma_T$.
* Calculate the uncertainty in the mean:

  $$
  \Delta T_{10} = \frac{\sigma_T}{\sqrt{n}}
  $$

### 4. Compute Period and g

* Compute the period:

  $$
  T = \frac{\overline{T}_{10}}{10}, \quad \Delta T = \frac{\Delta T_{10}}{10}
  $$
* Calculate **g**:

  $$
  g = \frac{4\pi^2 L}{T^2}
  $$
* Propagate uncertainties:

  $$
  \Delta g = g \sqrt{\left(\frac{\Delta L}{L}\right)^2 + \left(2\frac{\Delta T}{T}\right)^2}
  $$

---

## 📊 Python Code for Simulation & Visualization

The following Python code simulates the pendulum experiment and visualizes:

* Variations in timing due to human error.
* How these variations influence the calculated value of **g**.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
L = 1.00  # Length of the pendulum in meters
delta_L = 0.0005  # Uncertainty in length (half the resolution of a mm ruler)
true_g = 9.81  # True value of g for reference

# Simulate timing for 10 sets of 10 oscillations
np.random.seed(42)
true_T = 2 * np.pi * np.sqrt(L / true_g)  # True period
n_trials = 10
n_oscillations = 10

# Simulate human timing uncertainty (e.g., 0.2s std dev over 10 oscillations)
simulated_T10 = np.random.normal(loc=true_T * n_oscillations, scale=0.2, size=n_trials)
mean_T10 = np.mean(simulated_T10)
std_T10 = np.std(simulated_T10, ddof=1)
delta_T10 = std_T10 / np.sqrt(n_trials)

# Compute single period and uncertainty
T = mean_T10 / n_oscillations
delta_T = delta_T10 / n_oscillations

# Calculate g and its uncertainty
g_measured = 4 * np.pi**2 * L / T**2
delta_g = g_measured * np.sqrt((delta_L / L)**2 + (2 * delta_T / T)**2)

# Print results
print(f"Measured g = {g_measured:.4f} ± {delta_g:.4f} m/s²")

# Visualization
fig, axs = plt.subplots(2, 1, figsize=(10, 8), gridspec_kw={'height_ratios': [1, 1.2]})
plt.subplots_adjust(hspace=0.4)

# Plot timing measurements
axs[0].bar(range(1, n_trials + 1), simulated_T10, color='skyblue', edgecolor='black')
axs[0].axhline(mean_T10, color='red', linestyle='--', label=f'Mean = {mean_T10:.2f}s')
axs[0].set_title('Measured Time for 10 Oscillations (T₁₀)')
axs[0].set_xlabel('Trial Number')
axs[0].set_ylabel('Time (s)')
axs[0].legend()
axs[0].grid(True)

# Plot g with uncertainty
axs[1].errorbar(1, g_measured, yerr=delta_g, fmt='o', capsize=10, label=f'Measured g = {g_measured:.2f} ± {delta_g:.2f} m/s²')
axs[1].axhline(true_g, color='green', linestyle='--', label='True g = 9.81 m/s²')
axs[1].set_xlim(0.5, 1.5)
axs[1].set_ylim(9.6, 10.1)
axs[1].set_title('Calculated Gravitational Acceleration')
axs[1].set_ylabel('g (m/s²)')
axs[1].set_xticks([])
axs[1].legend()
axs[1].grid(True)

plt.suptitle("Pendulum Experiment: Timing and Gravitational Acceleration", fontsize=16)
plt.tight_layout(rect=[0, 0.03, 1, 0.95])
plt.savefig('pendulum_g_visualization.png', dpi=300)
plt.show()
```

---

## 🧾 Sample Tabulated Data (Markdown-Ready)

| Trial | T₁₀ (s) |
| ----- | ------- |
| 1     | 20.12   |
| 2     | 20.01   |
| 3     | 19.95   |
| 4     | 20.20   |
| 5     | 20.04   |
| 6     | 19.88   |
| 7     | 20.17   |
| 8     | 20.22   |
| 9     | 20.00   |
| 10    | 20.08   |

**Length**: L = 1.00 ± 0.0005 m
**Mean T₁₀**: 20.07 s
**Standard Deviation**: 0.11 s
**ΔT₁₀**: 0.035 s
**Period (T)**: 2.007 s ± 0.0035 s
**Calculated g**: 9.79 ± 0.04 m/s²

---

## 📌 Discussion & Sources of Uncertainty

1. **Measurement Resolution**:

   * A typical ruler’s resolution (1 mm) limits the precision in measuring the length.
   * Taking uncertainty as half the smallest division gives a more conservative estimate.

2. **Human Reaction Time**:

   * Stopwatch timing is affected by human response delays.
   * Measuring 10 oscillations instead of 1 helps reduce the impact of this error.

3. **Air Resistance and Swing Angle**:

   * The formula for **g** assumes small angles (θ < 15°).
   * Deviations from this introduce systematic errors.

4. **Pendulum Length Assumption**:

   * The length must be measured to the center of mass of the pendulum bob, which can be imprecise if the object isn't symmetric.

---

## ✅ Conclusion

This experiment provides a reasonably accurate value of **g** using very simple materials. By combining careful measurement, repeated trials, and uncertainty analysis — and visualizing the results — we gain a deeper appreciation of how precise physics experiments must be to achieve reliable results.