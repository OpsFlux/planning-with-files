# 用文件规划（Planning with Files）

> **像 Manus 一样工作** —— 据报道 Meta 以 **20 亿美元**收购的 AI 智能体公司。

这是一个 Claude Code 技能：把你的工作流改造成用持久化的 Markdown 文件来做计划、追踪进度、沉淀知识——这正是 Manus 用来规模化执行复杂任务的核心模式。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-blue)](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/skills)

## Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=OthmanAdi/planning-with-files&type=Date)](https://star-history.com/#OthmanAdi/planning-with-files&Date)

---

## 为什么需要这个技能？

在 2025 年 12 月 29 日，[Meta 以 20 亿美元收购 Manus](https://techcrunch.com/2025/12/29/meta-just-bought-manus-an-ai-startup-everyone-has-been-talking-about/)。短短 8 个月，Manus 从发布到实现 1 亿美元以上收入。它们的秘诀？**上下文工程（Context Engineering）**。

这个技能实现了 Manus 的核心工作流模式：

> “Markdown 是我写在磁盘上的‘工作记忆’。由于我以迭代方式处理信息，而活跃上下文存在限制，Markdown 文件就充当了笔记草稿纸、进度检查点，以及最终交付物的构建块。”
> —— Manus AI

## 问题

Claude Code（以及大多数 AI 智能体）常见问题：

- **记忆易失** —— TodoWrite 工具在上下文重置后会消失
- **目标漂移** —— 工具调用 50+ 次后，最初目标容易被遗忘
- **错误隐形** —— 失败不被记录，同类错误反复出现
- **上下文塞爆** —— 所有内容都塞进上下文，而不是落盘存储

## 解决方案：三文件模式

对每个复杂任务，都创建三个文件：

```
task_plan.md      → 追踪阶段与进度
notes.md          → 存放调研与发现
[deliverable].md  → 最终交付物
```

### 循环流程

```
1. 创建 task_plan.md，写清目标与阶段
2. 调研 → 写入 notes.md → 更新 task_plan.md
3. 阅读 notes.md → 生成交付物 → 更新 task_plan.md
4. 交付最终产物
```

**关键洞察：** 每次做重大决策前都阅读 `task_plan.md`，就能让目标一直停留在注意力窗口。这也是 Manus 能撑住 ~50 次工具调用仍不跑偏的原因。

## 安装

### 方案 1：直接克隆（推荐）

```bash
# 进入你的 Claude Code skills 目录
cd ~/.claude/skills  # or your custom skills path

# 克隆本技能
git clone https://github.com/OthmanAdi/planning-with-files.git
```

### 方案 2：手动安装

1. 下载或复制 `planning-with-files` 文件夹
2. 放到你的 Claude Code skills 目录：
   - macOS/Linux：`~/.claude/skills/`
   - Windows：`%USERPROFILE%\.claude\skills\`

### 验证安装

在 Claude Code 里，满足以下情况技能会自动激活：
- 开始复杂任务
- 提到 “planning / organize / track progress” 之类的意图
- 需要结构化产出

## 使用方式

安装后，Claude 会自动：

1. 在复杂任务开始前 **创建 `task_plan.md`**
2. 每完成一个阶段就用复选框 **更新进度**
3. 把发现写进 **`notes.md`**，而不是塞爆上下文
4. **记录错误**，便于复盘复用
5. 重大决策前 **重读计划**，把目标拉回注意力窗口

### 示例

**你：**“调研 TypeScript 的优势并写一份总结”

**Claude 会创建：**

```markdown
# 任务计划：TypeScript 优势调研

## 目标
产出一份关于 TypeScript 优势的调研总结。

## 阶段
- [x] 阶段 1：创建计划 ✓
- [ ] 阶段 2：调研并收集来源（当前）
- [ ] 阶段 3：综合整理发现
- [ ] 阶段 4：交付总结

## 状态
**当前处于阶段 2** —— 正在搜索资料来源
```

随后按阶段推进，并在过程中持续更新文件。

## Manus 原则

这个技能落实了以下关键的上下文工程原则：

| 原则 | 落地方式 |
|------|----------|
| 文件系统即记忆 | 内容写入文件，而非塞入上下文 |
| 用重复操控注意力 | 决策前重读计划 |
| 错误可持久化 | 在计划文件里记录失败 |
| 目标可追踪 | 复选框展示进度 |
| 仅追加式上下文 | 不改历史，只追加新信息 |

## 文件结构

```
planning-with-files/
├── SKILL.md        # 核心说明（Claude 会读取）
├── reference.md    # Manus 原则深度解析
├── examples.md     # 真实使用示例
└── README.md       # 本文件
```

## 何时使用

**适用：**
- 多步骤任务（3+ 步）
- 调研类任务
- 构建/创建项目
- 跨多次工具调用的任务
- 任何需要组织与跟踪的工作

**不适用：**
- 简单问题
- 单文件编辑
- 快速查询

## 致谢

- **Manus AI** —— 率先探索并沉淀了这套上下文工程模式
- **Anthropic** —— 提供 Claude Code 与 Agent Skills 框架
- 灵感来源：[Context Engineering for AI Agents](https://manus.im/de/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus)

## 贡献

欢迎贡献！你可以：
1. Fork 仓库
2. 新建功能分支
3. 提交 Pull Request

## 许可证

MIT 许可证 —— 可自由使用、修改与分发。

## 感谢

感谢每一位 star、fork 和分享过这个技能的人。这个项目在不到 24 小时里就迅速传播开来，社区的支持非常给力。

如果这个技能能帮你更高效地工作，那就达成我的目的了。

---

**作者：** [Ahmad Othman Ammar Adi](https://github.com/OthmanAdi)
