# DDCP实验数据仓库

本仓库包含DPCC（Dual-Pathway Cognitive Control）算法的实验数据和验证结果。

## 仓库说明

**注意**: 为保护研究成果，本仓库仅包含实验数据和报告，不包含核心算法源代码。

## 实验数据

### 大规模实验 (2026-02-07)

- **样本数**: 1619个有效样本（清理后）
- **原始样本**: 1800个
- **有效率**: 89.9%
- **模型数**: 4个
- **重复次数**: 50次/模型

### 文件列表

```
large_scale_experiment_2026-02-07/
├── cleaned_results.json    # 清理后的实验数据 (JSON格式)
└── cleaned_results.csv     # 清理后的实验数据 (CSV格式)

FINAL_EXPERIMENT_REPORT.md  # 完整实验报告
analysis_for_paper.md       # 论文指标分析
```

## 核心结果

### 模型性能对比

| 模型 | 忠实度 | 连贯性 | 相关性 |
|------|--------|--------|--------|
| **qwen3:4b (DPCC)** | **57.60%** | 76.69% | **40.66%** |
| llama3.1:8b | 48.79% | 62.04% | 17.02% |
| qwen3-vl:4b | 34.46% | 79.26% | 29.94% |
| nemotron-3-nano | 22.87% | 70.60% | 9.18% |

### 统计显著性

- **模型间ANOVA**: F=144.93, p=3.68e-83 (高度显著)
- **DPCC vs 基线**: 忠实度改进 +62.8% (p<0.0001)

### 消融实验

- **DPCC-Full**: 100% 矛盾召回率
- **DPCC-Forward-Only**: 0% 矛盾召回率
- **统计显著性**: p<0.0001

## 使用说明

### 加载数据

```python
import json
import pandas as pd

# JSON格式
with open('large_scale_experiment_2026-02-07/cleaned_results.json', 'r') as f:
    data = json.load(f)

# CSV格式
df = pd.read_csv('large_scale_experiment_2026-02-07/cleaned_results.csv')
```

### 数据字段

| 字段 | 说明 |
|------|------|
| model_name | 模型名称 |
| experiment_group | 实验组 (A/B/C) |
| repetition | 重复次数 |
| scenario_id | 场景ID |
| scenario_type | 场景类型 |
| faithfulness_score | 忠实度分数 |
| coherence_score | 连贯性分数 |
| relevance_score | 相关性分数 |
| response_time_ms | 响应时间(ms) |
| memory_usage_mb | 内存使用(MB) |

## 引用

如果您使用了本数据，请引用：

```
DPCC: Dual-Pathway Cognitive Control for Contradictory Information Processing
[作者信息待补充]
```

## 许可

本数据仅供学术研究使用。

---

**生成时间**: 2026-02-07  
**实验完成时间**: 2026-02-07 14:08  
**数据清理时间**: 2026-02-07 14:42
