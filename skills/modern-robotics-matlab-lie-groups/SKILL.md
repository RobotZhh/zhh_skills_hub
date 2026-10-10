---
name: "modern-robotics-matlab-lie-groups"
description: "SE(3)/SO(3) and twist utilities in Modern Robotics MATLAB. Invoke when users need frame transforms, exp/log maps, adjoint maps, or pose validation/projection."
---

# Modern Robotics MATLAB Lie Groups

Use this skill for rigid-body math in `so(3)`, `se(3)`, `SO(3)`, and `SE(3)` with the MATLAB `mr` package.

## Invoke When

- User asks about rotation/pose conversion, e.g. `RpToTrans`, `TransToRp`, `RotInv`, `TransInv`.
- User needs matrix exponential/logarithm on Lie groups, e.g. `MatrixExp3`, `MatrixLog3`, `MatrixExp6`, `MatrixLog6`.
- User needs vector/matrix conversion for twists and angular velocity, e.g. `VecToso3`, `so3ToVec`, `VecTose3`, `se3ToVec`.
- User asks for pose validity checks or nearest valid group element, e.g. `TestIfSO3`, `TestIfSE3`, `ProjectToSO3`, `ProjectToSE3`, `DistanceToSO3`, `DistanceToSE3`.
- User asks for adjoint/`ad` operators or screw-axis primitives.

## Key Functions

- Group and algebra ops: `MatrixExp3`, `MatrixLog3`, `MatrixExp6`, `MatrixLog6`.
- Conversions: `RpToTrans`, `TransToRp`, `VecToso3`, `so3ToVec`, `VecTose3`, `se3ToVec`.
- Validity/projection: `TestIfSO3`, `TestIfSE3`, `ProjectToSO3`, `ProjectToSE3`, `DistanceToSO3`, `DistanceToSE3`.
- Jacobian helpers: `Adjoint`, `ad`, `AxisAng3`, `AxisAng6`, `ScrewToAxis`, `NearZero`, `Normalize`.

## Output Expectations

- Provide MATLAB-ready code snippets.
- State frame convention (space/body) explicitly.
- Include numeric sanity checks for orthonormality or determinant where applicable.
