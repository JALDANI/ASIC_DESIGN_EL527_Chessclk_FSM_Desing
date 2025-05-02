# Chess Clock FSM Design (EL527 ASIC)

This repository contains the Verilog RTL, testbenches, QFlow scripts, layout files, and reports for the digital Chess Clock Finite State Machine (FSM) project developed for the EL527 ASIC Design course at DAU, Gandhinagar.

## Table of Contents

* [Project Overview](#project-overview)
* [Repository Structure](#repository-structure)
* [Prerequisites](#prerequisites)
* [Getting Started](#getting-started)

  * [Simulation](#simulation)
  * [Synthesis with QFlow](#synthesis-with-qflow)
* [File Descriptions](#file-descriptions)
* [Authors](#authors)


## Project Overview

The Chess Clock FSM implements a two-player chess clock using a Finite State Machine in Verilog. Each player has an independent countdown timer; only one timer is active at a time. The FSM supports the following states:

* **Stop**: Both timers halted (default/reset state)
* **RunA**: Player A's timer running
* **RunB**: Player B's timer running
* **Wait**: Both timers paused (simultaneous button press)

Key features:

* Debounced button inputs for reliable turn switching
* Mutual exclusion: only one timer runs at any time
* QFlow-based ASIC flow: synthesis, placement, routing, STA
* Waveform testbenches covering all state transitions

## Repository Structure

```
├── code/
│   ├── chessclkfsm.v         # Verilog FSM module
├── qflow/                    # QFlow flow scripts and config
│   ├── synth.ys              # Yosys synthesis script
│   ├── place.layout         # Placement constraints
│   ├── route.config          # Routing config
│   └── sta.tcl               # STA commands
├── layouts/                  # Magic layout & GDS files
├── images/                   # Block diagrams, FSM state diagram, waveforms
├── reports/                  # Logs and STA reports
│   ├── synth.log
│   ├── place.log
│   ├── route.log
│   └── sta.log
└── README.md                 # This file
```

## Prerequisites

* **Verilog simulator** (e.g. Icarus Verilog, ModelSim)
* **GTKWave** for waveform viewing
* **QFlow** open‑source ASIC flow (Yosys, GrayWolf, QRouter, Magic)
* **Standard cell library** (provided in `qflow/lib`)

## Getting Started

### Simulation

1. Navigate to the `code/` directory:

   ```bash
   cd code
   ```

2. Compile the Verilog code and testbench:

   ```bash
   iverilog -o tb.vvp chessclkfsm.v debounce.v testbench.v
   ```

3. Run the simulation:

   ```bash
   vvp tb.vvp
   ```

4. Open the resulting `.vcd` file in GTKWave:

   ```bash
   gtkwave dump.vcd
   ```

### Synthesis with QFlow

1. Copy the `code/*.v` files into your QFlow project RTL directory.

2. In the `qflow/` folder, run:

   ```bash
   qflow synth -d myproject
   qflow place -d myproject
   qflow route -d myproject
   ```

3. Perform static timing analysis:

   ```bash
   vesta myproject/sta.log
   ```

4. View layout in Magic:

   ```bash
   magic -rcfile qflow.magicrc myproject/myproject.mag
   ```

## File Descriptions

| File            | Description                                           |
| --------------- | ----------------------------------------------------- |
| `chessclkfsm.v` | FSM module controlling two timers                     |
| `synth.ys`      | Yosys script for RTL-to-gate-level synthesis          |
| `place.layout`  | Placement constraints and floorplan directives        |
| `route.config`  | QRouter configuration file                            |
| `sta.tcl`       | Tcl script for Vesta static timing analysis           |
| `layouts/*.mag` | Magic layout files                                    |
| `reports/*.log` | Flow logs: synthesis, placement, routing, STA         |

## Authors

* **[Jal Dani](https://github.com/JALDANI)** <[202201315@daiict.ac.in](mailto:202201315@daiict.ac.in)>
* **[Preet Dave](https://github.com/DavePreet)** <[202201072@daiict.ac.in](mailto:202201072@daiict.ac.in)>

Course: ASIC Design (EL527), DAU, Gandhinagar

