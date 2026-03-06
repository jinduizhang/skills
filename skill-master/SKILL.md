---
name: skill-master
description: Skill优化大师。自动分析并优化任意Skill，提升遵从度。整合三个优化子技能：skill-compliance-boost（提升遵从度）、skill-optimizer（通用优化）、skill-trimmer（超长裁剪）。自动识别问题并选择最优优化方案。
metadata:
  author: skill-master
  version: "1.0"
---

# Skill优化大师

## 触发条件

当用户请求包含以下关键词时，加载此skill：
- "优化skill"、"提升遵从度"
- "精简skill"、"裁剪skill"
- "让skill更听话"
- "优化这个skill目录"
- 指定了skill目录路径

---

## 使用方法

### 用户输入示例

```
优化这个skill：~/.config/opencode/skills/my-ut-skill/
```

或

```
我的skill太长了，帮我裁剪一下：./.opencode/skills/coverage-skill/
```

或

```
这个skill不听话，提升一下遵从度
```

---

## 自动分析流程

### Step 1: 定位目标Skill

1. 如果用户提供了目录路径，直接使用
2. 如果用户只给了关键词，搜索匹配的skill目录
3. 读取目标 SKILL.md 内容

### Step 2: 诊断问题

分析目标skill的问题：

| 问题 | 检测方法 | 解决方案 |
|------|----------|----------|
| Token太长 | 行数>500 | 加载 skill-trimmer |
| 触发不准确 | description模糊/太短 | 加载 skill-optimizer |
| 不按要求执行 | 缺少强制词 | 加载 skill-compliance-boost |
| 多任务混合 | 包含多个功能 | 加载 skill-compliance-boost |
| 综合问题 | 多个问题并存 | 按顺序加载多个子skill |

### Step 3: 自动选择子技能

根据诊断结果自动选择：

```
诊断结果 → 加载对应子skill
├── Token太长 (>500行) → skill-trimmer
│   ├── 详细文档 → references/
│   ├── 模板 → assets/
│   └── SKILL.md → <500行
│
├── 需要优化触发条件 → skill-optimizer
│   ├── 添加正向触发词
│   └── 添加负向触发词
│
├── 需要提升遵从度 → skill-compliance-boost
│   ├── 添加强制格式
│   └── 明确执行边界
│
└── 综合问题 → 按顺序执行
    ├── skill-trimmer (先裁剪)
    ├── skill-optimizer (再优化)
    └── skill-compliance-boost (最后提升遵从度)
```

---

## 子技能说明

### skill-compliance-boost
**用途**: 提升Skill遵从度

**触发**: "提升遵从度"、"让skill更听话"

**优化内容**:
- 优化description触发词
- 添加强制格式 [HIGHEST_PRIORITY]
- 明确执行边界

### skill-optimizer
**用途**: 通用Skill优化

**触发**: "优化skill"、"精简skill"

**优化内容**:
- 删除冗余内容
- 添加触发条件
- 精简到核心指令

### skill-trimmer
**用途**: 超长Skill裁剪

**触发**: "裁剪skill"、"太长"

**优化内容**:
- 拆分到references/
- 拆分到assets/
- SKILL.md <500行

---

## 优化检查清单

优化完成后验证：

- [ ] SKILL.md < 500行
- [ ] description 包含触发关键词
- [ ] description 包含负向触发词（禁止什么）
- [ ] 有 [HIGHEST_PRIORITY] 强制节
- [ ] 有 MUST 执行词
- [ ] 单一任务，不混合

---

## 输出报告

```markdown
# 优化完成

## 诊断结果
- 问题1: [描述] → 加载 [子技能]
- 问题2: [描述] → 加载 [子技能]

## 执行的子技能
- [x] skill-trimmer (裁剪)
- [x] skill-optimizer (优化)
- [x] skill-compliance-boost (提升遵从度)

## 修改的文件
- SKILL.md (已优化)
- references/xxx.md (新增/移动)

## 验证结果
- [x] Token < 500
- [x] 有触发关键词
- [x] 有强制执行规则
```
