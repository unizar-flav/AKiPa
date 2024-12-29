# AKiPa
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/unizar-flav/AKiPa/blob/master/AkiPa.ipynb)

## Overview
AKiPa is a python script aimed to analyze the observed rate constants obtained from the KiPaD script, from data obtained from multiwavelength time-resolved absorption spectroscopy by using stopped-flow.

## Usage
This software is developed in Google Colab. To access it, click on the Google Colab badge above or this [link](https://colab.research.google.com/github/unizar-flav/AKiPa/blob/master/AkiPa.ipynb).

**Step 1**: Verify the data's format. It must be a CSV file and with the following structure:

| [L] (μM) | k_obs (1/s)|
|---|---|
|10|115|
|25|135|
|30|150|
|...|...|

Here:
* **k_obs**: Kinetic rates obtaineds from the KiPaD script.
* **[L]**: Concentration of the Ligand added at every experiment from which k_obs is determined.

**Step 2**: Load the libraries, modules and functions *(Modules and functions)*. This step only needs to be performed once regardless of the number of datasets to process.

**Step 3**: Run the next cell *(Upload files)*. A message will appear below it asking the user to select the file to be uploaded.

**Step 4**: The following cell *(Plot experimental data (k_obs))* will plot the k_obs vs [L]. The plot is interactive, allowing zooming via box zoom or wheel zoom. Users can also download the plot as a PNG file.

**Step 5**: The next cell *(Parameters)*, allows the user to first select the fitting model for the data and the modify the initial values of the parameters of the model (which will later be optimized by procesa)
- **fitting**: a dropdown menu that allows to select the method for fitting:
    - **Linear**: executes a linear fitting with the following expression: $k_{obs}= k_{on}\cdot [L] + k_{off}$. Where:
      -  $k_{on}$ is the ligand association rate.
      -  $k_{off}$ is the ligand dissociation rate.
    - **Hyperbolic**: exceutes a hyperbolic fitting with the following expression: $k_{obs}= \frac{[L] \cdot k_{lim}}{[L] + K_d}$
      -  $K_d$ is the equilibrium dissociation constant determined as $K_d = \frac{k_off}{k_on}$.
      -  $k_{lim}$ is the limiting rate constant.

**Step 6**: This cell *(Procesa)* runs the *procesa()* function performns the optimization of the proposed fitting method. The cell will print the residuals at each iteration and when the optimization process is finish it will print the optimized values of the parameters of the model proposed and their standard deviation.

**Step 7**:  The final cell*(Export results)* will gather all the inputted and generated data and save it as a set of CSV and HTML files within a ZIP archive. List of data:
1. Original experimental data
2. Modelled data
3. Intial parameters along with the fitting result from procesa (optimized parameters, their standard deviation, and details from the fitting process)

