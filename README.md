# README Monte Carlo‑simulation of monomers- and polymers

**Course:** TMA4320 Introduksjon til vitenskapelige beregninger (NTNU)  
**Semester:** Spring 2022  
**Institution:** NTNU, Department of Physics  

## Overview
This repository contains a Monte Carlo (Metropolis) simulation project investigating how electrostatic interactions and polymer multivalency can drive liquid–liquid phase separation and the formation of membrane-less organelles (clusters/droplets) in cells.

In this simplified model, oppositely charged monomers/polymers move on a 2D periodic lattice (an `N × N` grid). Interactions are short-ranged, where only nearest-neighbor charge–charge interactions contribute to the energy. The system is evolved using the Metropolis algorithm, and clustering is quantified as a function of temperature and multivalency (polymer length).

## What this repo demonstrates

- Implementation of the Metropolis Monte Carlo algorithm (Markov Chain Monte Carlo)
- Design of a discrete physical model with tunable parameters (temperature, interaction strength, system size)
- Simulation of interacting systems on a 2D lattice with periodic boundary conditions
- Energy-based state transitions using Boltzmann-weighted acceptance criteria
- Recursive connected-component detection (cluster labeling)
- Statistical estimation of equilibrium properties (mean cluster size and cluster count)
- Analysis of system behavior under varying control parameters
- Comparison of different dynamical models (rigid vs. flexible movement rules)
- Performance optimization using Numba JIT compilation
- Reproducible scientific visualization using NumPy and Matplotlib


## What is implemented
### 1) Monomer systems (L = 1)
- Random initialization of `M` positive and `M` negative monomers on an `N × N` grid
- Periodic boundary conditions (torus geometry)
- Energy calculation using nearest-neighbor electrostatic interactions
- Metropolis Monte Carlo simulation
- Cluster detection (connected components on the lattice, 4-neighborhood)
- Estimation of mean cluster size ⟨d⟩ as a function of temperature

### 2) Polymer systems (L > 1)
- Random initialization of `M` positive and `M` negative polymers, each with `L` monomers
- Energy calculation excluding interactions within the same polymer
- Two polymer move models:
  - Rigid move: entire polymer attempts to move as a unit; move rejected on collision
  - Medium flexibility move: rows/columns blocked by collisions stay; collision-free parts move
- Polymer integrity check (reject move if polymer becomes “broken” / disconnected)
- Large-scale simulations measuring:
  - ⟨d⟩/L (mean cluster size normalized by multivalency)
  - ⟨m⟩ (mean number of clusters; interpreted as number of organelles)

## Model assumptions (simplifications)
- Movement restricted to a discrete 2D grid
- Nearest-neighbor only interactions (screening in aqueous solution)
- No diagonal connectivity for clusters/polymers (4-neighborhood)
- Polymers do not twist/rotate in 3D; movement is horizontal/vertical only
- Parameter choices (e.g., grid spacing) are chosen for computational feasibility, not biological realism

## Requirements
- `Python 3`
- `numpy`
- `matplotlib`
- `numba` (optional but strongly recommended for speed)

Install dependencies:
```bash
pip install numpy matplotlib numba



