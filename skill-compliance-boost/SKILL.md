---
name: skill-compliance-boost
description: 提升Skill遵从度。当用户请求"优化skill"、"提升遵从度"、"精简skill"、"裁剪skill"时使用。此skill可将长skill优化为高遵从度版本。
metadata:
  author: skill-compliance-boost
  version: "1.0"
---

# Skill遵从度优化器

## 触发条件

当用户请求包含以下关键词时，加载此skill：
- "优化skill"、"提升遵从度"
- "精简skill"、"裁剪skill"  
- "让skill更听话"、"skill不执行"

## 核心原则 [HIGHEST_PRIORITY]

### 问题诊断

| 问题 | 解决方案 |
|------|----------|
| Token太长 | 拆分到references/，SKILL.md<500行 |
| 触发不准确 | description加正负触发词 |
| 不按要求执行 | 添加强制格式[HIGHEST_PRIORITY]+MUST |
| 指令被稀释 | 拆分skill，保持单任务 |

### 优化公式

```
问题skill + 优化方法 = 高遵从度skill

问题: 800行融合skill，token太长，不执行
方案: 拆分为 1个路由skill + N个专业skill
```

---

## 优化步骤

### Step 1: 诊断问题

分析原skill的问题：
1. 行数是否>500？
2. description是否模糊？
3. 是否缺少强制词？
4. 是否多任务混合？

### Step 2: 精简Token

**来源**: [mgechev/skills-best-practices](https://github.com/mgechev/skills-best-practices)

```
原始内容 → 分类处理
├── 执行流程 → 精简为"Read xxx"
├── 详细文档 → 移到references/
├── 模板 → 移到assets/
└── 规则 → 只保留5-10条核心
```

### Step 3: 优化触发条件

**Bad:**
```yaml
description: "UT生成skill"
```

**Good:**
```yaml
单元测试。触发description: "生成：生成UT、写测试。禁止：不要生成E2E测试。"
```

### Step 4: 添加强制格式

```markdown
## 执行规则 [HIGHEST_PRIORITY]

你 MUST：
1. 当请求包含"[关键词]"时，执行[动作]
2. 禁止[具体行为]
3. 如果[条件]，则[动作]
```

### Step 5: 拆分skill

**问题**: 3个功能融合
**方案**: 1个路由 + 3个子skill

```
ut-operation/           # 路由skill
├── SKILL.md           # 识别关键词，加载子skill
├── ut-generate/       # 子skill1
├── ut-fix/           # 子skill2
└── ut-coverage/      # 子skill3
```

---

## 验证检查清单

- [ ] SKILL.md < 500行
- [ ] description包含触发关键词
- [ ] description包含负向触发词（禁止什么）
- [ ] 有[HIGHEST_PRIORITY]强制节
- [ ] 有MUST执行词
- [ ] 单一任务，不混合

---

## 输出格式

```markdown
# 优化报告

## 原问题
[描述问题]

## 优化内容
- 删除: [删除内容]
- 保留: [保留核心]
- 新增: [新增规则]
- 拆分: [拆分的skill结构]

## 验证结果
- [x] Token < 500
- [x] 有触发关键词
- [x] 有强制执行规则
- [x] 单一任务
```

---

## 参考资源

- 官方最佳实践: [mgechev/skills-best-practices](https://github.com/mgechev/skills-best-practices)
- OpenCode文档: [open-code.ai/zh/docs/skills](https://open-code.ai/zh/docs/skills)
- Agent Skills规范: [agentskills.io](https://agentskills.io)
