---
name: sdd-brownfield
description: 已有项目的规范驱动开发(SDD)。先进行项目分析（架构/功能/技术栈），再使用spec-kit开发新功能。适合在现有代码库中添加新功能。
metadata:
  author: sdd-brownfield
  version: "1.0"
---

# 已有项目SDD开发 [HIGHEST_PRIORITY]

## 触发条件

当用户请求包含以下关键词时，加载此skill：
- "在已有项目中开发"、"添加新功能"
- "项目分析"、"架构分析"
- "brownfield开发"、"现有代码库开发"
- "先分析再开发"

## 工作流程

### 阶段0: 项目分析

在开发新功能前，先分析现有项目。

#### 1. 架构分析

分析项目结构：
- 目录结构
- 模块划分
- 依赖关系
- 架构模式（MVC/微服务/分层等）

输出：`.specify/analysis/architecture.md`

#### 2. 功能分析

分析现有功能：
- 核心功能模块
- API端点
- 数据模型
- 业务逻辑流程

输出：`.specify/analysis/features.md`

#### 3. 技术栈分析

分析技术栈：
- 前端框架
- 后端框架
- 数据库
- 依赖管理
- 构建工具

输出：`.specify/analysis/tech-stack.md`

---

### 阶段1-5: SDD标准流程

完成分析后，使用spec-kit标准流程：

| 阶段 | 命令 | 产出 |
|------|------|------|
| 1. 确立原则 | /speckit.constitution | constitution.md |
| 2. 定义需求 | /speckit.specify | spec.md |
| 3. 技术方案 | /speckit.plan | plan.md |
| 4. 任务拆分 | /speckit.tasks | tasks.md |
| 5. 执行实现 | /speckit.implement | 代码 |

---

## 使用方法

### Step 1: 安装spec-kit（如果未安装）

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
specify init . --ai opencode --force
```

### Step 2: 项目分析

在OpenCode中执行：

```bash
# 架构分析
分析项目架构，包括目录结构、模块划分、依赖关系、架构模式。

# 功能分析
分析现有功能模块、API端点、数据模型、业务逻辑流程。

# 技术栈分析
分析前端框架、后端框架、数据库、依赖管理、构建工具。
```

分析结果保存到：
- `.specify/analysis/architecture.md`
- `.specify/analysis/features.md`
- `.specify/analysis/tech-stack.md`

### Step 3: 确立项目原则

```bash
/speckit.constitution 基于项目分析结果，创建开发原则，保持与现有代码风格一致。
```

### Step 4: 定义新功能需求

```bash
/speckit.specify 描述新功能需求，说明"做什么"和"为什么"，参考现有架构和功能。
```

示例：
```
在用户管理模块中添加批量导入功能。保持现有RESTful API风格，使用已有的验证机制。
```

### Step 5: 技术方案

```bash
/speckit.plan 使用项目现有技术栈，设计新功能的技术实现方案。
```

### Step 6: 任务拆分

```bash
/speckit.tasks
```

### Step 7: 执行实现

```bash
/speckit.implement
```

---

## 项目结构

```
现有项目/
├── .specify/
│   ├── analysis/
│   │   ├── architecture.md   # 架构分析
│   │   ├── features.md        # 功能分析
│   │   └── tech-stack.md      # 技术栈分析
│   ├── memory/
│   │   └── constitution.md    # 项目原则
│   ├── specs/
│   │   └── 001-新功能/
│   │       ├── spec.md
│   │       ├── plan.md
│   │       └── tasks.md
│   └── templates/
├── src/                      # 现有源代码
└── tests/                    # 现有测试
```

---

## 核心规则 [HIGHEST_PRIORITY]

1. MUST 先完成项目分析，再开发新功能
2. MUST 保持与现有代码风格一致
3. MUST 使用项目现有的技术栈和模式
4. MUST 遵循现有架构的模块划分
5. MUST 保持与现有API的一致性
6. 禁止引入不必要的新技术栈
7. 禁止破坏现有功能

---

## 分析检查清单

- [ ] 目录结构清晰
- [ ] 模块划分明确
- [ ] 依赖关系文档化
- [ ] 核心功能模块已识别
- [ ] API端点已梳理
- [ ] 数据模型已理解
- [ ] 技术栈已确认
- [ ] 开发原则已建立

---

## 参考

- 官方文档: https://github.com/github/spec-kit
- Stars: 74K+
- Brownfield案例: https://github.com/mnriem/spec-kit-aspnet-brownfield-demo