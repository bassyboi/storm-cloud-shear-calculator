# Storm Calculator: CAPE Efficiency and Missing Parameter Solver

This is a dynamic storm calculator designed for field meteorologists and researchers. The tool accepts exactly two of three key storm parameters and an optional lightning strikes value, then "solves" for the missing parameter and calculates the effective updraft speed along with other derived values.

## Overview

The storm calculator uses the following key relationships:

1. **Effective Updraft Speed Calculation:**

   The updraft speed (\(w\)) is given by:
   \[
   w = \alpha \times \sqrt{2 \times \text{CAPE}} \times D
   \]
   - **CAPE (J/kg):** Convective Available Potential Energy.
   - **\(\alpha\) (Efficiency Factor):** Derived from the lightning strikes per minute (capped at 90%).
   - **\(D\) (Drag Factor):** A multiplier computed from the storm height, which is itself a function of CAPE.
   
2. **Effective Advective Wind Relationship:**
   
   The effective side wind that helps tilt the storm is given by:
   \[
   U_{\text{eff}} = w \times \tan(\theta)
   \]
   - **\(\theta\) (Storm Tilt Angle in degrees):** Observed tilt of the storm.

3. **Storm Height Calculation:**
   
   If CAPE is available, the storm height is computed as:
   \[
   \text{Storm Height} = 4000 + 2\sqrt{\text{CAPE}} \quad \text{(in meters)}
   \]
   If CAPE is missing, a default height of 4000 m is assumed.

4. **Input Requirements:**
   
   - Exactly **two** of the following three inputs must be provided:
     - **CAPE** (J/kg)
     - **Bulk Wind Shear** (in knots)
     - **Storm Tilt Angle** (in degrees)
   - Optionally, you can enter the lightning strikes per minute (default is 50 if not provided), which influences the efficiency factor \(\alpha\).

5. **Missing Parameter Solution:**
   
   Depending on which parameter is missing, the calculator uses the relationships defined above to solve for it:
   - If **Angle** is missing, it uses the provided CAPE and shear.
   - If **Shear** is missing, it solves based on CAPE and tilt.
   - If **CAPE** is missing, it assumes a default storm height (4000 m) and computes CAPE from the provided shear and tilt.

6. **Units and Conversions:**
   
   The effective updraft speed is presented in:
   - Meters per second (m/s)
   - Knots (conversion factor: 1 m/s ≈ 1.94384 knots)
   - Kilometers per hour (km/h) (conversion factor: 1 m/s ≈ 3.6 km/h)

## How It Works (In Plain Language)

1. **User Inputs:**
   - Enter exactly **two** out of the following:
     - CAPE (the energy available for a storm, in J/kg)
     - Bulk Wind Shear (the change in wind speed with height, in knots)
     - Storm Tilt Angle (how much the storm is leaning, in degrees)
   - Optionally, you can provide the number of lightning strikes per minute; this value adjusts the efficiency factor \( \alpha \), which is capped at 90%.

2. **Calculations:**
   - The tool calculates the ideal updraft speed from CAPE using the formula \( \sqrt{2 \times \text{CAPE}} \).
   - This ideal speed is then reduced by the efficiency factor (from lightning activity) and adjusted by a drag factor, which is computed based on the storm height.
   - The effective updraft speed is finally used along with the storm tilt to derive the effective advective wind (\( U_{\text{eff}} \)).

3. **Output:**
   - The calculator displays all three key parameters (CAPE, shear, and tilt) along with the computed efficiency, the storm height, and the effective updraft speed, with wind speed conversions in m/s, knots, and km/h.

## Files

- **index.html**: The main HTML file that contains the user interface, CSS styling, and JavaScript logic for the calculator.


## Usage Example

- If you input:
  - **CAPE** = 2000 J/kg
  - **Bulk Wind Shear** = 30 knots
  - (Leave the Storm Tilt Angle blank)
  
  The tool will calculate the missing tilt angle based on the other inputs and display:
  - The computed tilt (in degrees)
  - The effective updraft speed in m/s, knots, and km/h
  - The efficiency factor and the computed storm height.

## Contributing

Feel free to fork this repository and contribute improvements or fixes. Pull requests are welcome!

## License

This project is provided under the MIT License.

---

_Enjoy using the Storm Calculator to better understand your storm observations!_
