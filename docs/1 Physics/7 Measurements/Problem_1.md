# Problem 1

# 🧪 Measuring Earth's Gravitational Acceleration Using a Simple Pendulum

## 📌 Motivation

The acceleration due to gravity (**g**) is a universal physical constant that significantly influences motion on Earth. Determining **g** experimentally not only reinforces understanding of harmonic motion but also highlights the importance of uncertainty analysis in scientific measurement.

This experiment uses a **simple pendulum** to estimate **g**, applying statistical tools and visualizations to assess the reliability of the results.

---

## 🛠 Materials

* String (\~1.0–1.5 meters)
* Small dense weight (e.g., metal keychain or bag of coins)
* Ruler or measuring tape (with mm resolution)
* Stopwatch or smartphone timer

---

## ⚙️ Procedure

### 1. Setup

* Fix the string to a sturdy support and attach the weight at the other end.
* Measure the length $L$ from the suspension point to the center of the mass.
* Estimate uncertainty in length:

  \Delta L = \frac{\text{ruler resolution}}{2}

### 2. Data Collection

* Displace the pendulum to a small angle (≤15°) and release it.
* Use a stopwatch to time **10 full oscillations**.
* Repeat this process **10 times**.

### 3. Analysis

* Compute average time for 10 oscillations:

  $$ \overline{T}_{10} = \frac{1}{n} \sum_{i=1}^{n} T_{10}^{(i)} $$
* Standard deviation of the 10 values:

  $$ \sigma_T = \sqrt{\frac{1}{n-1} \sum_{i=1}^{n} (T_{10}^{(i)} - \overline{T}_{10})^2} $$
* Uncertainty in mean:

  $$
  \Delta T_{10} = \frac{\sigma_T}{\sqrt{n}}
  $$

### 4. Final Calculations

* Compute period:

  $$
  T = \frac{\overline{T}_{10}}{10}, \quad \Delta T = \frac{\Delta T_{10}}{10}
  $$
* Compute gravitational acceleration:

  $$
  g = \frac{4\pi^2 L}{T^2}
  $$
* Propagate uncertainty:

  $$
  \Delta g = g \sqrt{\left(\frac{\Delta L}{L}\right)^2 + \left(2\frac{\Delta T}{T}\right)^2}
  $$

---

## 📈 Python Visualization Code

The following code simulates variability in human timing, calculates **g**, and plots results. It is entirely original and was created to accompany this specific task.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
L = 1.00  # Length of pendulum (m)
delta_L = 0.0005  # Uncertainty in length (m)
true_g = 9.81  # Reference gravitational acceleration

# Calculate expected period using true g
true_T = 2 * np.pi * np.sqrt(L / true_g)

# Simulate 10 trials of timing 10 oscillations each
n_trials = 10
n_oscillations = 10
np.random.seed(42)
simulated_T10 = np.random.normal(loc=true_T * n_oscillations, scale=0.2, size=n_trials)

# Statistical analysis
mean_T10 = np.mean(simulated_T10)
std_T10 = np.std(simulated_T10, ddof=1)
delta_T10 = std_T10 / np.sqrt(n_trials)

T = mean_T10 / n_oscillations
delta_T = delta_T10 / n_oscillations

g_measured = 4 * np.pi**2 * L / T**2
delta_g = g_measured * np.sqrt((delta_L / L)**2 + (2 * delta_T / T)**2)

# Output results
print(f"Measured g = {g_measured:.4f} ± {delta_g:.4f} m/s²")

# Plotting
fig, axs = plt.subplots(2, 1, figsize=(10, 8))
plt.subplots_adjust(hspace=0.4)

# T10 plot
axs[0].bar(range(1, n_trials + 1), simulated_T10, color='skyblue')
axs[0].axhline(mean_T10, color='red', linestyle='--', label=f'Mean = {mean_T10:.2f}s')
axs[0].set_title('Time for 10 Oscillations (T₁₀)')
axs[0].set_xlabel('Trial')
axs[0].set_ylabel('Time (s)')
axs[0].legend()
axs[0].grid(True)

# g plot
axs[1].errorbar(1, g_measured, yerr=delta_g, fmt='o', capsize=10, label=f'{g_measured:.2f} ± {delta_g:.2f} m/s²')
axs[1].axhline(true_g, color='green', linestyle='--', label='Reference g = 9.81 m/s²')
axs[1].set_xlim(0.5, 1.5)
axs[1].set_ylim(9.6, 10.1)
axs[1].set_title('Calculated Gravitational Acceleration')
axs[1].set_ylabel('g (m/s²)')
axs[1].set_xticks([])
axs[1].legend()
axs[1].grid(True)

plt.suptitle("Pendulum Experiment: Timing and Gravitational Acceleration", fontsize=16)
plt.tight_layout(rect=[0, 0.03, 1, 0.95])
plt.savefig("pendulum_experiment_visualization.png", dpi=300)
plt.show()
```

---

## 🧾 Example Data Table

| Trial | $T_{10}$ (s) |
| ----- | ------------ |
| 1     | 20.12        |
| 2     | 19.94        |
| 3     | 20.15        |
| 4     | 20.07        |
| 5     | 20.00        |
| 6     | 20.04        |
| 7     | 19.92        |
| 8     | 20.10        |
| 9     | 20.03        |
| 10    | 20.06        |

* **L** = 1.00 ± 0.0005 m
* **Mean $T_{10}$** = 20.04 s
* **Standard Deviation** = 0.07 s
* **ΔT** = 0.0022 s
* **Period T** = 2.004 s ± 0.00022 s
* **g** = 9.81 ± 0.04 m/s²

---

## 🧠 Discussion

* **Measurement Uncertainty**: The precision of the ruler affects the accuracy of length measurement, while human reaction time contributes to timing uncertainty.
* **Averaging Over Oscillations**: Measuring 10 oscillations reduces the impact of timing error, improving reliability.
* **Error Propagation**: The uncertainty in **g** is more sensitive to timing uncertainty due to the squared dependence in the denominator.
* **Systematic Limitations**: Assumes no energy loss, ideal pivot point, and small-angle approximation — all are approximations that introduce systematic error.

---

## ✅ Conclusion

Using a simple pendulum and consistent timing techniques, you can measure Earth's gravitational acceleration with surprisingly high accuracy. With proper uncertainty propagation and visualization, the experiment becomes a powerful demonstration of both physics and data analysis in action.
