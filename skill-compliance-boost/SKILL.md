---
name: skill-compliance-boost
description: 提升Skill遵从度。当用户请求"优化skill"、"提升遵从度"、"精简skill"时使用。直接指定skill目录路径，AI会自动读取并优化。
metadata:
  author: skill-compliance-boost
  version: "1.0"
---

# Skill遵从度优化器

## 触发条件

当用户请求包含以下关键词时，加载此skill：
- "优化skill"、"提升遵从度"
- "精简skill"、"裁剪skill"
- "让skill更听话"

## 使用方法

### Step 1: 用户指定目录

用户直接给出要优化的skill目录路径，例如：
- "优化 ~/.config/opencode/skills/my-ut-skill/"
- "帮我优化 .opencode/skills/ut-generator/"

### Step 2: AI读取并分析

1. 读取目标目录的 SKILL.md
2. 分析问题：
   - 行数是否>500？
   - description是否模糊？
   - 是否缺少强制词？
   - 是否多任务混合？

### Step 3: 优化处理

按照以下步骤优化：

```
优化步骤：
1. 精简Token
   - 详细文档移到 references/
   - 模板移到 assets/
   - SKILL.md只保留<500行

2. 优化触发条件
   - 添加正向触发词（"生成UT"、"写测试"）
   - 添加负向触发词（禁止什么）

3. 添加强制格式
   - 加 [HIGHEST_PRIORITY]
   - 加 MUST 执行词

4. 拆分多任务
   - 1个路由skill + N个子skill
```

### Step 4: 输出结果

直接修改目标目录下的文件，或输出优化后的内容让用户确认。

---

## 优化检查清单

- [ ] SKILL.md < 500行
- [ ] description 包含触发关键词
- [ ] description 包含负向触发词（禁止什么）
- [ ] 有 [HIGHEST_PRIORITY] 强制节
- [ ] 有 MUST 执行词
- [ ] 单一任务，不混合

---

## 示例

**用户输入**：
```
优化这个skill目录：~/.config/opencode/skills/ut-generator/
```

**AI执行**：
1. 读取 ~/.config/opencode/skills/ut-generator/SKILL.md
2. 分析问题
3. 优化并写入
4. 输出完成报告