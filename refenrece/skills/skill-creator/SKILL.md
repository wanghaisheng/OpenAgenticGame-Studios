---
name: skill-creator
description: 创建有效 Skill 的指南。当用户想要创建新 Skill （或更新现有 Skill ）以通过专业知识、工作流或工具集成扩展 Claude 能力时，应使用此 Skill 。
license: 完整条款请参阅 LICENSE.txt
---

# Skill creator

此 Skill 为创建有效 Skill 提供指导。

## 关于 Skill

Skill 是模块化的、自包含的包，通过提供专业知识、工作流和工具来扩展 Claude 的能力。可以将它们视为特定领域或任务的"入职指南"——它们将 Claude 从通用代理转变为具备过程知识的专门代理，而这是任何模型都无法完全拥有的。

### Skill 提供的内容

1. 专门化工作流 - 特定领域的多步骤程序
2. 工具集成 - 使用特定文件格式或 API 的说明
3. 领域专业知识 - 公司特定的知识、架构、业务逻辑
4. 捆绑资源 - 用于复杂和重复任务的脚本、参考和资产

###  Skill 剖析

每个 Skill 由必需的 SKILL.md 文件和可选的捆绑资源组成：

```
skill-name/
├── SKILL.md (必需)
│   ├── YAML 前言元数据（必需）
│   │   ├── name: (必需)
│   │   └── description: (必需)
│   └── Markdown 指令（必需）
└── 捆绑资源（可选）
    ├── scripts/          - 可执行代码（Python/Bash/etc.）
    ├── references/       - 文档，根据需要加载到上下文中
    └── assets/           - 输出中使用的文件（模板、图标、字体等）
```

#### SKILL.md（必需）

**元数据质量：** YAML 前言中的 `name` 和 `description` 决定了 Claude 何时使用该 Skill 。应具体说明该 Skill 的功能以及何时使用。使用第三人称（例如"此 Skill 应用于..."而不是"使用此 Skill 当..."）。

#### 捆绑资源（可选）

##### Scripts (`scripts/`)

用于需要确定性可靠性或重复重写的任务的可执行代码（Python/Bash/etc.）。

- **何时包含：** 当同一代码被重复重写或需要确定性可靠性时
- **示例：** 用于 PDF 旋转任务的 `scripts/rotate_pdf.py`
- **优势：** 高效使用 Token、确定性、可能在无需加载到上下文的情况下执行
- **注意：** Claude 仍可能需要读取脚本以进行修补或特定环境的调整

##### References (`references/`)

旨在根据需要加载到上下文中以通知 Claude 过程和思维的文档和参考材料。

- **何时包含：** 用于 Claude 在工作时应该参考的文档
- **示例：** 用于财务架构的 `references/finance.md`、用于公司 NDA 模板的 `references/mnda.md`、用于公司策略的 `references/policies.md`、用于 API 规范的 `references/api_docs.md`
- **用例：** 数据库架构、API 文档、领域知识、公司策略、详细的工作流指南
- **优势：** 保持 SKILL.md 精简，仅在 Claude 确定需要时加载
- **最佳实践：** 如果文件很大（>10k 字），请在 SKILL.md 中包含 grep 搜索模式
- **避免重复：** 信息应存在于 SKILL.md 或参考文件中，而不是两者中。首选参考文件用于详细信息，除非它确实是 Skill 的核心——这使 SKILL.md 保持精简，同时使信息可发现而不会占用上下文窗口。仅在 SKILL.md 中保留基本的过程指令和工作流指导；将详细的参考材料、架构和示例移至参考文件。

##### Assets (`assets/`)

不打算加载到上下文中，而是在 Claude 产生的输出中使用的文件。

- **何时包含：** 当 Skill 需要在最终输出中使用的文件时
- **示例：** 用于品牌资产的 `assets/logo.png`、用于 PowerPoint 模板的 `assets/slides.pptx`、用于 HTML/React 样板的 `assets/frontend-template/`、用于排版的 `assets/font.ttf`
- **用例：** 模板、图像、图标、样板代码、字体、被复制或修改的示例文档
- **优势：** 将输出资源与文档分离，使 Claude 能够使用文件而无需将其加载到上下文中

### 渐进式披露设计原则

 Skill 使用三级加载系统来高效管理上下文：

1. **元数据（name + description）** - 始终在上下文中（~100 字）
2. **SKILL.md 主体** -  Skill 触发时（<5k 字）
3. **捆绑资源** - 根据 Claude 需要（无限制*）

*无限制是因为脚本可以在不读取到上下文窗口的情况下执行。

##  Skill 创建流程

要创建 Skill ，请按顺序遵循" Skill 创建流程"，仅在明显不适用时跳过步骤。

### 第 1 步：通过具体示例理解 Skill 

仅在 Skill 的使用模式已经清楚理解时才跳过此步骤。即使在使用现有 Skill 时，它仍然有价值。

要创建有效的 Skill ，请清楚地了解如何使用该 Skill 的具体示例。这种理解可以来自直接的用户示例或经过用户反馈验证的生成示例。

例如，在构建图像编辑器 Skill 时，相关问题包括：

- "图像编辑器 Skill 应该支持什么功能？编辑、旋转，还有其他吗？"
- "能否举一些如何使用此 Skill 的示例？"
- "我可以想象用户要求'从此图像中消除红眼'或'旋转此图像'。还有其他您想象此 Skill 的使用方式吗？"
- "用户会说什么来触发此 Skill ？"

为避免压倒用户，请避免在单条消息中问太多问题。从最重要的问题开始，并根据需要跟进以提高效果。

当清楚了解 Skill 应支持的功能时，结束此步骤。

### 第 2 步：规划可重用的 Skill 内容

要将具体示例转化为有效的 Skill ，通过以下方式分析每个示例：

1. 考虑如何从头开始执行该示例
2. 识别在重复执行这些工作流时会有帮助的脚本、参考和资产

示例：在构建 `pdf-editor`  Skill 以处理"帮我旋转此 PDF"等查询时，分析显示：

1. 旋转 PDF 每次都需要重写相同的代码
2. 在 Skill 中存储 `scripts/rotate_pdf.py` 脚本会有帮助

示例：在设计 `frontend-webapp-builder`  Skill 以处理"为我构建一个待办事项应用"或"为我构建一个仪表板来跟踪我的步数"等查询时，分析显示：

1. 编写前端 Web 应用每次都需要相同的样板 HTML/React
2. 在 Skill 中存储包含样板 HTML/React 项目文件的 `assets/hello-world/` 模板会有帮助

示例：在构建 `big-query`  Skill 以处理"今天有多少用户登录？"等查询时，分析显示：

1. 每次查询 BigQuery 都需要重新发现表架构和关系
2. 在 Skill 中存储记录表架构的 `references/schema.md` 文件会有帮助

要建立 Skill 的内容，分析每个具体示例以创建要包含的可重用资源列表：脚本、参考和资产。

### 第 3 步：初始化 Skill 

此时，是时候实际创建 Skill 了。

仅在正在开发的 Skill 已存在，并且需要迭代或打包时才跳过此步骤。在这种情况下，继续下一步。

从零开始创建新 Skill 时，始终运行 `init_skill.py` 脚本。该脚本方便地生成新的模板 Skill 目录，自动包含 Skill 所需的一切，使 Skill 创建过程更加高效和可靠。

用法：

```bash
scripts/init_skill.py <skill-name> --path <output-directory>
```

该脚本：

- 在指定路径创建 Skill 目录
- 生成具有正确前言和 TODO 占位符的 SKILL.md 模板
- 创建示例资源目录：`scripts/`、`references/` 和 `assets/`
- 在每个目录中添加可以自定义或删除的示例文件

初始化后，根据需要自定义或删除生成的 SKILL.md 和示例文件。

### 第 4 步：编辑 Skill 

编辑（新生成的或现有的） Skill 时，请记住该 Skill 是为另一个 Claude 实例创建的。专注于包含对 Claude 有益且不明显的信息。考虑什么样的过程知识、领域特定细节或可重用资产将帮助另一个 Claude 实例更有效地执行这些任务。

#### 从可重用 Skill 内容开始

要开始实现，从上面确定的可重用资源开始：`scripts/`、`references/` 和 `assets/` 文件。请注意，此步骤可能需要用户输入。例如，在实现 `brand-guidelines`  Skill 时，用户可能需要提供要存储在 `assets/` 中的品牌资产或模板，或要存储在 `references/` 中的文档。

此外，删除 Skill 不需要的任何示例文件和目录。初始化脚本在 `scripts/`、`references/` 和 `assets/` 中创建示例文件以演示结构，但大多数 Skill 不需要所有这些。

#### 更新 SKILL.md

**写作风格：** 使用**祈使/不定式形式**（动词优先指令）编写整个 Skill ，而不是第二人称。使用客观、指导性语言（例如，"要完成 X，执行 Y"而不是"你应该做 X"或"如果你需要做 X"）。这为 AI 消费保持了一致性和清晰度。

要完成 SKILL.md，回答以下问题：

1.  Skill 的目的是什么，用几句话描述？
2. 何时应使用该 Skill ？
3. 在实践中，Claude 应该如何使用该 Skill ？应引用上面开发的所有可重用 Skill 内容，以便 Claude 知道如何使用它们。

### 第 5 步：打包 Skill 

 Skill 准备好后，应将其打包为可分发的 zip 文件，与用户共享。打包过程首先自动验证 Skill 以确保它满足所有要求：

```bash
scripts/package_skill.py <path/to/skill-folder>
```

可选输出目录规范：

```bash
scripts/package_skill.py <path/to/skill-folder> ./dist
```

打包脚本将：

1. **验证** Skill 自动，检查：
   - YAML 前言格式和必需字段
   -  Skill 命名约定和目录结构
   - 描述完整性和质量
   - 文件组织和资源引用

2. 如果验证通过，**打包** Skill ，创建以 Skill 命名的 zip 文件（例如，`my-skill.zip`），其中包括所有文件并保持适当的目录结构以进行分发。

如果验证失败，脚本将报告错误并退出而不创建包。修复任何验证错误并再次运行打包命令。

### 第 6 步：迭代

在测试 Skill 后，用户可能会请求改进。通常这就在使用 Skill 之后发生，并对 Skill 的表现有新鲜的上下文。

**迭代工作流：**
1. 在实际任务上使用 Skill 
2. 注意困难或低效
3. 识别 SKILL.md 或捆绑资源应如何更新
4. 实施更改并再次测试