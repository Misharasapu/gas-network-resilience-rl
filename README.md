# Gas Network Resilience with Q-learning

Clean, employer-friendly snapshot of my Mechanical Engineering IRP exploring how tabular Q-learning can improve gas pipeline pressure resilience during cold spells, using a simulated network in pandapipes.

## Overview

**Problem**  
Cold spells drive demand spikes and effective capacity reductions, creating low-pressure risks in gas networks.  

**Approach**  
Build a pandapipes network, stress it (demand increase, diameter reduction), and train a Q-learning agent to choose discrete interventions (adding strategic sources) that keep minimum junction pressure near a target.  

**Outcome**  
Learned policies stabilize pressure better than random actions and show converging Q-values over episodes.  

---

## Repository Structure

- **src/** → core code (entry point, contains `main.py`)  
- **data/** → small CSVs used by `main.py` (original filenames preserved)  
- **figures/** → plots and images generated during runs  
- **archive/** → legacy scripts and experiments (kept out of main view)  
- **report/** → final project report (PDF)  
- **requirements.txt** → Python dependencies  
- **.gitignore** → standard Python ignores + data files  
- **README.md** → this file  

**Note**  
Data CSVs were moved to `data/` but kept with their original filenames for code consistency.

---

## Quick Start (Windows, Git Bash)

### 1) Clone
git clone https://github.com/Misharasapu/gas-network-resilience-rl.git  
cd gas-network-resilience-rl  

### 2) Create & activate venv
python -m venv .venv  
source .venv/Scripts/activate  

### 3) Install dependencies
pip install -r requirements.txt  

### 4) Run
python src/main.py  

---

## How It Works (high level)

### Simulation (pandapipes)
- Builds a methane network with junctions, pipes, sinks (demands), and an external grid (source).  
- Applies demand increase factors and pipe diameter reduction to emulate cold-spell stress.  
- Runs hydraulic pipeflow and reads junction pressures.  

### State
- Uses the minimum junction pressure (bar) discretized into 0.1-bar bins.  

### Actions
- Discrete choices to add a strategic source at predefined coordinates and connect it to a selected load.  

### Reward
- Encourages minimum pressure near the 25 bar target (within a tolerance), with scaled penalties when drifting away.  

### Agent
- Tabular Q-learning with ε-greedy exploration, learning rate alpha, discount gamma, and decaying epsilon.  

---

## Data
- Small CSVs for nodes, pipes, demands, and source are stored in `data/`.  
- Large datasets are not included.  
- Filenames are unchanged from the original project to avoid code edits.  

---

## Results You Can Expect
- **Pressure stabilization**: Episodes trend toward keeping the minimum pressure within the acceptable band.  
- **Learning curves**: Total reward improves vs. random policy; Q-values converge across episodes.  
- **Visuals**: Plots (learning curves, pressure before/after) appear in `figures/`.  

---

## Notes for Reviewers
- This repo is intentionally simple and readable.  
- The original exploratory notebooks/scripts were moved to `archive/`.  
- Future refactors (e.g., splitting into `gas_network_simulation.py`, `q_learning.py`, etc.) can be added without changing the public API of `main.py`.  

---

## Requirements
See `requirements.txt`. Core libs:  
- python >= 3.10  
- numpy  
- pandas  
- matplotlib  
- pandapipes   

---

## Citation
Sapukotanage, M. (2024). *Improving the Resilience of Pipe Networks to Cold Spells using Machine Learning*.  
Individual Research Project, University of Bristol.  
