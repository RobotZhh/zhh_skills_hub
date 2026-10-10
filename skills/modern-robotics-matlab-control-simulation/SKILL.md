---
name: "modern-robotics-matlab-control-simulation"
description: "Computed-torque control and closed-loop simulation in Modern Robotics MATLAB. Invoke when users request tracking control tuning, simulation loops, or torque command validation."
---

# Modern Robotics MATLAB Control And Simulation

Use this skill for controller implementation and simulation workflow in MATLAB `mr`.

## Invoke When

- User asks for computed-torque control (`ComputedTorque`).
- User asks for closed-loop simulation examples (`SimulateControl`).
- User needs end-to-end reference tracking with trajectory + dynamics integration.

## Key Functions

- Control law: `ComputedTorque`.
- Simulation: `SimulateControl`, `EulerStep`, plus dynamics helpers.
- Dependencies often combined with: trajectory functions and `InverseDynamics`/`ForwardDynamics`.

## Output Expectations

- Provide practical gain-tuning guidance (`Kp`, `Ki`, `Kd`) and stability caution.
- Clarify controller/model mismatch assumptions.
- Include simulation metrics (tracking error, torque peak) for validation.
