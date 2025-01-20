# Storm Calculator

The **Storm Calculator** is a web-based tool for solving key storm dynamics parameters (CAPE, bulk wind shear, and tilt angle) based on a set of physical relationships used in convective meteorology. This tool calculates the effective updraft speed from CAPE while dynamically adjusting for air density changes with altitude. It then uses this effective updraft to derive the storm shear and tilt angle relationships.

> **Key Features:**
> - **Dynamic Air Density:** Computes air density at the storm height using a simplified barometric formula.
> - **Drag-Adjusted Updraft Speed:** Adjusts the ideal updraft speed (√(2×CAPE)) by a 60% realization factor and a drag factor depending on storm height and air density.
> - **Interactive Input:** Solve for exactly two parameters (CAPE, shear [in knots], or tilt angle) to determine the third.
> - **Built-in Iterative Solver:** Uses a bisection method to solve for CAPE when it is the missing parameter.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation and Usage](#installation-and-usage)
- [Code Explanation](#code-explanation)
- [Contributing](#contributing)
- [License](#license)

## Overview

The calculations implemented in this tool are based on the following relationships:

- **Updraft Speed:**  
  The ideal updraft speed is calculated as:  
  \[
  w_{\text{ideal}} = \sqrt{2 \times \text{CAPE}}
  \]
  Only 60% of this theoretical speed is realized, so:
  \[
  w = \alpha \times \sqrt{2 \times \text{CAPE}} \quad (\alpha = 0.6)
  \]

- **Drag Factor:**  
  The effective updraft is further reduced by a drag factor:  
  \[
  D = 1 - \frac{C_d \times \rho(z) \times z}{k}
  \]
  where:
  - \( C_d = 0.8 \) is the drag coefficient,
  - \( \rho(z) \) is the air density computed at the storm height \( z \),
  - \( k = 1 \times 10^6 \) is a scaling constant.
  
- **Storm Height:**  
  The storm height is approximated as a function of CAPE:
  \[
  z = 4000 + 2\sqrt{\text{CAPE}}
  \]
  
- **Shear (ΔV):**  
  The effective wind shear is then given by:
  \[
  \Delta V = 2 \times w \times \tan(\theta)
  \]
  where \( \theta \) is the storm tilt angle.

If the user inputs exactly two of the three variables (CAPE, shear in knots, or tilt angle), the missing parameter is computed from the remaining two.

## Features

- **Dynamic Air Density Computation:**  
  Uses the barometric formula:
  \[
  \rho(z) = \rho_0 \left(\frac{T(z)}{T_0}\right)^{\frac{g}{R \cdot L} - 1}
  \]
  where the temperature at altitude \( T(z) \) is given by:
  \[
  T(z) = T_0 - L \times z
  \]

- **Interactive Web Interface:**  
  A clean user interface built with HTML, CSS, and JavaScript allows users to input values and view results.

- **Bisection Method for CAPE:**  
  When CAPE is the missing variable, a bisection solver is employed to handle the nonlinear dependency in the calculation.

