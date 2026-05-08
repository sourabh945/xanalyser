# X-Analyser

## Overview

X-Analyser is a Python-based computational tool designed for the analysis and processing of X-Ray Diffraction (XRD) data. It provides automated routines to read spectral data, identify diffraction peaks, perform curve fitting, and calculate physical properties such as crystallite size using the Scherrer equation.

## Features

* **Data Parsing & Extraction:** Easily import `.csv` or `.tsv` files containing raw angle and intensity data.
* **Peak Detection:** The library includes customizable peak finding algorithms (e.g., `peak_finder`, `all_peak`) that identify diffraction peaks based on user-defined baseline and height tolerances.
* **Gaussian Curve Fitting:** Utilizes `scipy.optimize.curve_fit` to accurately fit Gaussian curves to localized XRD peaks, calculating the optimized mean and standard deviation (sigma).
* **FWHM Calculation:** Automatically calculates the Full Width at Half Maximum (FWHM) for specific peaks based on the Gaussian fit.
* **Crystallite Size Estimation:** Estimates the crystal size using an implementation of the Scherrer equation, utilizing an internal constant for the Cu K-alpha wavelength (`lambdak1 = 15.406` Angstroms).
* **Plotting & Visualization:** Includes a wrapper `plot` class to easily visualize raw data and fitted curves using Matplotlib, along with methods to save graphs locally.
* **Export Utilities:** Ability to quickly export newly fitted data and analytical results back into `.csv` format.

## File Structure

* `main.py`: The core library containing the `xrd_data` class, Gaussian mathematical functions, peak detection logic, and plotting mechanisms.
* `plot.py`: A lightweight command-line script that accepts an XRD data file as an argument and immediately plots the angle vs. intensity graph to the screen.
* `not_used.py`: Contains experimental or deprecated code, including a recursive iteration algorithm (`all_peak_finder_rec`) for determining peak bounds.

## Dependencies

This toolkit requires the following Python libraries:

* `pandas` (For reading tabular data structures)
* `numpy` (For mathematical arrays and array operations)
* `matplotlib` (For plotting and visual outputs)
* `scipy` (Specifically `scipy.optimize` for Gaussian curve fitting)

## Example Usage

Using the core library inside a Python environment to process a file with a tab separator:

```python
from main import open_file, xrd_data, plot
import numpy as np

# Load data
loaded = open_file("data.tsv", separator='\t')
angle = np.array(loaded[0])
intensity = np.array(loaded[1])

# Initialize analysis object
data = xrd_data(angle, intensity)

# Find peaks above a specific baseline and height tolerance
peaks = data.peak_finder((1500, 300))

# Plot the first detected peak
plot1 = plot(peaks[0][0], peaks[0][1])
plot1.show()

```
