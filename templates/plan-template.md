# 实施计划：[FEATURE]

**分支**：`[###-feature-name]` | **日期**：[DATE] | **规范**：[link]
**输入**：来自 `/specs/[###-feature-name]/spec.md` 的功能规范

**注意**：此模板由 `/speckit.plan` 命令填充。请参阅 `.specify/templates/commands/plan.md` 了解执行工作流。

## 摘要

[从功能规范中提取：主要需求 + 研究得出的技术方案]

## 技术上下文

<!--
  需要采取行动：将本节中的内容替换为项目的技术细节。
  此处的结构仅供参考，旨在指导迭代过程。
-->

**语言/版本**：[例如，Python 3.11, Swift 5.9, Rust 1.75 或 需要澄清]  
**主要依赖**：[例如，FastAPI, UIKit, LLVM 或 需要澄清]  
**存储**：[如果适用，例如，PostgreSQL, CoreData, files 或 不适用]  
**测试**：[例如，pytest, XCTest, cargo test 或 需要澄清]  
**目标平台**：[例如，Linux server, iOS 15+, WASM 或 需要澄清]
**项目类型**：[single/web/mobile - 决定源结构]  
**性能目标**：[特定领域，例如，1000 req/s, 10k lines/sec, 60 fps 或 需要澄清]  
**约束**：[特定领域，例如，<200ms p95, <100MB memory, offline-capable 或 需要澄清]  
**规模/范围**：[特定领域，例如，10k users, 1M LOC, 50 screens 或 需要澄清]

## 章程检查

*关卡：必须在第 0 阶段研究之前通过。在第 1 阶段设计后重新检查。*

[根据章程文件确定的关卡]

## 项目结构

### 文档（此功能）

```text
specs/[###-feature]/
├── plan.md              # 此文件 (/speckit.plan 命令输出)
├── research.md          # 第 0 阶段输出 (/speckit.plan 命令)
├── data-model.md        # 第 1 阶段输出 (/speckit.plan 命令)
├── quickstart.md        # 第 1 阶段输出 (/speckit.plan 命令)
├── contracts/           # 第 1 阶段输出 (/speckit.plan 命令)
└── tasks.md             # 第 2 阶段输出 (/speckit.tasks 命令 - 不是由 /speckit.plan 创建)
```

### 源代码（仓库根目录）
<!--
  需要采取行动：将下面的占位符树替换为此功能的具体布局。
  删除未使用的选项，并使用实际路径（例如，apps/admin, packages/something）展开所选结构。
  交付的计划不得包含选项标签。
-->

```text
# [如果不使用则删除] 选项 1：单个项目（默认）
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# [如果不使用则删除] 选项 2：Web 应用程序（当检测到 "frontend" + "backend" 时）
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# [如果不使用则删除] 选项 3：移动 + API（当检测到 "iOS/Android" 时）
api/
└── [与上面的 backend 相同]

ios/ 或 android/
└── [特定于平台的结构：功能模块，UI 流程，平台测试]
```

**结构决策**：[记录所选结构并引用上面捕获的实际目录]

## 复杂度跟踪

> **仅当章程检查有违规且必须证明合理时才填写**

| 违规项 | 为何需要 | 拒绝更简单替代方案的原因 |
|-----------|------------|-------------------------------------|
| [例如，第 4 个项目] | [当前需求] | [为何 3 个项目不足] |
| [例如，Repository 模式] | [具体问题] | [为何直接 DB 访问不足] |
