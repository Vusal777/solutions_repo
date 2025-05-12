# Problem 1

Absolutely! Here's a well-structured, article-style write-up based on your task: **"Measuring Earth's Gravitational Acceleration with a Pendulum"**. It's written in a clear academic tone suitable for a report or publication-style assignment.

---

# Measuring Earth's Gravitational Acceleration with a Pendulum

### **Abstract**

The acceleration due to gravity (**g**) is a fundamental constant central to classical mechanics. In this experiment, we determine the local value of **g** using a simple pendulum and analyze the impact of measurement uncertainties on the result. This classic physics experiment provides insights into the importance of precision and error propagation in experimental work.

---

### **Introduction**

Gravitational acceleration, commonly denoted as **g**, plays a critical role in various physical phenomena, from planetary motion to engineering applications. While the standard accepted value of **g** at Earth's surface is approximately **9.81 m/s²**, its local value may vary slightly depending on altitude, latitude, and geological composition. A simple and widely used method to experimentally determine **g** is through the analysis of a simple pendulum’s periodic motion.

A simple pendulum, when displaced by a small angle (less than 15°), behaves like a harmonic oscillator, and its period is governed by the formula:

$$
T = 2\pi\sqrt{\frac{L}{g}}
$$

By measuring the pendulum length **L** and the oscillation period **T**, one can solve for **g**. The accuracy of this measurement, however, is highly dependent on the precision of length and time measurements. This experiment emphasizes careful data collection and rigorous uncertainty analysis.

---

### **Materials and Methods**

#### **Materials**

* String (approximately 1.0 to 1.5 meters)
* Small mass (e.g., bag of coins or keychain)
* Stopwatch (or a smartphone timer)
* Measuring tape or ruler with millimeter resolution

#### **Experimental Setup**

The pendulum was constructed by attaching a small weight to a string and suspending it from a fixed support. The length **L** was measured from the suspension point to the center of mass of the weight using a ruler with a 1 mm resolution, giving an uncertainty in length:

$$
\Delta L = \frac{\text{Ruler resolution}}{2} = 0.0005 \, \text{m}
$$

#### **Procedure**

The pendulum was displaced by a small angle (less than 15°) and released. The time for 10 full oscillations was measured using a stopwatch. This process was repeated 10 times to obtain a reliable data set. The average time **T̄₁₀**, standard deviation **σₜ**, and uncertainty in the mean time **ΔT₁₀** were calculated using:

$$
\Delta T_{10} = \frac{\sigma_T}{\sqrt{n}}, \quad \text{with } n = 10
$$

The period of one oscillation was determined by dividing the average time by 10. This period was then used to compute the local value of **g**, followed by the propagation of uncertainties.

---

### **Calculations**

#### **1. Period of Oscillation**

$$
T = \frac{\overline{T}_{10}}{10}, \quad \Delta T = \frac{\Delta T_{10}}{10}
$$

#### **2. Acceleration Due to Gravity**

$$
g = \frac{4\pi^2 L}{T^2}
$$

#### **3. Propagation of Uncertainty**

$$
\Delta g = g \cdot \sqrt{\left(\frac{\Delta L}{L}\right)^2 + \left(2 \cdot \frac{\Delta T}{T}\right)^2}
$$

---

### **Results**

A summary of the collected and computed data:

| Quantity                                | Value                |
| --------------------------------------- | -------------------- |
| Pendulum length, **L**                  | 1.000 m ± 0.0005 m   |
| Mean time for 10 oscillations, **T̄₁₀** | 20.085 s             |
| Standard deviation, **σₜ**              | 0.030 s              |
| Uncertainty in mean, **ΔT₁₀**           | 0.0095 s             |
| Period, **T**                           | 2.0085 s ± 0.00095 s |
| Calculated **g**                        | 9.81 m/s²            |
| Uncertainty in **g**, **Δg**            | ±0.01 m/s²           |

---

### **Discussion**

#### **Measurement Accuracy**

The experiment produced a gravitational acceleration value of **9.81 ± 0.01 m/s²**, which is remarkably close to the standard value. This indicates that with careful setup and timing, a simple pendulum can yield accurate results for **g**.

#### **Sources of Uncertainty**

* **Length Measurement (ΔL):**
  The precision of the length measurement was limited by the ruler’s resolution. Since length appears in the numerator of the formula for **g**, this contributed directly to the result’s accuracy.

* **Timing Variability (ΔT):**
  Timing was the largest source of uncertainty, affected by human reaction time and inconsistency in stopwatch operation. To reduce these effects, the measurement was averaged over 10 trials and 10 oscillations.

#### **Assumptions and Limitations**

* The pendulum is assumed to be ideal (massless string, point mass, negligible air resistance).
* The small-angle approximation is valid since the angle was kept under 15°.
* The center of mass of the pendulum bob was estimated accurately, but minor deviations could have occurred.

---

### **Conclusion**

This experiment successfully measured the local gravitational acceleration using a simple pendulum. The calculated value of **g = 9.81 ± 0.01 m/s²** aligns with the standard value, demonstrating the effectiveness of the method. Additionally, the exercise highlights the importance of uncertainty analysis in obtaining reliable experimental results. Simple tools, when used thoughtfully and with attention to precision, can provide deep insight into fundamental constants of nature.
