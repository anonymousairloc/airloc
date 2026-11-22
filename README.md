# AirLoc: interactive simulation

Anonymous artifact for a paper under double-blind review.

`index.html` is a single self-contained page. It loads no external resources and contains no analytics or tracking.

## Simulation, not recorded data

Range and angle measurements are generated from the error trends reported in Fig. 1 of the paper: range error grows with distance (about 35 cm at 10 m), and angle error grows with the bearing to the tag (about 0.2 rad behind the user). The page shows how the algorithms behave. Its numbers are illustrative and are not the paper's experimental results.

## What you can do

- Walk a testbed with the arrow keys or WASD, or press **Auto-walk**.
- Drag any tag to relocate it.
- Switch between the **multilateration baseline** (tags at surveyed positions, as in [11]) and **AirLoc** (no tag position known; one fixed tag anchors the map).
- Change the parameters studied in the paper: tag selection, number of selected tags k, observation weighting, and the exponents n_d and n_a of Eq. 4.
- Compare relocation handling:
  - **Default:** the method as described in the paper. The full graph is kept, and each tag has one landmark node.
  - **Landmark versioning:** the planned fix, not in the paper. When new observations of a tag disagree with its landmark beyond the ranging noise, a new landmark node is started. Old observations stay on the old node and still constrain the past trajectory.
  - **Robust kernel:** listed as future work in the paper.

## Implementation notes

- Odometry comes from simulated pedestrian dead reckoning (step length and heading with noise and gyroscope drift).
- At each step, the k nearest tags in range are admitted and weighted by Eq. 4.
- The GraphSLAM problem of Eq. 3 is re-optimized every Δ poses over the full trajectory. The normal equations are solved exactly with a Schur complement on the landmarks, so the page stays responsive for long walks.
- The campus and apartment layouts are schematic approximations of the two testbeds, not the surveyed floor plans.

## Run locally

Download `index.html` and open it in any modern browser. No build step or server is needed.

## Code and data

The full implementation and the recorded logs will be released after the review.
