# Senatus Framework

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
│       ├── action.md       # 执行行动项
│       ├── collect.md      # 收集手动变更
│       ├── constitution.md # 创建项目宪法
│       ├── correct.md      # 项目纠正
│       ├── discuss.md      # 主题讨论
│       ├── inspire.md      # 启发式讨论
│       ├── new-topic.md    # 创建新讨论主题
│       ├── plan.md         # 生成行动计划
│       └── research.md     # 项目源码研究
├── .github/
│   └── prompts/            # GitHub Copilot 提示词
│       ├── action.prompt.md
│       ├── collect.prompt.md
│       ├── constitution.prompt.md
│       ├── correct.prompt.md
│       ├── discuss.prompt.md
│       ├── inspire.prompt.md
│       ├── new-topic.prompt.md
│       ├── plan.prompt.md
│       └── research.prompt.md
├── .specify/               # 文档模板
│   ├── discuss-template.md      # 讨论文档模板
│   ├── research-template.md     # 研究报告模板
│   ├── plan-template.md         # 行动计划模板
│   ├── implementation-template.md # 实施记录模板
│   └── constitution-template.md # 项目宪法模板
└── specify/                # 工作目录（使用时生成）
    ├── constitution.md     # 项目约束宪法
    └── [编号]-[主题名]/    # 主题工作目录
        ├── discuss.md      # 讨论记录
        ├── research.md     # 研究报告
        ├── plan.md         # 行动计划
        └── implementation/ # 实施记录目录
            └── [行动编号].md
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

### 1. 建立项目约束 (`/constitution`)
```bash
/constitution
```
- 分析项目结构和技术栈
- 生成项目宪法文件 `specify/constitution.md`
- 定义技术约束、质量约束、安全约束、业务约束
- 后续所有操作都必须遵循这些约束

### 2. 创建讨论主题 (`/new-topic`)
```bash
/new-topic 实现用户认证功能
```
- 创建新的主题目录（如 `specify/001-implement-user-auth/`）
- 生成初始讨论文档 `discuss.md`
- 为主题分配唯一序号

### 3. 项目研究 (`/research`)
```bash
/research
```
- 分析与当前主题相关的项目源码
- 生成详细的研究报告 `research.md`，包含：
  - 技术栈现状
  - 代码风格分析
  - 相关目录结构
  - 业务逻辑分析
  - 技术实现方案

### 4. 主题讨论 (`/discuss` 或 `/inspire`)
```bash
/discuss 我们应该使用JWT还是Session进行身份验证？
# 或者
/inspire
```
- `/discuss`：针对具体问题进行讨论
- `/inspire`：自动识别争议点并启发讨论
- 所有讨论记录都会添加到 `discuss.md` 文件中
- 记录格式：`D01 - 日期时间`，包含问题和结论

### 5. 生成行动计划 (`/plan`)
```bash
/plan
```
- 基于讨论结果和研究成果生成可执行的行动列表
- 创建 `plan.md` 文件，包含编号的行动项（A01, A02, A03...）
- 每个行动项都有明确的状态：⏳待执行 / ✅已完成

### 6. 执行行动 (`/action`)
```bash
/action
```
- 自动识别下一个待执行的行动项
- 批量执行最多5个待执行行动
- 为每个完成的行动生成实施记录
- 更新行动计划中的状态
- 可重复运行直到所有行动完成

### 7. 项目纠正 (`/correct`)
```bash
/correct 修正用户认证模块的Session过期时间配置
```
- 根据用户反馈立即执行项目纠正
- 自动记录纠正过程和结果
- 在讨论记录中添加纠正条目
- 在行动计划中添加已完成的纠正行动
- 生成详细的纠正实施记录

### 8. 收集手动变更 (`/collect`)
```bash
# 先手动修改代码并暂存
git add .

# 收集变更并记录
/collect
```
- 读取 Git staged 变更（`git diff --cached`）
- 自动分析暂存区代码变更的目的和影响
- 验证变更是否符合项目宪法约束
- 自动生成变更描述
- 将变更作为已完成行动添加到行动计划
- 生成详细的实施记录

## 命令详解

### `/action` - 执行行动
**作用**：自动化执行待办行动项

**输出**：
- 更新的 `plan.md`（状态更新）
- `implementation/[行动编号].md`（实施记录）

**特点**：
- 批量执行（最多5个行动）
- 自动生成实施文档
- 智能进度跟踪

### `/collect` - 收集手动变更
**作用**：收集用户手动修改的代码变更并记录到框架中

**输出**：
- 更新的 `plan.md`（新增已完成行动）
- `implementation/[行动编号].md`（实施记录）

**特点**：
- 读取 Git staged 变更
- 自动分析暂存区变更目的和影响
- 验证是否符合项目宪法约束
- 自动生成变更描述

### `/constitution` - 项目宪法
**作用**：创建项目的全局约束文件

**输出**：`specify/constitution.md`

**特点**：
- 自动分析项目技术栈
- 生成分类约束条款
- 支持版本管理和历史记录

### `/correct [纠正内容]` - 项目纠正
**作用**：根据用户反馈对项目进行纠正

**参数**：纠正内容（必需）

**输出**：
- 更新的 `discuss.md`（新增讨论记录）
- 更新的 `plan.md`（新增已完成行动）
- `implementation/[行动编号].md`（纠正记录）

**特点**：
- 基于用户反馈进行精准纠正
- 自动记录纠正过程和结果
- 即时更新讨论和行动记录

### `/discuss [讨论内容]` - 主题讨论
**作用**：针对特定问题进行结构化讨论

**参数**：讨论内容（必需）

**输出**：在 `discuss.md` 中添加讨论记录

**特点**：
- 基于项目研究成果进行讨论
- 严格遵循项目宪法约束
- 自动编号和时间戳记录

### `/inspire` - 启发讨论
**作用**：自动识别争议点，启发有价值的讨论

**输出**：在 `discuss.md` 中添加讨论记录

**特点**：
- 智能识别技术决策点
- 基于项目现状发现问题
- 引导深入技术讨论

### `/new-topic [主题描述]` - 新建主题
**作用**：创建结构化的讨论主题

**参数**：主题描述（必需）

**输出**：`specify/[序号]-[主题名]/discuss.md`

**特点**：
- 自动生成kebab-case目录名
- 分配递增的三位数序号
- 基于模板创建标准化文档

### `/plan` - 生成计划
**作用**：将讨论结果转化为可执行的行动列表

**输出**：`specify/[当前主题]/plan.md`

**特点**：
- 基于所有讨论记录生成行动项
- 按执行顺序排列
- 支持状态跟踪

### `/research` - 项目研究
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
- **行动**：A01, A02, A03...（A = Action）

### 状态标记
- **⏳待执行**：行动项尚未开始
- **✅已完成**：行动项已完成

### 文件命名
- 主题目录：`[序号]-[kebab-case主题名]/`
- 实施记录：`implementation/A[编号].md`

## 使用示例

### 完整工作流示例

```bash
# 1. 创建项目宪法
/constitution

# 2. 开始新主题
/new-topic 重构用户管理模块

# 3. 进行项目研究
/research

# 4. 讨论技术方案
/discuss 应该使用什么架构模式来重构用户管理？

# 5. 启发更多讨论点
/inspire

# 6. 生成行动计划
/plan

# 7. 执行行动项
/action
# 可重复执行直到所有行动完成
/action

# 8. 纠正问题（如需要）
/correct 修正用户认证模块的配置问题

# 9. 收集手动变更（如需要）
# 手动修改代码...
git add .
/collect
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
        ├── A01.md
        ├── A02.md
        └── A03.md
```

## 最佳实践

1. **始终从宪法开始**：为每个项目建立清晰的约束条件
2. **一次专注一个主题**：避免同时处理多个复杂主题
3. **充分研究后再讨论**：确保基于准确的项目理解进行决策
4. **记录所有争议点**：使用 `/inspire` 发现隐藏的技术问题
5. **小步快跑**：将大任务分解为可管理的行动项
6. **保持追溯性**：完整保留所有决策过程和实施记录

## 贡献与支持

Senatus Framework 由 [PaodingSoftware](https://github.com/PaodingSoftware) 开发和维护。

**项目地址**：https://github.com/PaodingSoftware/senatus

---

*通过 Senatus Framework，让每一个技术决策都有据可循，让每一次实施都有迹可循。*