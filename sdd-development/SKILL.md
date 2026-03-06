---
name: sdd-development
description: 规范驱动开发(SDD) Skill。基于github/spec-kit (74K stars)官方工作流。包含：需求定义(constitution)、功能规范(specify)、技术方案(plan)、任务拆分(tasks)、执行实现(implement)。
metadata:
  author: sdd-development
  version: "1.0"
---

# 规范驱动开发 (SDD)

## 触发条件

当用户请求包含以下关键词时，加载此skill：
- "SDD开发"、"规范驱动开发"
- "需求开发"、"需求文档"
- "用spec-kit"、"specify命令"
- "先写规范再写代码"

## SDD核心工作流

SDD (Spec-Driven Development) 是微软官方推出的规范驱动开发方法论，核心是：**先定义规范，再生成代码**。

### 五大阶段

| 阶段 | 命令 | 产出 |
|------|------|------|
| 1. 确立原则 | /speckit.constitution | constitution.md |
| 2. 定义需求 | /speckit.specify | spec.md |
| 3. 技术方案 | /speckit.plan | plan.md |
| 4. 任务拆分 | /speckit.tasks | tasks.md |
| 5. 执行实现 | /speckit.implement | 代码 |

---

## 使用方法

### Step 1: 安装spec-kit

```bash
# 安装Specify CLI
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# 初始化项目
specify init my-project --ai opencode

# 检查工具
specify check
```

### Step 2: 确立项目原则

```bash
/speckit.constitution 创建项目开发原则，包括代码质量、测试标准、用户体验一致性、性能要求
```

### Step 3: 定义功能需求

```bash
/speckit.specify 描述你要开发的功能，聚焦"做什么"和"为什么"，不要关注技术栈
```

示例需求：
```
开发一个照片管理应用。照片按日期分组到相册，相册可以拖拽重新排列。相册不能嵌套。照片以瓦片界面预览。
```

### Step 4: 技术方案

```bash
/speckit.plan 使用Vite + 原生HTML/CSS/JS。图片存储在本地，元数据存储在SQLite。
```

### Step 5: 任务拆分

```bash
/speckit.tasks
```

### Step 6: 执行实现

```bash
/speckit.implement
```

---

## 可用命令

### 核心命令

| 命令 | 作用 |
|------|------|
| /speckit.constitution | 创建项目原则和开发指南 |
| /speckit.specify | 定义功能和需求 |
| /speckit.plan | 创建技术实现方案 |
| /speckit.tasks | 生成可执行任务清单 |
| /speckit.implement | 执行所有任务 |

### 辅助命令

| 命令 | 作用 |
|------|------|
| /speckit.clarify | 澄清不明确的需求 |
| /speckit.analyze | 跨产物一致性分析 |
| /speckit.checklist | 生成质量检查清单 |

---

## 项目结构

```
项目目录/
├── .specify/
│   ├── memory/
│   │   └── constitution.md    # 项目原则
│   ├── scripts/               # 脚本
│   ├── specs/
│   │   └── 001-功能名/
│   │       ├── spec.md        # 功能规范
│   │       ├── plan.md        # 技术方案
│   │       └── tasks.md       # 任务清单
│   └── templates/
├── src/                      # 源代码
└── tests/                    # 测试
```

---

## 关键原则

1. **规范先于代码**: 先写spec，再写code
2. **明确"什么"而非"如何"**: 描述需求，不指定技术实现
3. **多阶段收敛**: 分步细化，而非一次性大prompt
4. **人机协同**: AI执行，人类验证

---

## 参考

- 官方仓库: https://github.com/github/spec-kit
- Stars: 74K+
- 支持: OpenCode, Claude Code, Cursor, Codex等
