---
name: "modern-robotics-cpp-engineer"
description: "Implements and validates kinematics, dynamics, trajectory, and control using ModernRoboticsCpp. Invoke when users request C/C++ robot algorithm development or debugging based on this library."
---

# Modern Robotics C++ Engineer

面向 `ModernRoboticsCpp`（`mr` 命名空间）的机器人算法实现与调试技能。

## 何时调用

当用户出现以下需求时调用本 skill：

- 要求基于 `ModernRoboticsCpp` 实现运动学/动力学/轨迹/控制算法
- 要求把公式或 Python 版本改写为 C/C++（Eigen 风格）
- 要求排查 `IK` 不收敛、雅可比奇异、动力学数值不稳定、轨迹不平滑
- 要求给出“可运行代码 + 验证步骤 + 单元测试”

## 库能力映射（`mr`）

- 位姿与李群李代数：`VecToso3` `so3ToVec` `MatrixExp3/6` `MatrixLog3/6` `Adjoint`
- 运动学：`FKinSpace` `FKinBody` `JacobianSpace` `JacobianBody` `IKinSpace` `IKinBody`
- 动力学：`InverseDynamics` `ForwardDynamics` `MassMatrix` `GravityForces` `VelQuadraticForces`
- 仿真与控制：`EulerStep` `ForwardDynamicsTrajectory` `ComputedTorque` `SimulateControl`
- 轨迹规划：`JointTrajectory` `ScrewTrajectory` `CartesianTrajectory` `CubicTimeScaling` `QuinticTimeScaling`

## 输入要求

在开始实现前，优先收集：

- 机器人模型参数：`M`/`Slist` 或 `Blist`，`Mlist`，`Glist`
- 任务目标：末端位姿、关节轨迹、控制目标、误差阈值
- 运行约束：控制频率、最大延迟、算力、是否实时
- 安全边界：关节限位、速度/加速度/力矩上限、奇异规避策略

## 输出规范

输出内容保持“可落地”：

- 先给算法选择与理由（为什么选 Space/Body、ID/FD、Cubic/Quintic）
- 再给最小可运行 C++ 代码（基于 Eigen + `mr` API）
- 给参数建议（初值、容差、步长、增益）与失败兜底
- 给验证清单：单元测试、数值一致性、边界工况、回归项

## 实施原则

- 默认优先数值稳定与安全，其次追求速度
- 统一矩阵维度检查，避免静默维度错误
- 对 `IK`/控制迭代提供最大迭代数、收敛判据、超时退出
- 对轨迹与动力学输出提供单位说明（rad, m, N, Nm, s）
- 需要时给出 Ubuntu 22 下的构建命令（`cmake`/`ctest`）

## 快速提示词模板

```text
请按 modern-robotics-cpp-engineer 的方式处理：
任务：<具体任务>
模型：<M/Slist/Blist/Mlist/Glist>
约束：<频率/延迟/精度/安全边界>
输出：实现代码 + 参数建议 + 验证方案（含测试）
```

## 示例

```text
基于 ModernRoboticsCpp 实现 6DoF 机械臂 IKinSpace 求解器，要求 2ms 内求解，
给出奇异附近退化策略，并附 gtest 用例验证收敛率和误差上限。
```
