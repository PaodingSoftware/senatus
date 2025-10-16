# Senatus Framework

![Senatus Framework](senatus.png)

**Senatus** 是一个规范驱动开发框架，专为软件开发中的需求分析、讨论、研究和实施提供完整的工作流程。该框架通过系统化的命令和模板，帮助开发者从初始想法到最终实现进行有序的项目管理。

支持的 AI 编程助手：
- Claude Code
- GitHub Copilot

## 核心理念

Senatus 遵循古罗马议会的决策模式，其核心在于**讨论和记录**，通过结构化的对话和文档化过程解决AI开发中的关键难题：

### 解决的核心问题

1. **需求表述不足**：用户向AI表述需求时往往缺乏细节，导致AI需要猜测用户意图
   - 通过结构化讨论引导用户澄清需求细节
   - 基于项目研究提供精确的技术背景
   - 多轮对话逐步完善需求理解

2. **上下文容量限制**：复杂需求超出AI上下文容量，导致重要信息丢失
   - 将复杂需求分解为独立的讨论主题
   - 系统化记录每个决策和实施过程
   - 通过文档持久化保存所有关键信息

### 设计原则

- **规范驱动**：通过项目宪法确保所有操作符合既定标准
- **渐进式澄清**：从粗粒度需求到精细化实施方案
- **结构化记录**：标准化的文档格式确保信息完整性
- **可追溯性**：完整保留从想法到实现的全过程
- **上下文延续**：通过文档系统突破单次对话的容量限制

## 项目结构

```
senatus/
├── .claude/
│   └── commands/           # 自定义命令定义
│       ├── senatus.implement.md    # 执行任务项（批量）
│       ├── senatus.collect.md      # 收集手动变更
│       ├── senatus.constitution.md # 创建项目宪法
│       ├── senatus.context.md      # 了解项目背景
│       ├── senatus.correct.md      # 修复问题
│       ├── senatus.discuss.md      # 主题讨论
│       ├── senatus.inspire.md      # 启发式讨论
│       ├── senatus.new-topic.md    # 创建新讨论主题
│       ├── senatus.plan.md         # 生成任务计划
│       └── senatus.research.md     # 项目源码研究
├── .github/
│   └── prompts/            # GitHub Copilot 提示词
│       ├── senatus.implement.prompt.md
│       ├── senatus.collect.prompt.md
│       ├── senatus.constitution.prompt.md
│       ├── senatus.context.prompt.md
│       ├── senatus.correct.prompt.md
│       ├── senatus.discuss.prompt.md
│       ├── senatus.inspire.prompt.md
│       ├── senatus.new-topic.prompt.md
│       ├── senatus.plan.prompt.md
│       └── senatus.research.prompt.md
├── .specify/               # 文档模板
│   ├── discuss-template.md      # 讨论文档模板
│   ├── research-template.md     # 研究报告模板
│   ├── plan-template.md         # 任务计划模板
│   ├── implementation-template.md # 实施记录模板
│   └── constitution-template.md # 项目宪法模板
└── specify/                # 工作目录（使用时生成）
    ├── constitution.md     # 项目约束宪法
    └── [编号]-[主题名]/    # 主题工作目录
        ├── discuss.md      # 讨论记录
        ├── research.md     # 研究报告
        ├── plan.md         # 任务计划
        └── implementation/ # 实施记录目录
            └── [任务编号].md
```

## 安装与配置

### 前置条件
- 安装 AI 编程助手（[Claude Code](https://claude.com/claude-code) 或 [GitHub Copilot](https://github.com/features/copilot)）
- 确保项目根目录包含 `.claude` 和/或 `.github` 文件夹

### 使用方式
1. 将 Senatus 框架文件复制到你的项目根目录
2. 在支持的 AI 编程助手中打开你的项目
3. 框架将自动加载所有自定义命令

## 完整工作流程

### 1. 建立项目约束 (`/senatus.constitution`)
```bash
/senatus.constitution
```
- 分析项目结构和技术栈
- 生成项目宪法文件 `specify/constitution.md`
- 定义技术约束、质量约束、安全约束、业务约束
- 后续所有操作都必须遵循这些约束

### 2. 创建讨论主题 (`/senatus.new-topic`)
```bash
/senatus.new-topic 实现用户认证功能
```
- 创建新的主题目录（如 `specify/001-implement-user-auth/`）
- 生成初始讨论文档 `discuss.md`
- 为主题分配唯一序号

### 3. 项目研究 (`/senatus.research`)
```bash
/senatus.research
```
- 分析与当前主题相关的项目源码
- 生成详细的研究报告 `research.md`，包含：
  - 技术栈现状
  - 代码风格分析
  - 相关目录结构
  - 业务逻辑分析
  - 技术实现方案

### 4. 主题讨论 (`/senatus.discuss` 或 `/senatus.inspire`)
```bash
/senatus.discuss 我们应该使用JWT还是Session进行身份验证？
# 或者
/senatus.inspire
```
- `/senatus.discuss`：针对具体问题进行讨论
- `/senatus.inspire`：自动识别争议点并启发讨论
- 所有讨论记录都会添加到 `discuss.md` 文件中
- 记录格式：`D01 - 日期时间`，包含问题和结论

### 5. 生成任务计划 (`/senatus.plan`)
```bash
/senatus.plan
# 或带有额外注意事项
/senatus.plan 注意保持向后兼容性
```
- 基于讨论结果和研究成果生成可执行的任务列表
- 可选：提供额外的注意事项或约束条件
- 创建 `plan.md` 文件，包含编号的任务项（T01, T02, T03...）
- 每个任务项都有明确的状态：⏳待执行 / 🔄进行中 / ✅已完成

### 6. 执行任务 (`/senatus.implement`)
```bash
# 批量执行（最多5个任务）
/senatus.implement
```
- 自动识别下一个待执行的任务项
- `/senatus.implement`：批量执行最多5个待执行任务
- 为每个完成的任务生成实施记录
- 更新任务计划中的状态
- 可重复运行直到所有任务完成

### 7. 修复问题 (`/senatus.correct`)
```bash
/senatus.correct 修复用户认证模块的Session过期时间配置
```
- 根据用户反馈立即执行问题修复
- 自动记录修复过程和结果
- 在讨论记录中添加修复条目
- 在任务计划中添加已完成的修复任务
- 生成详细的修复实施记录

### 8. 收集手动变更 (`/senatus.collect`)
```bash
# 先手动修改代码并暂存
git add .

# 收集变更并记录
/senatus.collect
```
- 读取 Git staged 变更（`git diff --cached`）
- 自动分析暂存区代码变更的目的和影响
- 验证变更是否符合项目宪法约束
- 自动生成变更描述
- 将变更作为已完成任务添加到任务计划
- 生成详细的实施记录

## 命令详解

### `/senatus.implement` - 执行任务（批量）
**作用**：自动化批量执行待办任务项

**输出**：
- 更新的 `plan.md`（状态更新）
- `implementation/[任务编号].md`（实施记录）

**特点**：
- 批量执行（最多5个任务）
- 自动生成实施文档
- 智能进度跟踪

### `/senatus.collect` - 收集手动变更
**作用**：收集用户手动修改的代码变更并记录到框架中

**输出**：
- 更新的 `plan.md`（新增已完成任务）
- `implementation/[任务编号].md`（实施记录）

**特点**：
- 读取 Git staged 变更
- 自动分析暂存区变更目的和影响
- 验证是否符合项目宪法约束
- 自动生成变更描述

### `/senatus.constitution` - 项目宪法
**作用**：创建项目的全局约束文件

**输出**：`specify/constitution.md`

**特点**：
- 自动分析项目技术栈
- 生成分类约束条款
- 支持版本管理和历史记录

### `/senatus.context` - 了解项目背景
**作用**：综合了解项目背景，为后续讨论做准备

**输出**：无

**特点**：
- 综合分析项目宪法、主题、研究报告和已有实现记录
- 基于完整上下文理解项目现状
- 严格遵循项目宪法约束

### `/senatus.correct [问题描述]` - 修复问题
**作用**：根据用户反馈修复项目问题

**参数**：问题描述（必需）

**输出**：
- 更新的 `discuss.md`（新增讨论记录）
- 更新的 `plan.md`（新增已完成任务）
- `implementation/[任务编号].md`（修复记录）

**特点**：
- 基于用户反馈进行精准修复
- 自动记录修复过程和结果
- 即时更新讨论和任务记录

### `/senatus.discuss [讨论内容]` - 主题讨论
**作用**：针对特定问题进行结构化讨论

**参数**：讨论内容（必需）

**输出**：在 `discuss.md` 中添加讨论记录

**特点**：
- 基于项目研究成果进行讨论
- 严格遵循项目宪法约束
- 自动编号和时间戳记录

### `/senatus.inspire` - 启发讨论
**作用**：自动识别争议点，启发有价值的讨论

**输出**：在 `discuss.md` 中添加讨论记录

**特点**：
- 智能识别技术决策点
- 基于项目现状发现问题
- 引导深入技术讨论

### `/senatus.new-topic [主题描述]` - 新建主题
**作用**：创建结构化的讨论主题

**参数**：主题描述（必需）

**输出**：`specify/[序号]-[主题名]/discuss.md`

**特点**：
- 自动生成kebab-case目录名
- 分配递增的三位数序号
- 基于模板创建标准化文档

### `/senatus.plan [注意事项]` - 生成计划
**作用**：将讨论结果转化为可执行的任务列表

**参数**：注意事项（可选）- 生成计划时需要考虑的额外约束或要求

**输出**：`specify/[当前主题]/plan.md`

**特点**：
- 基于所有讨论记录和研究报告生成任务项
- 支持用户输入额外的注意事项
- 按执行顺序排列
- 支持状态跟踪
- 严格遵循项目宪法约束

### `/senatus.research` - 项目研究
**作用**：深入分析项目源码，生成研究报告

**输出**：`specify/[当前主题]/research.md`

**分析内容**：
- 技术栈识别
- 代码风格和架构模式
- 相关文件和目录结构
- 业务逻辑和技术实现

## 文档规范

### 编号系统
- **主题**：001, 002, 003...（三位数递增）
- **讨论**：D01, D02, D03...（D = Discussion）
- **任务**：T01, T02, T03...（T = Task）

### 状态标记
- **⏳待执行**：任务项尚未开始
- **🔄进行中**：任务项部分完成，需继续执行
- **✅已完成**：任务项已完成

### 文件命名
- 主题目录：`[序号]-[kebab-case主题名]/`
- 实施记录：`implementation/T[编号].md`

## 使用示例

### 完整工作流示例

```bash
# 1. 创建项目宪法
/senatus.constitution

# 2. 开始新主题
/senatus.new-topic 重构用户管理模块

# 3. 进行项目研究
/senatus.research

# 4. 讨论技术方案
/senatus.discuss 应该使用什么架构模式来重构用户管理？

# 5. 启发更多讨论点
/senatus.inspire

# 6. 生成任务计划
/senatus.plan

# 7. 批量执行任务项（一次最多5个任务）
/senatus.implement
# 可重复执行直到所有任务完成
/senatus.implement

# 8. 修复问题（如需要）
/senatus.correct 修复用户认证模块的配置问题

# 9. 收集手动变更（如需要）
# 手动修改代码...
git add .
/senatus.collect
```

### 生成的文件结构示例

```
specify/
├── constitution.md
└── 001-refactor-user-management/
    ├── discuss.md
    ├── research.md
    ├── plan.md
    └── implementation/
        ├── T01.md
        ├── T02.md
        └── T03.md
```

## 最佳实践

1. **始终从宪法开始**：为每个项目建立清晰的约束条件
2. **一次专注一个主题**：避免同时处理多个复杂主题
3. **充分研究后再讨论**：确保基于准确的项目理解进行决策
4. **记录所有争议点**：使用 `/senatus.inspire` 发现隐藏的技术问题
5. **小步快跑**：将大任务分解为可管理的任务项
6. **保持追溯性**：完整保留所有决策过程和实施记录

## 贡献与支持

Senatus Framework 由 [PaodingSoftware](https://github.com/PaodingSoftware) 开发和维护。

**项目地址**：https://github.com/PaodingSoftware/senatus

---

*通过 Senatus Framework，让每一个技术决策都有据可循，让每一次实施都有迹可循。*