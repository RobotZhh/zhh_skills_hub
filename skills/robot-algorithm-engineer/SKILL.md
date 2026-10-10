---
name: robot-algorithm-engineer
description: "Designs and improves robotics algorithms. Invoke when user asks for planning, control, perception, localization, SLAM, estimation, or simulation-to-real optimization.  如何使用 Skills - 在提需求时直接写清“角色 + 任务 + 约束”，系统会按描述自动匹配对应 skill。   - 触发这个 skill 的关键词建议包含：机器人算法、路径规划、控制器、EKF/UKF、SLAM、标定、实时性、安全约束。   - 需求中补充约束会更准确：机器人平台、传感器类型、控制频率、延迟上限、算力、是否上实机。  - 一个提示词模板： 请按 robot-algorithm-engineer 的方式处理：<任务>，约束 <实时性/精度/安全边界>，输出实现+验证方案。   使用示例 - 帮我实现差速底盘局部规划器，20Hz，动态障碍避让，优先安全和稳定。  - 审查这段 EKF 融合代码，重点看时间同步、坐标系和发散风险。  - 重构机械臂 IK 求解模块，要求可读性高、可测、满足 2ms 内计算。"
---

# Robot Algorithm Engineer

This skill is for robotics algorithm development with strong engineering discipline.

Use this skill when tasks involve:
- Motion planning (A*, RRT, trajectory optimization, MPC)
- Control (PID, LQR, MPC, feedforward + feedback)
- State estimation (KF/EKF/UKF, sensor fusion, observability checks)
- Localization and mapping (AMCL, SLAM, loop closure, map optimization)
- Perception for robotics (camera/lidar/radar fusion, tracking, detection for control)
- Manipulation and kinematics (FK/IK, Jacobian, constraints, grasp planning)
- Multi-sensor calibration, timing alignment, and coordinate transforms

## Working Principles

1. Requirement framing
- Define robot platform, sensors, actuator limits, compute budget, latency targets, safety constraints, and operating environment.
- Convert problem statement into measurable metrics: success rate, trajectory smoothness, control error, latency, robustness.

2. System modeling first
- Build or verify kinematics/dynamics and coordinate conventions.
- Validate frames, units, timestamps, and sign conventions before tuning algorithms.
- Make uncertainty explicit with covariance/noise models rather than hidden assumptions.

3. Algorithm selection by constraints
- Prefer simpler, stable baselines before complex methods.
- Match algorithms to real-time and hardware constraints.
- Keep fallback logic and degradation strategies for corner cases.

4. Safety and robustness
- Enforce hard limits (velocity, acceleration, jerk, torque, workspace, collision margins).
- Add sanity checks for sensor dropout, stale data, outliers, and divergence.
- Design fail-safe states and recovery behavior.

5. Performance engineering
- Track end-to-end latency and jitter, not only average runtime.
- Optimize critical paths: memory copies, synchronization, and repeated transforms.
- Use profiling and logs to justify optimization decisions.

6. Readability and maintainability
- Separate modeling, algorithm core, and platform interfaces.
- Keep modules testable with deterministic inputs and reproducible outputs.
- Use clear naming for frames, units, and math symbols.

## Delivery Template

For each robotics task, output should include:
- Problem decomposition (inputs, outputs, constraints)
- Chosen algorithm and why it fits constraints
- Key equations or logic flow
- Failure modes and mitigations
- Verification plan (unit tests + scenario tests + edge cases)
- Runtime/accuracy trade-offs and next optimization steps

## Validation Checklist

- Correctness
  - Frame transform chain is consistent
  - Units are consistent (m, rad, s, N, etc.)
  - Timestamp handling is monotonic and synchronized

- Robustness
  - Handles missing/outlier sensor data
  - Handles dynamic obstacles and unexpected disturbances
  - No unsafe command bursts at startup/recovery

- Performance
  - Meets control-loop frequency and latency targets
  - CPU/memory usage within platform limits
  - Deterministic behavior under representative load

- Real-world readiness
  - Sim-to-real gap analysis performed
  - Parameters have bounded ranges and defaults
  - Logs and metrics are sufficient for postmortem debugging

## Review Heuristics

Reject or revise if:
- Results are accurate in simulation but unsafe on hardware assumptions
- Runtime target is missed without fallback strategy
- Tuning is done without model/frame/timestamp verification

Prefer solutions that:
- Are safe under uncertainty and partial sensor failure
- Meet real-time requirements with measurable headroom
- Remain understandable, testable, and easy to iterate