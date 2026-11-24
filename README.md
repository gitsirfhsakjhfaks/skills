# Sun Skills

三个帮助理解问题、检验理解和复用工作经验的 Codex Skill：使用 `sun-focused-analysis` 看清关键关系，使用 `sun-inquiry` 检验自己是否理解，再用 `sun-work-experience` 沉淀和找回可复用的工作方法。三个 Skill 可以独立使用。

## 包含什么

| Skill | 解决的问题 | 使用方式 |
| --- | --- | --- |
| [sun-focused-analysis](skills/sun-focused-analysis/SKILL.md) | 复杂回答信息太散，看不清核心关系、依据和必要前提。 | 显式调用 `$sun-focused-analysis`。 |
| [sun-inquiry](skills/sun-inquiry/SKILL.md) | 看过回答，但不确定自己是否抓住主干、能否应对实际追问。 | 调用 `$sun-inquiry`，或明确要求检验理解。 |
| [sun-work-experience](skills/sun-work-experience/SKILL.md) | 工作经验散落在对话中，下次难以复用，也缺少可供周报使用的事实记录。 | 调用 `$sun-work-experience`，或要求沉淀工作、记录过程、找回已有经验。 |

## 统一命名

三个 Skill 均使用上表中的英文名称和 `sun-` 前缀。安装目录、`SKILL.md` 中的 `name`、界面展示名称和调用标识保持一致，不翻译或另起中文名；调用时在名称前加 `$`。

### sun-focused-analysis

围绕当前问题的关键关系深入解释，先建立骨架，再展开必要的推导。保留影响判断的证据、前提和不确定性，减少无关分支；不以省略关键逻辑来换取简短。

该 Skill 仅在明确调用时启用，保留了 `allow_implicit_invocation: false` 配置。启用后在当前聊天中持续采用，直到用户明确要求停用。

### sun-inquiry

默认检验主干：每次只问一个关键问题，等待用户独立回答，再根据具体回答判断是理解正确、不完整、错误，还是表达需要澄清。针对偏差解释后，换个角度复测。

主干掌握后，先询问用户是否开启场景检验；用户选择后，再模拟评审、汇报、答辩或实际应用中的追问。

发现适合动态展示的理解偏差时，可在用户选择后生成独立 HTML 文件。页面可离线打开和复用，保留相关材料摘录、原始问答、诊断与纠正依据、模型假设和复测状态，方便追溯。

### sun-work-experience

从工作对话和相关材料中提炼可复用经验，分别保存经验记录和会话工作日志，保留必要的复现材料。工作日志可以作为周报输入；遇到新问题时，可找回相关经验并判断适用条件。

只记录有依据的事实，区分 AI 建议、用户采用、实际执行和验证结果。新整理内容保留待核对状态，不把推测写成已取得的成果。

## 安装

在 Codex 中使用内置安装 Skill：

```text
使用 $skill-installer，从 https://github.com/gitsirfhsakjhfaks/skills 安装 skills/sun-focused-analysis、skills/sun-inquiry 和 skills/sun-work-experience 这三个 Skill。保留各自的英文目录名和展示名称。
```

也可以下载本仓库，将 `skills/` 中的三个完整目录复制到用户级的 `~/.agents/skills/`，或目标项目的 `.agents/skills/`。保留各目录中的 `agents/` 和 `references/`。这些是官方文档列出的本地 Skill 发现位置；安装后未出现时可重启 Codex。[官方安装与发现说明](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)

已安装旧名称的用户，应以对应的新目录替换旧目录，避免同时保留两份。`sun-work-experience` 的已有记录库路径和 `WORK_EXPERIENCE_HOME` 设置继续沿用。

## 使用示例

先分析一个问题：

```text
使用 $sun-focused-analysis，帮我理解下面这个方案的核心机制、关键依据和成立条件：
（粘贴方案或明确指向当前上下文）
```

需要检查理解时，再调用 `sun-inquiry`：

```text
使用 $sun-inquiry，检验我对上面这段回答的主干理解。一次问一个问题，等我回答后再评价。
```

已经掌握主干、希望模拟评审时：

```text
继续开启场景检验，模拟方案评审，检查我能否解释这个方案的依据、取舍和适用条件。
```

需要沉淀本次工作时：

```text
使用 $sun-work-experience，整理这次工作中值得复用的经验，并另存会话工作日志作为周报输入。
```

遇到类似问题、需要找回经验时：

```text
使用 $sun-work-experience，找一下以前解决类似问题的方法，说明哪些步骤适用于当前条件。
```

## 目录

```text
skills/
├── sun-focused-analysis/
│   ├── SKILL.md
│   └── agents/openai.yaml
├── sun-inquiry/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/html-remediation.md
└── sun-work-experience/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/record-formats.md
```

三个 Skill 均以指令为主，不需要额外安装脚本依赖。`sun-inquiry` 中的 HTML 辅助环节需要运行环境能够创建文件；具备浏览器能力时，应进一步验证保存后的交互页面。`sun-work-experience` 的保存和找回流程需要访问指定记录库。

## 许可证

本仓库采用 [MIT License](LICENSE)。
