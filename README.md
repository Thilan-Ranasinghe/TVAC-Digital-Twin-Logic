# TVAC Digital Twin: Systems Logic & Thermal Architecture 🛰️

## Overview
This repository contains the logical architecture and physical models developed for a **Digital Twin** of a Cryogenic Thermal Vacuum (TVAC) chamber. The goal was to optimize simulation performance while maintaining high-fidelity model-to-test correlation for solar array testing.

---

## 1. Thermo-Physical Foundations
### Nitrogen Property Library (P-h Mapping)
To accurately predict Nitrogen (LN2) behavior in subcooled and two-phase regimes, I developed a property interpolation logic. 

![Nitrogen P-h Curve](Bell_dome_P_H_validation.png)

*The logarithmic Pressure-Enthalpy mapping ensures that the ESATAN-TMS solver respects phase-change boundaries during extreme cooling transients.*

---

## 2. Heat Transfer & Fluid Dynamics
### Dynamic HTC Logic
Heat Transfer Coefficients (HTC) are updated dynamically based on film temperature. 

![HTC Update Flowchart](HTC_mapping_subroutine.png)
![HTC vs T-Film Plot](HTC_T_Film_analysis.png)
![HTC values for differen regimes analysed and simplified through two phase systems](HTC_value_range.png)

*By automating the HTC update loop, the model captures the transition between boiling regimes, a critical factor for cryogenic cooling accuracy.*

---

## 3. Reduced-Order Modeling (ROM)
### The 10-Minute Simulation Logic
The core achievement of this project was reducing a multi-day simulation into a **10-minute runtime** using a physics-based iteration loop.

![Iterative Energy balance used to update LN2 temp by updating enthalpy](Energy_balance_update.png)

*The logic utilizes an energy balance and enthalpy update system to track LN2 temperature states without the computational overhead of a full fluid-node solver.*

---

## 4. Hardware Safety & Control
### PID & Heater Protection interlocks
Industrial TVAC operations require strict safety protocols to protect vacuum panels and heater wires from thermal shock.

![PID Control Flowchart_valve](Cooling_Valve_PID_control_logic.png)
![Heater Wire Dual Function in heating and cooling phase (Control Strategy)](Heater_wire_heating_cooling_logic.png)

*These interlocks ensure the system operates within safe structural limits during rapid heating and cooling cycles.*

## 5. Final Integration of Cooling and Heating Phases

After modeling the control strategies for heating and cooling separately, the models were integrated into a fully automated system. This ensures a seamless transition between thermal extremes during the satellite component testing cycle.

![Full Integration Logic](Integration_of_Heating_and_Cooling_Strategy.png)

*The integrated logic manages the transition between PID-controlled cooling and protected heating cycles, representing the complete automated Digital Twin workflow.*

## 6. Model Validation & Correlation
A critical phase of the thesis was validating the simulated heat flux against established literature and experimental data.

### Physics Validation
By comparing the simulation’s heat flow results with literature-standard boiling curves ($W/m^2$ vs. $\Delta T$), the model's ability to capture the transition from nucleate to film boiling was verified.

![Literature vs simulation Comparison of heat flows](comparison_heat_flux_vs_temp_liter.png)

### Correlation Results
- **Primary Axis ($Y1$):** Transient heat flow ($W$) showing the stabilization of the cryogenic loop.
- **Secondary Axis ($Y2$):** Temperature profile ($K$) tracking the surface-to-fluid gradient.

![Simulated full cylce compared with experimental data](PID_CONTROL_FULL_CYCLE_PANEL_Temp.png)

*The high degree of correlation between the derived heat flow and established physical benchmarks confirms the Digital Twin's reliability for predicting chamber performance during high-load scenarios.*
---

## Technical Tooling
- **Simulation:** ESATAN-TMS
- **Logic Design:** Fortran, LaTeX (TikZ for flowcharts)
- **Data Analysis:** Python (NumPy, Matplotlib), Matlab

*Note: This work was conducted as part of a Bachelor’s Thesis at SpaceTech GmbH in collaboration with the Technical University of Munich (TUM).*
