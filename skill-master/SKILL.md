---
name: skill-master
description: Skill优化大师。自动分析并优化任意Skill，提升遵从度。支持三种模式：1)提升遵从度 2)通用优化 3)超长裁剪。自动识别问题并选择最优优化方案。
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
| Token太长 | 行数>500 | 裁剪模式 |
| 触发不准确 | description模糊/太短 | 优化触发条件 |
| 不按要求执行 | 缺少强制词 | 添加强制格式 |
| 多任务混合 | 包含多个功能 | 拆分子skill |
| 综合问题 | 多个问题并存 | 综合优化 |

### Step 3: 自动优化

根据诊断结果自动选择优化方案：

```
诊断结果 → 优化方案
├── 问题1: Token太长 → 使用裁剪模式
│   ├── 详细文档 → references/
│   ├── 模板 → assets/
│   └── SKILL.md → <500行
│
├── 问题2: 触发不准确 → 优化description
│   ├── 添加正向触发词
│   └── 添加负向触发词
│
├── 问题3: 不按要求执行 → 添加强制格式
│   ├── [HIGHEST_PRIORITY]
│   └── MUST 执行词
│
└── 问题4: 多任务混合 → 拆分skill
    ├── 1个路由skill
    └── N个子skill
```

---

## 三种优化模式

### 模式1: 提升遵从度 (compliance)

**触发**: "提升遵从度"、"让skill更听话"

**优化内容**:
- 优化description触发词
- 添加强制格式
- 明确执行边界

### 模式2: 通用优化 (optimize)

**触发**: "优化skill"、"精简skill"

**优化内容**:
- 删除冗余内容
- 添加触发条件
- 精简到核心指令

### 模式3: 超长裁剪 (trim)

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
- 问题1: [描述]
- 问题2: [描述]

## 优化内容
- [x] 精简Token
- [x] 优化触发条件
- [x] 添加强制格式

## 修改的文件
- SKILL.md (已优化)
- references/xxx.md (新增/移动)

## 验证结果
- [x] Token < 500
- [x] 有触发关键词
- [x] 有强制执行规则
```
