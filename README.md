# ABB RobotStudio Component Packaging Simulation

This repository contains a robotic packaging application developed in **ABB RobotStudio** using **RAPID**. The system simulates an industrial pick-and-place workflow in which a robot collects components from three warehouses and packs them into a box carrier with six compartments, based on user-defined product IDs and quantities. :contentReference[oaicite:2]{index=2}

## Project Overview

The robotic cell consists of:

- **three warehouses**: A, B, and C
- **a packaging box carrier** with 6 compartments
- **an ABB industrial robot**
- a simulated **camera-based target update mechanism**

Each warehouse can contain up to 10 components. The user enters how many devices should be packed, as well as their corresponding product IDs. Each product requires a specific combination of components from one or more warehouses. The robot then performs the required pick-and-place sequence automatically. :contentReference[oaicite:3]{index=3}

If the box becomes full, the robot pauses the process, asks the user to replace the box, and continues only after confirmation. The robot also uses camera-generated offsets to simulate real-world variations in component and box positions. :contentReference[oaicite:4]{index=4}

## Main Features

- ABB RobotStudio simulation of a packaging task
- RAPID implementation of robot motion logic
- pick-and-place handling from multiple warehouses
- trajectory planning between home position, warehouses, and box compartments
- user input validation for quantity and product IDs
- automatic component availability check
- box-capacity handling with operator confirmation
- simulated camera offsets for X, Y, and orientation updates
- dynamic target update for warehouse components and packaging positions :contentReference[oaicite:5]{index=5}

## Workcell Description

The workcell contains three storage locations labeled **A**, **B**, and **C**, along with a packaging box. The robot receives the target positions and orientations of the components and box from a simulated camera. The box has six slots, and each slot can hold at most one component. :contentReference[oaicite:6]{index=6}

The system supports packing up to 5 devices per cycle, with valid product IDs in the range **1001–1004**. The robot determines how many components are needed from each warehouse and checks whether the requested order can be fulfilled before starting execution. :contentReference[oaicite:7]{index=7}

## Trajectory Planning

The robot motion is organized around a set of predefined points of interest:

- **Home** position
- approach and pick positions for each warehouse
- approach and place positions for each compartment in the box

The robot uses a combination of:

- **MoveJ** motions for fast approach and return
- **MoveL** motions for precise picking and placing
- different speed settings for transport and manipulation phases

For example, the robot moves from the home position to an approach point above a warehouse using a joint motion at high speed, then descends linearly at lower speed to pick up the component using a vacuum gripper. A similar logic is used for placing components into the packaging box. :contentReference[oaicite:8]{index=8}

## Input Validation and Execution Logic

The system first asks the operator to enter:

1. the number of devices to be packed
2. the list of product IDs

The program validates:
- that the number of devices is between **1 and 5**
- that all entered product IDs are valid (**1001–1004**)

After that, the system calculates how many components are required from each warehouse and checks whether the available stock is sufficient. If the requested number of components exceeds warehouse capacity, the program stops and reports an error. Otherwise, the robot asks the operator for final confirmation before starting the packaging process. :contentReference[oaicite:9]{index=9}

## Box Handling Logic

The packaging box contains 6 compartments. When all compartments are filled, the robot returns to the home position, signals that the box must be replaced, and waits for operator confirmation before resuming operation. During active operation, the digital output `RobotActive` is set to 1. During box replacement, it is set to 0. :contentReference[oaicite:10]{index=10}

## Camera Simulation

A camera simulation function generates random offsets in:

- **X**
- **Y**
- **θ (rotation)**

These offsets are used to update the original targets of both warehouse components and box positions. This mimics real industrial conditions in which parts and containers are not always perfectly aligned. Despite these target variations, the robot continues to perform the packaging task successfully. :contentReference[oaicite:11]{index=11}

## Technologies Used

- **ABB RobotStudio**
- **RAPID programming language**

## Repository Structure

You can adapt this section to your actual file layout.

```text
.
├── RAPID/
│   ├── main.mod
│   ├── trajectories.mod
│   ├── camera.mod
│   ├── input_validation.mod
│   └── packaging_logic.mod
├── images/
│   ├── workcell.png
│   └── trajectories.png
├── reports/
│   └── Izvestaj.pdf
└── README.md# abb-robotstudio-component-packaging
ABB RobotStudio pick-and-place packaging simulation using RAPID, with trajectory planning, warehouse-to-box handling, user input validation, and camera-based target offsets.
