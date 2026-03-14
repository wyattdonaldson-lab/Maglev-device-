# Active Magnetic Levitation via PID Control

A closed-loop control system that stabilizes a ferromagnetic object in mid-air. This project demonstrates real-time hardware interfacing and control theory, using an IR sensor for position feedback to dynamically adjust the magnetic field of an electromagnet.

## The Physics & Control Logic
Magnetic levitation of a passive object is inherently unstable (Earnshaw's theorem). To maintain levitation, the system requires continuous, active adjustments to the magnetic field based on the object's position. 

This project solves the instability using a custom-tuned Proportional-Integral-Derivative (PID) controller:
* **Proportional (Kp = 0.4):** Provides the baseline restoring force based on the current distance from the setpoint.
* **Integral (Ki = 0.0005):** Eliminates steady-state error, compensating for the static weight of the levitating object. Includes anti-windup clamping to prevent system runaway.
* **Derivative (Kd = 15.0):** Provides critical damping. Because the magnetic force follows an inverse-square law, the system is highly volatile. The heavily weighted derivative term predicts the object's trajectory and applies braking force to prevent oscillations.

## Hardware Architecture
* **Microcontroller:** Arduino (Handles ADC reads, PID calculations, and PWM generation).
* **Motor Driver:** LMD18201 H-Bridge (Delivers high-current PWM to the electromagnet).
* **Actuator:** 12V DC Electromagnet 
* **Feedback Sensor:** Analog Infrared (IR) distance sensor.

**Note on Tuning:** The current PID gains (Kp, Ki, Kd) are tuned for my specific electromagnet and object mass. If you change the object's weight or the coil geometry, you will need to re-tune the loop.
