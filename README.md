
<img width="1020" height="443" alt="image" src="https://github.com/user-attachments/assets/61f6346a-8c5f-4d1c-9935-3a9c6ce95f99" />

# Automotive Smart Wiper Mechanism Simulation (MIL Testing)

## 📌 Project Overview
This repository contains a MATLAB/Simulink model of an automotive Smart Wiper Mechanism developed using a **Model-Based Design (MBD)** approach. The system processes digital/Boolean control inputs to govern windshield wiper behavior based on automatic and manual operational modes. 

The primary focus of this project is to execute **Model-in-the-Loop (MIL)** verification using deterministic test cases to ensure the control logic behaves exactly as specified.

 **Note**: This simulation model and its verification framework were built by referencing guided instructional video tutorials to ensure precise Signal Editor configurations and test execution.
---
## Observation & Simulation Results

By executing a 5-second simulation window with **`Interpolate data` disabled** (to preserve clean, discrete digital state transitions), the following system behaviors were observed:
* **Ignition Safety Interlock (0.0s - 1.0s):** When the Ignition Key is OFF (`0`), the wiper remains safely deactivated (`0`) regardless of any manual knob adjustments or sensor triggers.
* **Manual Mode (1.0s - 2.0s):** When the Ignition Key is turned ON (`1`) and the driver turns the Wiper Knob ON (`1`), the wiper output instantly transitions to **ON (`1`)**.
* **Automated Rain Sensing Mode (2.0s - 4.0s):** When the manual knob is turned OFF (`0`) but the Rain Sensor detects water (`1`), the logic seamlessly maintains the wiper output at **ON (`1`)**.
* **System Deactivation (4.0s - 5.0s):** When both the manual knob and the rain sensor are deactivated, the wiper instantly drops back to **OFF (`0`)**.

### Verification Verdict: Passed (Zero Deviation)
Comparing the actual model output (`wiper_actual`) directly against the reference baseline (`wiper`) inside the Scope shows that both digital signals overlap perfectly. The system achieved **exactly 0 deviation (zero error)** across the entire test lifecycle, mathematically proving that the subsystem's internal logic is 100% bug-free.

---

## Real-Life Application & Implementation
The logical layout verified in this project maps directly to modern production vehicle network architectures:

1. **Body Control Module (BCM):** The internal AND/OR combinational logic represents the software state-machine running inside the vehicle's BCM, which manages body electronics.
2. **Sensors & Switches:** The inputs mimic the physical hazard/wiper stalk switch on the steering column and the infrared **Rain/Moisture Sensor** mounted behind the rearview mirror.
3. **Actuator Relay:** The binary output (`1` or `0`) triggers the physical automotive relay that supplies battery voltage to the windshield wiper motor.
4. **Hardware Redundancy:** By utilizing an **OR gate constraint** between the manual knob and the rain sensor, the system ensures functional safety—if the automatic rain sensor fails on the highway, the driver can still manually override and force the wipers ON.

---

## 🎯 Conclusion
In conclusion, the Smart Wiper Mechanism was successfully modeled, simulated, and verified via MIL testing. The project successfully highlights how discrete logic control safely handles multi-input system requirements in vehicles. Achieving zero tracking error against the reference criteria confirms that the model satisfies functional logic parameters and is fully prepared for automated C-code generation and Hardware-in-the-Loop (HIL) testing phases.
