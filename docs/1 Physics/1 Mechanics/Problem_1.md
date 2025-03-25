# Problem 1

import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # Gravitational acceleration (m/s^2)

def range_of_projectile(v0, angle):
    """Calculate the range of a projectile given initial velocity and angle."""
    # Convert angle to radians
    angle_rad = np.radians(angle)
    # Calculate the range
    R = (v0**2 * np.sin(2 * angle_rad)) / g
    return R

# Initial conditions
v0 = 20  # Initial velocity in m/s
angles = np.linspace(0, 90, 100)  # Angles from 0 to 90 degrees

# Calculate range for each angle
ranges = [range_of_projectile(v0, angle) for angle in angles]

# Plot the results
plt.figure(figsize=(8, 6))
plt.plot(angles, ranges, label=f'Initial velocity = {v0} m/s')
plt.title('Range of a Projectile vs. Angle of Projection')
plt.xlabel('Angle of Projection (degrees)')
plt.ylabel('Range (meters)')
plt.grid(True)
plt.legend()
plt.show()
