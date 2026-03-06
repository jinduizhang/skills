---
name: skill-trimmer
description: 超长Skill裁剪优化。当Skill超过500行时，使用渐进式披露策略裁剪：提取核心指令到SKILL.md，详细内容移到references/，复杂逻辑封装到scripts/。
---

# 超长Skill裁剪指南

## 裁剪原则

### 核心法则：500行上限

| 当前行数 | 动作 |
|---------|------|
| <300行 | 保持，无需裁剪 |
| 300-500行 | 可选裁剪 |
| >500行 | **必须裁剪** |
| >800行 | 深度重构 |

---

## 裁剪步骤（四步法）

### Step 1: 分类内容

```
原始内容可能包含：
├── 上下文收集步骤      → 精简为"执行环境检查"
├── Mock策略分析       → 移到 references/mock-strategy.md
├── Mock框架选择       → 移到 references/frameworks.md
├── 样例输出           → 移到 assets/templates/
├── 详细规则           → 移到 references/rules.md
├── 执行流程（核心）   → 保留在 SKILL.md
└── 边界情况           → 移到 references/edge-cases.md
```

### Step 2: 提取核心指令（保留在SKILL.md）

```markdown
# UT生成 [HIGHEST_PRIORITY]

## 触发条件
当用户请求包含: "生成UT"、"写测试"

## 执行流程

1. 环境检查 → 执行 references/env-check.md
2. 策略分析 → 执行 references/mock-strategy.md
3. 生成测试 → 使用 assets/test-template.ts
4. 验证执行 → 运行测试命令

## 核心规则
- 必须先加载 references/mock-strategy.md
- 必须使用 assets/test-template.ts 作为模板
- 输出后必须运行测试验证
```

### Step 3: 迁移到references/

```
references/
├── env-check.md        # 环境检查步骤
├── mock-strategy.md   # Mock策略分析
├── frameworks.md      # Mock框架选择指南
└── edge-cases.md     # 边界情况处理
```

### Step 4: 迁移到assets/

```
assets/
├── test-template.ts   # 测试模板
├── mock-config.json   # Mock配置样例
└── output-example.md # 输出示例
```

---

## 裁剪检查清单

- [ ] SKILL.md 总行数 < 500
- [ ] 每个reference文件 < 300行
- [ ] 核心指令在SKILL.md前100行
- [ ] 只用 "Read xxx" 引用详细文档
- [ ] assets/ 只包含可直接使用的模板
- [ ] 没有重复的解释性文字

---

## 关键原则

### 1. SKILL.md是导航，不是百科全书

```markdown
# 错误：百科全书式
## Mock策略分析
Jest适合以下场景：
1. 单元测试...
2. 集成测试...

# 正确：导航式
## Mock策略分析
Read references/mock-strategy.md 选择合适的Mock策略。
```

### 2. 模板直接可用

```markdown
# 错误：文字描述
输出格式应该是清晰的...

# 正确：直接给模板
使用 assets/test-template.ts 作为模板生成测试。
```

### 3. 决策树用表格

```markdown
| 场景 | 框架 | 原因 |
|------|------|------|
| HTTP请求 | MSW | 拦截真实请求 |
| 简单函数 | jest.fn() | 轻量 |
```