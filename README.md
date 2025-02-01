# gnuplot
## Analyzing and Visualizing Interaction Energies with GROMACS and Gnuplot

This section explains how to analyze interaction energies from GROMACS simulation data and visualize them using Gnuplot.

### Step 1: Analyze Interaction Energy Data
Use the following command to analyze the interaction energy data and calculate the autocorrelation function:

```bash
gmx_mpi analyze -f interaction_energy.xvg -ac

gnuplot -e "
set terminal png size 800,600;
set output 'interactionenergy_with_reference.png';
set title 'Energy vs Time';
set xlabel 'Time (ps)';
set ylabel 'Energy (kJ/mol)';
set grid;
plot 'interaction_energy.xvg' using 1:2 with lines title 'Pressure' linecolor rgb 'purple', \
     'interaction_energy.xvg' using 1:2 smooth sbezier with lines title '10-ps Running Avg' linecolor rgb 'red';"

Explanation of the Plot
Input File: interaction_energy.xvg
Output File: interactionenergy_with_reference.png
Graph Details:
X-Axis: Time (ps)
Y-Axis: Energy (kJ/mol)
Grid: Added for better readability.
Purple Line: Raw interaction energy data.
Red Line: Smoothed data showing a 10-ps running average using Bezier smoothing.

# Gnuplot RMSD and Interaction Energy Analysis

This repository contains Gnuplot scripts for generating high-quality plots comparing RMSD (Root Mean Square Deviation) and interaction energy data. The plots are used to visualize and compare data from molecular dynamics simulations and reference structures.

## Requirements
- Gnuplot installed on your system.
- GROMACS (for interaction energy analysis).

## Files
- `rmsd.xvg`: RMSD data from the molecular dynamics simulation.
- `rmsd_xtal.xvg`: RMSD data from the crystal structure.
- `interaction_energy.xvg`: Interaction energy data from a GROMACS simulation.
- `gnuplot_script`: The Gnuplot script used to generate the plots.

## RMSD Comparison

To generate an RMSD comparison plot, run the following command in your terminal:

```bash
gnuplot -e "
set terminal pngcairo size 1000,700 enhanced font 'Arial,16';
set output 'rmsd_clean.png';

set title 'RMSD Comparison' font ',18';
set xlabel 'Time (ns)' font ',16';
set ylabel 'RMSD (nm)' font ',16';
set key top left box font ',14';

set grid lw 1 lc rgb 'gray80';
set border lw 1.5;

set xrange [0:*];
set yrange [0:*];

set style line 1 lt 1 lw 0.7 lc rgb 'black';
set style line 2 lt 1 lw 0.7 lc rgb 'red';

plot 'rmsd.xvg' using 1:2 with lines linestyle 1 smooth csplines title 'Ref: Equilibrated', \
     'rmsd_xtal.xvg' using 1:2 with lines linestyle 2 smooth csplines title 'Ref: Crystal';
"


Notes
Make sure you have Gnuplot installed on your system.
Ensure the file interaction_energy.xvg is in the working directory before running these commands.


