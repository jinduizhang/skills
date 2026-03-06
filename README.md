# Skill 优化工具箱

> 用于优化 OpenCode Skill，提升遵从度和执行精确度

---

## 安装

```bash
# 克隆到本地
git clone https://github.com/jinduizhang/skills.git ~/.config/opencode/skills/
```

或者复制以下文件夹到你的 OpenCode skills 目录：
- `~/.config/opencode/skills/skill-compliance-boost/`
- `~/.config/opencode/skills/skill-optimizer/`
- `~/.config/opencode/skills/skill-trimmer/`

---

## 三个 Skill 介绍

### 1. skill-compliance-boost ⭐ 主要用这个
**用途**：提升 Skill 遵从度，让 AI 更听话

**触发关键词**：
- "优化skill"、"提升遵从度"
- "精简skill"、"裁剪skill"
- "让skill更听话"

**解决问题**：
- Token太长，指令被稀释
- 触发不准确
- 不按要求执行

---

### 2. skill-optimizer
**用途**：通用 Skill 优化

**触发关键词**：
- "优化skill"、"精简skill"

**解决问题**：
- 删除非关键因素
- 添加触发条件
- 添加强制规则

---

### 3. skill-trimmer
**用途**：超长 Skill 裁剪

**触发关键词**：
- "裁剪skill"、"太长"

**解决问题**：
- SKILL.md > 500行
- 内容太详细导致稀释

---

## 使用方法

### Step 1: 加载 Skill

在 OpenCode 中输入：
```
skill({ name: "skill-compliance-boost" })
```

### Step 2: 发送你的 Skill

把你要优化的 Skill 内容发送给 AI。

### Step 3: AI 自动优化

AI 会按照以下步骤处理：

```
1. 诊断问题
   - 检查行数是否>500
   - 检查description是否模糊
   - 检查是否缺少强制词
   
2. 精简Token
   - 详细文档移到 references/
   - 模板移到 assets/
   - 只保留核心指令

3. 优化触发
   - 添加正向触发词
   - 添加负向触发词（禁止什么）

4. 添加强制格式
   - 加 [HIGHEST_PRIORITY]
   - 加 MUST 执行词

5. 拆分多任务
   - 1个路由 + N个子skill
```

---

## 优化前后对比

### ❌ 优化前（问题）
```yaml
---
name: ut-skill
description: UT相关技能
---

# UT技能
包含生成、修复、覆盖率提升...

（800行详细内容...）
```

### ✅ 优化后
```yaml
---
name: ut-operation
description: 单元测试操作技能。触发：生成UT、写测试。禁止：不要生成E2E测试。
---

# UT操作技能 [HIGHEST_PRIORITY]

## 触发路由
| 关键词 | 加载 |
|--------|------|
| 生成UT | ut-generate |
| 修复UT | ut-fix |
| 覆盖率 | ut-coverage |

## 执行规则 [HIGHEST_PRIORITY]
1. MUST 识别关键词
2. MUST 使用skill()加载子skill
3. 禁止 混用任务
```

---

## 验证检查清单

优化后检查：
- [ ] SKILL.md < 500行
- [ ] description 包含触发关键词
- [ ] description 包含负向触发词（禁止什么）
- [ ] 有 `[HIGHEST_PRIORITY]` 标记
- [ ] 有 `MUST` 执行词
- [ ] 单一任务，不混合

---

## 参考来源

- [mgechev/skills-best-practices](https://github.com/mgechev/skills-best-practices) - 官方最佳实践
- [OpenCode Skills 文档](https://open-code.ai/zh/docs/skills)
- [Agent Skills 规范](https://agentskills.io)
