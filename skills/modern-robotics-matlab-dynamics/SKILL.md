---
name: "modern-robotics-matlab-dynamics"
description: "Robot dynamics modeling with Modern Robotics MATLAB. Invoke when users need inverse/forward dynamics, mass matrix, gravity, Coriolis, or wrench-to-torque mapping."
---

# Modern Robotics MATLAB Dynamics

Use this skill for rigid-body manipulator dynamics in MATLAB `mr`.

## Invoke When

- User asks for inverse dynamics torque computation (`InverseDynamics`).
- User asks for forward dynamics acceleration prediction (`ForwardDynamics`).
- User asks for dynamic terms decomposition (`MassMatrix`, `GravityForces`, `VelQuadraticForces`, `EndEffectorForces`).
- User needs trajectory-level dynamics rollout (`InverseDynamicsTrajectory`, `ForwardDynamicsTrajectory`).

## Key Functions

- Core: `InverseDynamics`, `ForwardDynamics`.
- Terms: `MassMatrix`, `GravityForces`, `VelQuadraticForces`, `EndEffectorForces`.
- Batch trajectory: `InverseDynamicsTrajectory`, `ForwardDynamicsTrajectory`, `EulerStep`.

## Output Expectations

- Confirm model inputs (`Mlist`, `Glist`, `Slist`) and units.
- Explain sign convention for gravity and external wrench.
- Provide reproducible MATLAB examples with dimensions checked.
