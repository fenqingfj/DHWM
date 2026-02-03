# 孤岛索引（1-10：正规名称与作用）

## 系统总览（离形全息宇宙型世界大模型）

如果只看“孤岛列表”，容易误解系统只是若干测试用例。实际上，孤岛是 DHWM（离形全息宇宙型世界大模型）的**产品级质量门禁与强证据链**：它们把“智能体现”落成可审计的世界状态、可执行的动作闭环与可复现的统计结论。

- 系统详细设计与作用（对外说明）：[DHWM_SYSTEM_DESIGN_CN.md](DHWM_SYSTEM_DESIGN_CN.md)

本项目将验证任务统一编号为“孤岛 1-10”。产物通常是 JSON/MD 证据包，并带有稳定的语义字段，便于审计与自动化门禁：

- `suite`: strict / hard / ultra / open
- `island_id`: 1-10
- `island_name`: 稳定别名（machine-readable）
- `island_title`: 正式名称（human-readable）

其中：
- `strict/hard/ultra`：用于孤岛 1-9 的“无训练可复现”验收与回归
- `open`：用于孤岛10（以及 Open 变体链路）的“对外世界逼近 + 漂移/代价闭环”评测

## 无训练说明（Strict 验收口径）

孤岛 1-9 的验收与审计目标是：在 **无训练/无权重更新** 的条件下，验证系统能否在受控任务上运行并产出可复现证据。

- “无训练”指运行过程中不进行参数学习或模型权重更新；随机性通过固定 seed 保证可复现
- 这不否认系统是 AI 系统：它是一个以世界状态、规则/现象演化、与可审计推理管线为核心的 AI/世界模型系统
- 同时也不自动等价于 AGI：AGI 需要外部不可控任务与更强泛化证明

## 任务一览（孤岛 1-9：Strict）
| Island | island_name | island_title | 核心作用（验证点） | 典型指标（summary 中） |
|---:|---|---|---|---|
| 1 | nbody_gravity_orbit | N-Body Gravity (Orbit Stability) | 动力学演化与轨道有界性 | r_min, r_max, extrema |
| 2 | counterfactual_ecosystem_lv | Counterfactual Ecosystem (Lotka-Volterra) | 反事实干预与因果可测差异 | rabbit_peak/trough, grass_trough/recover |
| 3 | micro_macro_economy | Micro-to-Macro Economy (Shock Response) | 微观扰动到宏观指标映射 | base/shock gdp, unemployment |
| 4 | structure_discovery_wl | Structure Discovery (WL Fingerprint) | 结构同构识别与指纹稳定性 | fingerprint_hist, degree |
| 5 | lever_equilibrium | Physics Intuition (Lever Equilibrium) | 约束求解与物理一致性 | residual, hand_energy |
| 6 | coupled_evolution | Creativity (Coupled Evolution) | 耦合演化导致结构趋同 | d0, d1 |
| 7 | three_body_chaos | Three-Body Chaos (Lyapunov + Energy) | 混沌系统稳定性与能量漂移 | energy_error, rmse, lyapunov_est |
| 8 | dark_forest | Dark Forest (Stealth/Aggression Emergence) | 多主体对抗环境下涌现策略 | survival_rate, stealth_emergence, aggression_emergence |
| 9 | maxwells_demon | Maxwell's Demon (Landauer Bound) | 信息处理的能量代价（热力学约束） | entropy/work/efficiency 相关字段 |

---

## 任务一览（孤岛 10：Open-World 产品级评测基准）

孤岛10面向“产品级质量门禁 + 强证据链”：它测试的不是静态正确率，而是漂移（drift）出现时，系统能否检测变化并在预算约束下恢复，同时可审计代价与收益。

| Island | island_name | island_title | 核心作用（验证点） | 典型指标（artifacts 中） |
|---:|---|---|---|---|
| 10 | active_experimentation_innovation | Active Experimentation + Innovation [Open] | 漂移检测/恢复闭环 + 代价敏感主动探测 | detect_rate, delay_detected, recover_to_target, regret_to_target_total, action_cost_totals |

孤岛10同时覆盖 `numeric` 与 `engine` 两种环境后端；策略变体建议通过 `WMV2_ACTIVEEXP_PRESET` 命名化复现（例如 `dao_a0.20_drift_B4detH_tr0C`）。

### 十岛一键验证（聚合证据包）

仓库提供“十岛（1-10）”的一键聚合验证入口（会覆盖 strict 1-9 与 open 相关证据链）：
- 说明文档：[TEN_ISLANDS_VALIDATION_CN.md](TEN_ISLANDS_VALIDATION_CN.md)
- 运行入口：`python -m tools.wmv2_validate --suite all`

### 孤岛10强证据链入口（推荐）

当你需要对外或对内做“可审计、可对照、可回归”的产品级证据包时，推荐使用孤岛10强证据链工具（会生成统一 bundle 报告与 steps 目录）：

- 快速回归：`python -m tools.open_world_strong_evidence --quick`
- 全量对照：`python -m tools.open_world_strong_evidence --full`

### Open 变体：对外世界逼近（研究级，不影响验收）

当目标从“封闭世界可复现”升级为“对外世界尽可能逼近”时，建议为现有孤岛增加并行的 Open 变体验证层，专门覆盖：
- 部分可观测（信念态与主动观测）
- 非平稳/漂移（机制切换与快速适配）
- 反身性/对抗性（反馈回路与对手适应）
- 代价敏感（信息增益/成本）

说明文档： [OPEN_WORLD_ISLANDS_UPGRADE_CN.md](OPEN_WORLD_ISLANDS_UPGRADE_CN.md)

---

## 文档索引（对外引用建议）

- 孤岛10产品级说明：[ISLAND_10_ACTIVE_EXPERIMENTATION_CN.md](ISLAND_10_ACTIVE_EXPERIMENTATION_CN.md)
- 十岛聚合验证说明：[TEN_ISLANDS_VALIDATION_CN.md](TEN_ISLANDS_VALIDATION_CN.md)
- Open 变体升级说明：[OPEN_WORLD_ISLANDS_UPGRADE_CN.md](OPEN_WORLD_ISLANDS_UPGRADE_CN.md)
