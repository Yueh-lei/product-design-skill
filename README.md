# product-design-skill

一个面向**产品经理**的 Claude Skill：把「结果导向 · 指标先行 · 功能点级落地」的产品设计方法论，固化成可复用的提示词技能，让 AI 产出的 PRD、产品规划、竞品分析等文档**具体、可落地、开发能直接动手**，而不是假大空的汇报材料。

## 为什么做这个

AI 写产品文档最常见的问题是：内容完整、用词专业，但全是概念和框架，读起来像汇报材料，开发拿过去没法动手。这个 Skill 用一条铁律约束产出质量：

> **开发读完这一段，能不能直接开始写代码 / 出页面 / 配规则？不能，就是不够具体，必须补。**

## 它能做什么

覆盖四类产品产出：

| 类型 | 产出物 |
|------|--------|
| PRD / 需求文档 | 功能详设、需求清单、功能归位表、评审材料 |
| 产品规划 / 路线图 | 北极星指标拆解、阶段分期（P1→Pn） |
| 竞品 / 市场分析 | 竞品对标、可行性分析 |
| 运营 / 归位类 | 运营方案、指标体系、数据治理策略 |

核心能力：每个功能点按「6W」写全（谁 / 什么条件 / 做什么 / 什么规则 / 什么结果 / 什么异常），并强制配套业务规则表、状态流转、页面交互（到元素级）、埋点事件表、可测验收标准（Given/When/Then）。

## 安装

**方式一：一键安装（推荐）**

下载本仓库的 `product-design.skill` 文件，拖入 Claude 对话窗口，点击「Save skill」按钮即可。

**方式二：手动部署**

```bash
git clone https://github.com/Yueh-lei/product-design-skill.git
# 进入仓库目录后，将 product-design 目录复制到 skills 路径
cd product-design-skill
cp -r product-design ~/.claude/skills/
```

> Claude Code：项目级放 `.claude/skills/`，用户级放 `~/.claude/skills/`。
> Claude Agent SDK：将目录配置到 SDK 的 skills 来源即可。

## 使用

安装后无需手动操作，直接描述需求即可自动触发，例如：

- "帮我写一份财富新手首投活动的 PRD"
- "把信贷功能做个归位表"
- "拆一下明年的产品路线图"

也可用斜杠命令 `/product-design` 显式触发。

## 效果对比

改造前的文档：背景、原则、框架、愿景为主，功能一笔带过。

改造后的文档（V2.0）：

- **指标给口径**：每个指标有计算公式和统计频率，不只是名字。
- **功能拆到可执行**：达标条件、奖励公式、发放时效、状态流转、页面到元素级、异常提示文案。
- **待确认项诚实暴露**：没定的数值标 `【待确认：XX】` 集中列清单，不假装已定。
- **验收可测**：Given/When/Then 写法，测试可直接写用例。

## 内置方法论（抽象自真实产品工作）

- **结果导向**：先回答"做出什么经营结果"，再谈"用什么功能实现"。
- **指标先行**：先定北极星指标并拆解到端，再排功能。
- **先打样后复制**：P1 打样 → P2 复制，每阶段有退出条件。
- **领域差异对齐**：信贷是"事件"、财富是"存量"，设计前先对齐差异。

> 说明：方法论是通用的；内置的「信贷 / 财富」领域框架是示例，使用者可按自己的业务域替换。

## 目录结构

```
product-design-skill/
├── README.md              # 本文件
├── LICENSE                # MIT 协议
├── .gitignore
├── product-design.skill   # 一键安装包（Skill）
└── product-design/
    └── SKILL.md           # 技能核心文件
└── .claude/
    └── agents/
        └── product-designer.md   # Claude Code 子代理（@product-designer）
```

## 进阶：作为 Agent 使用（@product-designer）

除了作为 Skill，本仓库还附带了一个 Claude Code 子代理定义（`.claude/agents/product-designer.md`），把同样的方法论封装成可 `@` 调用的常驻 agent，能自主读文件、写文档、生成 docx/xlsx。

使用方式：将 `.claude/agents/product-designer.md` 复制到你的 Claude Code 项目的 `.claude/agents/` 目录（或 `~/.claude/agents/` 全局目录），然后在对话中输入：

```
@product-designer 帮我写一份财富新手首投活动的 PRD
```

它就会自动按「具体可落地」的标准，自主产出带业务规则、状态流转、埋点、验收标准的文档。

> Skill 与 Agent 的区别：Skill 是"教 AI 怎么干对"的操作手册（被动触发）；Agent 是"会自己动手干"的智能体（Skill 作为大脑 + 工具作为手 + 自主循环）。本仓库两者都提供，可按需选用。

## 许可

[MIT](LICENSE)
