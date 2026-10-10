---
name: "modern-robotics-matlab-trajectory"
description: "Joint/cartesian/screw trajectory generation in Modern Robotics MATLAB. Invoke when users ask for time scaling, waypoint interpolation, or pose trajectory synthesis."
---

# Modern Robotics MATLAB Trajectory Planning

Use this skill for reference trajectory generation using MATLAB `mr`.

## Invoke When

- User needs joint-space interpolation (`JointTrajectory`).
- User needs Cartesian-space interpolation (`CartesianTrajectory`).
- User needs screw-motion interpolation (`ScrewTrajectory`).
- User asks for time-scaling profiles (`CubicTimeScaling`, `QuinticTimeScaling`).

## Key Functions

- Trajectories: `JointTrajectory`, `CartesianTrajectory`, `ScrewTrajectory`.
- Time scaling: `CubicTimeScaling`, `QuinticTimeScaling`.

## Output Expectations

- Specify total duration `Tf`, sample count `N`, and method index clearly.
- Highlight continuity differences between cubic and quintic profiles.
- Include quick plotting snippets for position/velocity sanity checks.
