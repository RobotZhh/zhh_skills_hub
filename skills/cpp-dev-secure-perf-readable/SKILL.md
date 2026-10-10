---
name: cpp-dev-secure-perf-readable
description: 怎么触发 - 你在提需求时明确写上： 按安全性、性能、可读性优先处理 - 任务类型建议用这些词： 实现 、 重构 、 性能优化 、 代码审查 、 修复 bug - 涉及 C/C++ 时，尽量补充约束：输入规模、实时性、平台、编译器、是否多线程 使用示例 - 帮我实现差速底盘局部规划器，20Hz，动态障碍避让，优先安全和稳定。 - 审查这段 EKF 融合代码，重点看时间同步、坐标系和发散风险。 - 重构机械臂 IK 求解模块，要求可读性高、可测、满足 2ms 内计算。
---

---
name: cpp-dev-secure-perf-readable
description: - 安全优先的实现原则（RAII、UB 风险规避、输入校验、并发安全） - 可度量的性能优化准则（复杂度、内存分配、数据局部性、基准验证） - 可维护的可读性规范（职责分离、命名清晰、接口边界明确） - 输出要求与审查启发式（避免“快但不安全”或“过度优化不可维护”）
如何使用 Skills

- 在提需求时直接写清“角色 + 任务 + 约束”，系统会按描述自动匹配对应 skill。
- 触发这个 skill 的关键词建议包含：机器人算法、路径规划、控制器、EKF/UKF、SLAM、标定、实时性、安全约束。
- 需求中补充约束会更准确：机器人平台、传感器类型、控制频率、延迟上限、算力、是否上实机。
- 一个提示词模板： 请按 robot-algorithm-engineer 的方式处理：<任务>，约束 <实时性/精度/安全边界>，输出实现+验证方案。
使用示例

- 帮我实现差速底盘局部规划器，20Hz，动态障碍避让，优先安全和稳定。
- 审查这段 EKF 融合代码，重点看时间同步、坐标系和发散风险。
- 重构机械臂 IK 求解模块，要求可读性高、可测、满足 2ms 内计算。


---

---
name: "cpp-dev-secure-perf-readable"
description: "Guides secure, high-performance, readable C/C++ development. Invoke when writing, reviewing, refactoring, or debugging C/C++ code."
---

# C/C++ Secure-Performance-Readability Guide

Use this skill to produce C/C++ code that balances three priorities:
- Security first (memory safety, input validation, undefined behavior avoidance)
- Performance with evidence (algorithmic and low-level efficiency)
- Readability and maintainability (clear structure, naming, and contracts)

Invoke this skill when:
- The user asks to write or modify C/C++ code
- The user asks for code review, refactor, optimization, or bug fixing in C/C++
- The task includes constraints about safety, speed, reliability, or long-term maintenance

## Core Workflow

1. Clarify objective and constraints
- Identify correctness requirements, expected input sizes, latency/throughput limits, portability targets, and compiler/toolchain constraints.
- Prefer explicit assumptions over implicit behavior.

2. Design for correctness and safety first
- Minimize raw ownership. Prefer RAII, stack allocation where practical, and smart pointers with clear ownership semantics.
- Eliminate undefined behavior risks: bounds checks, integer overflow awareness, lifetime correctness, strict aliasing correctness, valid initialization.
- Validate all untrusted inputs and fail early with explicit error handling.
- Avoid dangerous C APIs when safer alternatives exist.

3. Implement with performance-aware structure
- Choose data structures and algorithms based on complexity and cache behavior.
- Reduce allocations and copies in hot paths; use move semantics and reserve capacity where appropriate.
- Keep branch behavior predictable and avoid unnecessary virtual dispatch in critical paths.
- Measure before/after for non-trivial optimizations; avoid premature micro-optimization.

4. Preserve readability
- Use descriptive names, small focused functions, and clear interfaces.
- Separate policy from mechanism; isolate platform-specific code.
- Keep control flow simple; reduce hidden side effects and deeply nested logic.

5. Verify and harden
- Compile with strict warnings and treat warnings seriously.
- Use sanitizers in debug/testing where possible (ASan, UBSan, TSan as applicable).
- Add/adjust tests for boundary cases, invalid input, and error paths.
- Check thread safety assumptions for shared state.

## Security Checklist (C/C++)

- Memory and lifetime
  - No use-after-free, double-free, dangling references, or invalidated iterators.
  - No out-of-bounds reads/writes.
  - Clear ownership model for every resource.

- Input and parsing
  - Validate lengths, ranges, and formats before processing.
  - Defend against integer overflow/underflow in size and index calculations.
  - Handle malformed inputs without crashes or undefined behavior.

- API and error handling
  - Return explicit errors (status, expected-like patterns, or exceptions per project style).
  - Never ignore critical return values.
  - Avoid leaking sensitive data in logs/errors.

- Concurrency
  - Protect shared mutable state with clear synchronization strategy.
  - Avoid data races and deadlocks through lock ordering or lock-free discipline.

## Performance Checklist (C/C++)

- Use appropriate complexity and data locality
- Reduce heap churn (pooling/reserve/reuse when justified)
- Avoid needless temporary objects and string copies
- Prefer `std::string_view`/`span`-like non-owning views when safe
- Benchmark representative workloads before accepting optimization claims

## Readability Checklist (C/C++)

- One responsibility per function/module
- Explicit invariants and pre/post conditions in code structure
- Consistent naming/style with project conventions
- Minimal macro complexity; prefer constexpr/templates where clearer
- Keep headers clean; reduce coupling and include bloat

## Output Requirements for This Skill

When responding to a C/C++ task:
- Explain key trade-offs among security, performance, and readability.
- Provide production-quality code changes aligned with existing project conventions.
- Include concise verification steps (build/tests/sanitizer suggestions).
- Highlight risk points and how they were mitigated.

## Review Heuristics

Reject or revise solutions that:
- Improve speed by introducing UB risk
- Increase safety but create avoidable performance regressions in hot paths
- Optimize aggressively at the cost of maintainability without evidence

Prefer solutions that:
- Are correct and safe by construction
- Are measurable and efficient where it matters
- Remain easy to understand and extend