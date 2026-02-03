# 研究级证据链：OOD + 对照 + 统计（抬高“开放真实世界强者”的口径）

本说明给出一套可复核的“研究级证据链”跑法，目标是把结论从“阈值 PASS”升级为：
- 在分布切换（OOD）与更困难条件下仍稳健
- 相对强基线存在统计显著优势（均值/CI/效应量）
- 关键机制可被消融定位（不是靠单一技巧或固定参数）

---

## 1) 一键生成研究级证据包（推荐）

```bash
python -m tools.open_world_strong_evidence --quick
```

完整模式（更慢，适合对外背书/论文式证据）：

```bash
python -m tools.open_world_strong_evidence
```

输出目录：`tests/artifacts/open_world_strong_evidence_*/`
- `report.md`：总览与复核入口
- `manifest.json`：证据链（sha256）与 meta
- `steps/*`：各子实验的原始产物与报告

---

## 2) 证据包包含哪些子实验？

该一键脚本会自动运行并归档：
- `wmv2_validate --suite all`：十岛聚合验证（回归 + 阈值自检 + 证据索引）
- `island10_sweep`：多 seed 对照（active vs greedy/random）+ CI 报告
- `island10_open_policy_matrix`：Open-world 条件下多 posterior 组合对比（统计聚合）
- `island10_open_posterior_ablation`：Open-world posterior 消融点位（gate + repeats）
- `island10_open_env_compare`：Open-world OOD（numeric vs engine）对比

---

## 3) 如何阅读“强/不强”

建议按顺序复核：
1) `steps/validate_all/*/thresholds_spec_validation.md`：先确认阈值规范没缺岛、没缺参、没漏用  
2) `steps/validate_all/*/evidence_index.md`：确认基线回归整体 PASS  
3) `steps/island10_sweep_*/meta_report.md`：看相对 baseline 的提升是否稳定、CI 是否不跨 0  
4) `steps/open_env_compare/*/report.md`：看 OOD（engine 环境）是否仍稳健  
5) `steps/open_posterior_ablation/*/report.md`：看消融后哪些能力明显退化（定位机制贡献）

---

## 4) 常见升级方向（更“硬”）

- 扩大 seeds 与 repeats：CI 变窄，显著性更强
- 增加 OOD 维度：更强漂移、更低预算、更长 horizon、更强对抗
- 增加对照基线：引入更强的 oracle/控制器作为上界（标注为上界，不作为公平对照）

