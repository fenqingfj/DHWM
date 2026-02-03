# 离形全息宇宙型世界大模型（DHWM）系统设计与作用（对外说明）

本文件用于对外解释：这是一个什么系统、它有哪些“智能体现”、以及“十大孤岛验证”在系统里扮演什么角色。

---

## 一句话

DHWM 是一个以“可审计世界状态（图+上下文）”为底座、以“离形全息切片（Holographic Slice）”为通信协议、以“管线算子（Pipeline Ops）”为可插拔推理与控制框架的世界模型系统：它不仅生成解释，还能在约束与代价下做主动探测、因果干预与自适应恢复，并通过标准化证据包进行回归与门禁。

---

## 核心设计原则（为什么叫“离形全息宇宙型”）

### 1) 离形（Decoupled / Forma-free）

系统的“智能”不绑定某一种固定神经网络形态或单一模型：世界状态、推理过程、对外接口与验证证据是独立模块，可替换、可升级、可回滚。

### 2) 全息（Holographic）

系统以“切片”作为最小共享单元：每个智能体/子智能体/远端世界引擎只需要共享足够表达世界的一部分（slice），即可做合并、稳定与再推理，而不需要共享全量内部实现。

核心数据结构：
- [HolographicSlice](file:///d:/AI/WordModule/world_model_v2/agents/base.py)

### 3) 宇宙（Universe / World）

系统维护一个“客观世界容器”与“主观认知容器”的协同：
- 客观世界：可持久化、可演化、可合并的世界引擎
- 主观认知：智能体在世界中感知、推理、反思、导出方案的过程

核心引擎：
- [WorldEngine](file:///d:/AI/WordModule/world_model_v2/core/engine.py)
- 世界上下文容器 [WorldContext](file:///d:/AI/WordModule/world_model_v2/state/context.py)
- 持久化后端 [SQLiteGraphBackend](file:///d:/AI/WordModule/world_model_v2/state/sqlite_backend.py)

---

## 系统架构（组件与职责）

### Agent（主观智能体）

Agent 是“把世界状态变成行动”的执行主体，提供统一生命周期接口：
- `wake → perceive → think → reflect → commit/sync`

核心实现：
- [HolographicAgent](file:///d:/AI/WordModule/world_model_v2/agents/holographic.py)
- [MainChainAgent](file:///d:/AI/WordModule/world_model_v2/agents/main_chain.py)
- [SubAgentEntity](file:///d:/AI/WordModule/world_model_v2/agents/subagent_entity.py)

策略人格（Persona）是“可替换的认知/偏好/决策风格”：
- [IPersona](file:///d:/AI/WordModule/world_model_v2/agents/personas/base.py)
- [personas/impl.py](file:///d:/AI/WordModule/world_model_v2/agents/personas/impl.py)

### Engine（客观世界引擎）

WorldEngine 是“客观世界容器”，对外可解释为三层职责：
- 世界状态：节点/边/属性（结构化可审计）
- 世界演化：物理/规则系统推进（可回放）
- 世界融合：从 slice/外部源合并知识与结构（可同步）

### Memory（世界记忆与可审计持久化）

系统的“记忆”不是单一文本，而是图结构 + 可检索上下文 + 持久化日志：
- 图状态容器：WorldContext
- 图持久化：SQLiteGraphBackend（节点状态、边、KV、事件/episode 日志）

这让系统具备“可追溯性”：第三方可以仅凭 artifacts/DB 复算指标与推导关键结论。

### Pipeline（可插拔推理与控制算子）

Pipeline 是“把能力模块化”的关键：用 spec 驱动执行，让系统能力可组合、可替换、可对照。

核心执行器：
- [PipelineExecutor](file:///d:/AI/WordModule/world_model_v2/pipeline/executor.py)

代表性算子（部分）：
- 预测/传播/投票/反事实/类比/生成子体/导出等：见 [pipeline/ops](file:///d:/AI/WordModule/world_model_v2/pipeline/ops/)

### Connector & Server（对外接口）

系统支持本地与远端世界：
- 服务端提供世界同步与流式更新（WS/REST）：[server.py](file:///d:/AI/WordModule/world_model_v2/server.py)
- 客户端连接器负责下行订阅与上行同步： [RemoteConnector](file:///d:/AI/WordModule/world_model_v2/client/connector.py)

这使得“智能体”和“世界引擎”可以部署分离，形成产品级形态（服务化世界 + 多智能体协作）。

---

## 多世界（Multi-World）与多智能体（Multi-Agent）

DHWM 的“多世界”不是简单的“多个测试环境”，而是一套可调度、可分工、可逐步掌握的世界族：系统用统一的世界表征与证据包协议，在不同世界之间迁移结构与经验，并通过自治子体持续扩张覆盖率。

### 多世界掌握度（Mastery）

系统对外提供“九世界掌握度”指标：用覆盖率、平均世界分数、宏观/微观晶体比例等维度衡量在不同世界族上的稳定能力，而不是只看单次演示。

相关说明与接口列表：
- [AUTONOMY_AND_MULTI_WORLD_GUIDE_CN.md](file:///d:/AI/WordModule/docs/AUTONOMY_AND_MULTI_WORLD_GUIDE_CN.md)

### 调度与分工（Director + Habit）

主脑提供调度建议（补短板但不偏科），子脑把建议固化成“习惯权重”，从而实现“多世界的持续均衡训练/探索”，避免系统只在少数世界上过拟合。

### 子体自治探索（SubAgent Autonomy）

当掌握度达到门槛，子体进入自治探索阶段：
- 从本地语料或受控来源提取信息（可溯源）
- 写入自身世界引擎并演化
- 导出 proposal（结构化变更建议）
- 提交主脑并由门禁/策略决定是否合并

对外可用一句话描述：
- “多世界不是人工枚举，而是通过自治子体持续扩张覆盖面，同时保持可审计、可回滚的合并机制。”

## 典型数据流（从智能到可验证）

下面是一条“产品级闭环”的抽象流程：

1. 感知：Agent 接收世界更新（本地引擎或远端同步），形成/更新 WorldContext
2. 推理：Pipeline 组合算子（预测、传播、类比、反事实等）生成候选解释与行动
3. 决策：Persona/策略选择行动，并写入可审计事件
4. 执行：WorldEngine（或远端世界）执行行动，返回新观测与代价
5. 复盘：反思与总结写回世界记忆（结构化存储），形成可审计证据
6. 门禁：验证套件在固定 seeds/压力轴上回归，输出通过/失败与差异定位

入口示例（用于理解系统“如何跑起来”）：
- 训练入口：[train.py](file:///d:/AI/WordModule/world_model_v2/train.py)
- Pipeline 入口：[runner.py](file:///d:/AI/WordModule/world_model_v2/runner.py)

---

## “十大孤岛验证”为什么不是摆设（它的系统作用）

十大孤岛不是“为了好看”的 demo，而是系统的三种产品级能力：

### 1) 可审计（Auditability）

每个孤岛都输出结构化 artifacts（summary/per-episode/events 等），使第三方可以复算关键指标，并定位退化来自哪一类机制。

### 2) 可回归（Regression）

孤岛为系统提供跨版本、跨策略的稳定回归基线：你可以高频迭代主系统，而不担心“看起来更聪明但暗处退化”。

### 3) 可门禁（Gate）

孤岛可以成为产品发布与策略切换的门禁：不达标则阻断发布/回滚/切换到更稳策略（例如通过 preset）。

其中，孤岛 1-9 主要覆盖“无训练可复现”的严格验收；孤岛 10 主要覆盖“漂移 + 代价 + 主动探测 + 恢复”的产品级闭环能力（Open-World）。

索引入口：
- [ISLANDS_INDEX.md](file:///d:/AI/WordModule/docs/ISLANDS_INDEX.md)
- 孤岛10说明：[ISLAND_10_ACTIVE_EXPERIMENTATION_CN.md](file:///d:/AI/WordModule/docs/ISLAND_10_ACTIVE_EXPERIMENTATION_CN.md)

---

## 对外沟通建议（避免被误解成“只是实验”）

对外建议用两句话解释定位：

1) “我们不是把大模型当成黑盒聊天，而是把智能落实为：在可审计世界里做推理、做干预、承担代价，并能在漂移中恢复。”  
2) “十大孤岛是这套系统的质量门禁与强证据链：每次升级都必须在固定 seeds/压力轴上可复现地变好或至少不退化。”

---

## 泛化与退化：怎么解释，怎么验证

对外沟通时，最容易被误解的是把“验证指标”当成“系统默认能力”。这里必须先把概念拆开：**泛化是系统能力**，**验证是度量与门禁**，两者不是同一个东西。

### 1) 能力泛化（Capability Generalization）

含义：系统在不同任务/不同压力轴/不同实现后端下，仍能保持稳定优势与闭环表现。

对应验证功能（用于证明，不等于能力本体）：
- 十大孤岛（1-9 strict）：验证跨任务族的稳定可复现性（无训练条件）
- 孤岛10 open-world：验证漂移/预算/主动探测/恢复闭环在 OOD 轴上的稳定性（含 numeric/engine 双后端）
- paired bootstrap CI：验证优势不是单次运气，而是统计稳定差异

### 2) 全息泛化（Holography Generalization / Proxy）

含义：系统能在“信息不完整/局部可观测”的情况下，从切片中恢复关键结构并继续推理，且这种能力能跨规模/跨形态保持稳定。

注意：当前我们用的是 **proxy**（近似全息），它是验证工具，不代表系统已经达到理论上的“真全息”。

对应验证功能：
- 全息性 proxy 基准：边界/局部切片 → 重建结构一致性 + 压缩比 + 耗时

### 3) 性能泛化（Performance Generalization / Regression）

含义：系统在不同输入规模、不同管线组合下，吞吐/延迟保持稳定，不因版本迭代出现不可解释退化。

对应验证功能：
- WorldEngine ingest/evolve/save 回归基准（吞吐/耗时）
- Pipeline 推理分解基准（perceive/think/reflect 等算子耗时分位数）

### 4) 表达泛化（Expression Generalization）

含义：系统在不同任务形态（开放问答/解释、创意文案、多轮对话回应）下，能稳定输出结构化、可引用证据的自然语言表达；并且表达不会脱离世界内核的证据与约束。

对应验证功能（表达层门禁，不等于世界内核能力本体）：
- 表达层基准：要求输出 JSON（answer/citations/checks），包含指定事实与引用，避免禁用语与无依据发挥  
  `python -m tools.wmv2_expression_benchmark --backend auto --mode grounded`


进一步补强（端到端 grounded）：表达层不再引用“自造 evidence”，而是必须引用强证据链 bundle 中的真实 artifacts（例如全息网格/噪声曲线的 report.json）。  
`python -m tools.wmv2_expression_artifacts_benchmark --backend auto --bundle_dir <open_world_strong_evidence_run_dir>`

---

## 如何扩展“全息性”与“速度”验证，并与 LLM 基准对齐

对外讨论系统是否“退化”，需要两类证据：能力泛化证据（能不能在不同条件下仍然做对）与性能回归证据（做得多快/多省，是否变差）。本仓库建议用“三件套”建立可回归的对比面板。

### 1) 全息性（Holography Proxy）

“真全息”很难一次性证明，但可以用可复现的 proxy 指标衡量：在只给出边界/局部切片时，系统能否稳定重建关键结构与可审计属性。

推荐入口（会输出 report.json/report.md 到 tests/artifacts）：

```bash
python -m tools.wmv2_holography_benchmark
```

它目前提供的 proxy 是：从网格边界切片重建内部网格（边界信息 → interior 结构），并输出压缩比、重建一致性与耗时。

为了避免“只证明重建流程跑通”，该基准还会输出 `hash_ok`：对比重建前后世界的节点状态哈希与链接哈希是否一致，用于作为“切片条件下的推理/重建正确性”代理指标。

进一步扩展（对应“更大规模/不规则结构/动态系统/噪声鲁棒性”）：
- 更大规模网格：在 `--cases` 里加入 `64x64,96x96,128x128`，观察压缩比与耗时曲线
- 不规则结构（关系推理 proxy）：使用共振图关系推断基准（只给部分节点切片，推断节点对之间是否共振）  
  `python -m tools.wmv2_holography_resonance_benchmark --n_nodes 200 --observe_k 80 --threshold 0.80`
- 噪声鲁棒性：对切片的 payload 位注入随机翻转/丢点，观察 F1 曲线（precision/recall）  
  `python -m tools.wmv2_holography_resonance_benchmark --noise_flip_bits 24 --noise_dropout_prob 0.1`
- 噪声曲线（对外展示推荐）：对 flip_bits×dropout 的网格做 sweep，输出可直接引用的表格（mean/p50/p95）  
  `python -m tools.wmv2_holography_resonance_noise_sweep --seed_count 5 --noise_flip_bits 0,8,16,24,32 --noise_dropout_prob 0,0.1,0.2,0.3`
- 动态系统：让世界随时间漂移，同时叠加噪声/丢点，观察不同 t 的 F1（时变边界条件）  
  `python -m tools.wmv2_holography_resonance_benchmark --drift_steps 5 --drift_flip_bits 6 --noise_flip_bits 12`

### 2) 训练/推理速度（Regression-Oriented Perf）

速度验证的目标不是“追求绝对数值”，而是监控回归：同一台机器、同一配置下，吞吐/延迟是否变差。

推荐入口：

```bash
python -m tools.wmv2_perf_benchmark --repeats 3
```

输出包含 ingest 吞吐（bytes/s）、evolve 吞吐（steps/s）与总耗时。可用 `--compare <旧report.json>` 自动给出 delta，用于“退化讨论”。

如果你需要更贴近“主系统推理”的速度分解（按 Pipeline 算子统计 perceive/think/reflect 等步骤耗时），推荐使用：

```bash
python -m tools.wmv2_pipeline_perf_benchmark --repeats 5 --warmup 1
```

它会输出总耗时以及每个 operator 的 mean/p50/p95，用于定位退化发生在哪个推理环节。

### 3) 与 LLM 的对齐方式（能力分数 + 延迟参考）

能力对齐：使用已有的全球基准（六大孤岛）让任何 LLM/系统在同一随机用例上交付结构化数值指标，从而得到可公开比较的 score：

```bash
python -m benchmark.runner --adapter world_model_v2 --seed 12345 --cases-per-island 10
python -m benchmark.runner --adapter openai_compat --seed 12345 --cases-per-island 10
python -m benchmark.runner --adapter deepseek_compat --seed 12345 --cases-per-island 10
```

延迟参考：用统一 prompt 做 LLM 往返延迟测量（不是可比的“推理速度”，但可以作为产品交互延迟参考线）：

```bash
python -m tools.llm_latency_benchmark --provider deepseek --n 5
python -m tools.llm_latency_benchmark --provider openai_compat --n 5 --openai_model $env:OPENAI_MODEL
```

建议的对外话术是：
- “能力用可审计基准评分对齐，速度用可回归吞吐/延迟监控对齐；两者共同决定产品级退化与否。”
