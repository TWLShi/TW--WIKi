# 05_调派规则模型

**最后更新**：2026-04-23

## 1. 规则类型
- LEVEL（等级调派）
- PLAN（预案调派）
- ALGO（算法调派）

## 2. N_total 公式在规则中的映射
$$
N_{\text{total}} = N_{\text{base}} + \alpha_{\text{sub}} + \beta_{\text{struct}} + G_{\text{special}} + M_{\text{support}}
$$

（详细见 [[调派规模计算模型]]）

**配置示例**（JSON conditions）：
```json
{"building_height": ">50", "hazard": true}
```