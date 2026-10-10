---
name: "modern-robotics-matlab-kinematics"
description: "Forward/inverse kinematics and Jacobians with Modern Robotics MATLAB. Invoke when users ask for FK, IK, body/space Jacobians, and screw-axis modeling."
---

# Modern Robotics MATLAB Kinematics

Use this skill for manipulator kinematics with the MATLAB `mr` package.

## Invoke When

- User asks for forward kinematics in space/body frame (`FKinSpace`, `FKinBody`).
- User asks for inverse kinematics with iterative solvers (`IKinSpace`, `IKinBody`).
- User needs Jacobian computation (`JacobianSpace`, `JacobianBody`).
- User needs screw-axis setup or body/space frame conversion support.

## Key Functions

- FK: `FKinSpace`, `FKinBody`.
- IK: `IKinSpace`, `IKinBody`.
- Jacobians: `JacobianSpace`, `JacobianBody`.
- Supporting transforms: `Adjoint`, `TransInv`, `RpToTrans`, `TransToRp`.

## Output Expectations

- Clarify inputs: home pose `M`, screw list (`Slist` or `Blist`), and joint vector `thetalist`.
- Provide convergence settings for IK (`eomg`, `ev`) and initial guess guidance.
- Include frame-consistency notes to avoid body/space mismatch.
