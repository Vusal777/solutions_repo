
# **Investigating the Dynamics of a Forced Damped Pendulum**  

## **1. Theoretical Foundation**  

The forced damped pendulum is governed by the nonlinear differential equation:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + c \sin\theta = A \cos(\omega t)
$$

where:
- ${ \theta }$ is the angular displacement,
-  <b><i>b</i></b> is the damping coefficient,
- <b><i>c</i></b> represents the gravitational restoring force (\( <b> g/L </b> \)),
- <i><b>A</b></i> is the amplitude of the external driving force,
- <b> ω </b> is the driving frequency.

### **Small-Angle Approximation**
For small angles ($$ θ ≈ sinθ $$), the equation reduces to a **driven damped harmonic oscillator**:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + c \theta = A \cos(\omega t)
$$

which has a well-known analytical solution for periodic motion. However, for larger angles, **chaotic motion** can arise.

### **Resonance Condition**
When the driving frequency <b> ω </b> is close to the **natural frequency** of the pendulum:

$$
\omega_0 = \sqrt{c}
$$

resonance occurs, leading to **large oscillations**. The presence of damping limits this growth.

---

## **2. Python Implementation**
To analyze the pendulum, we solve the nonlinear equation numerically using **Runge-Kutta (RK45)**.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Define the forced damped pendulum differential equation
def forced_damped_pendulum(t, y, b, c, A, omega):
    """
    Computes the derivatives for the forced damped pendulum.
    :param t: Time variable
    :param y: [theta, omega] where theta is the angle and omega is the angular velocity
    :param b: Damping coefficient
    :param c: Strength of the restoring force (gravity / length)
    :param A: Driving force amplitude
    :param omega: Driving force frequency
    :return: [dtheta/dt, domega/dt]
    """
    theta, omega_vel = y
    dtheta_dt = omega_vel
    domega_dt = -b * omega_vel - c * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]

# Parameters
b = 0.5    # Damping coefficient
c = 1.0    # Gravity/Length
A = 1.2    # Driving force amplitude
omega_d = 2.0  # Driving frequency

time_span = (0, 50)  # Time range
initial_conditions = [0.5, 0]  # Initial angle and velocity
time_eval = np.linspace(*time_span, 1000)  # Time points for evaluation

# Solve the system using Runge-Kutta method
sol = solve_ivp(forced_damped_pendulum, time_span, initial_conditions, args=(b, c, A, omega_d), t_eval=time_eval)

# Plot the time evolution of theta
plt.figure(figsize=(8, 5))
plt.plot(sol.t, sol.y[0], label='Theta (Angle)')
plt.xlabel('Time')
plt.ylabel('Theta (radians)')
plt.title('Forced Damped Pendulum Motion')
plt.legend()
plt.grid()
plt.show()

# Phase space plot (theta vs. omega)
plt.figure(figsize=(8, 5))
plt.plot(sol.y[0], sol.y[1], label='Phase Space (Theta vs. Omega)')
plt.xlabel('Theta (radians)')
plt.ylabel('Omega (angular velocity)')
plt.title('Phase Space of Forced Damped Pendulum')
plt.legend()
plt.grid()
plt.show()
```

---

## **3. Results and Graphical Analysis**

### **Time Evolution of \( \theta \)**
- For **low damping**, the pendulum oscillates periodically.
- Increasing the **driving force amplitude** \( A \) can cause **irregular (chaotic) motion**.
- At **resonance**, oscillations become large.

### **Phase Space Analysis**
The **(θ, ω)** phase space plot shows:
- **Simple periodic motion** (closed loops) for weak forcing.
- **Chaotic motion** (random patterns) for high driving amplitudes.

---

## **4. Practical Applications**
The forced damped pendulum models various real-world systems:
- **Energy Harvesting:** Vibration-based energy harvesting devices.
- **Mechanical Systems:** Suspension bridges under periodic forces (e.g., Tacoma Narrows Bridge collapse).
- **Electrical Circuits:** Analogous to **driven RLC circuits** in electronics.

---

## **5. Limitations & Possible Extensions**
### **Limitations:**
- The model assumes **constant damping** and **periodic forcing**.
- It **ignores** factors like air resistance or turbulent forces.

### **Extensions:**
- **Chaos Analysis:** Compute **Poincaré sections** to visualize chaotic trajectories.
- **Bifurcation Diagrams:** Show how **small parameter changes** lead to **chaotic motion**.
- **Non-periodic Forcing:** Explore **real-world forcing functions** (e.g., earthquakes).

---

### **Final Thoughts**
This study bridges **theory** and **computation**, demonstrating how a simple system exhibits complex dynamics.

Would you like to explore **Poincaré maps**, **bifurcation diagrams**, or **chaos analysis**? 🚀