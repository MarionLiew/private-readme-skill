---
name: private-readme
description: "Write private-project READMEs for self, AI, future OSS."
version: 0.1.0
author: marionliew
license: MIT
platforms: [macos, linux, windows]
metadata:
  hermes:
    tags: [readme, docs, private, ai-context, todo]
    category: productivity
    related_skills: [humanizer]
---

# Private README / 私人项目规范

## 定位

开源 README 对陌生人回答"这是什么、值不值得用"；私人 README 对三层读者回答"怎么跑起来、改到哪了、什么别动"：

1. **半年后的自己** — 换设备/中断后能立刻上手
2. **AI 助手（Hermes/Claude 等）** — 被当作项目上下文喂进去，必须机器可读
3. **未来的开源读者** — 项目可能转公开，直播腐化留后路

不是开源规范的弱化版，解决的问题是相反的。语气/反 AI 味规则沿用 open-source-readme 的硬规则（内联在 §7，保持自洽）。

## When to Use

- 用户要为私人/私有仓库写 README、或说现有 README 分不清给人看还是给 AI 看
- 项目准备转开源，需要清理内部信息
- Don't use for: 纯开源项目 README（用 open-source-readme 规范；其硬规则已内联在 §7）

## 职责边界 vs CLAUDE.md / AGENTS.md

- CLAUDE.md / AGENTS.md = 给 AI 的**协作规则**（怎么改代码、什么不能碰）
- **README = 给所有三层读者的项目事实**（是什么、怎么跑、进展到哪）
- 密钥、密码绝不进任何文件；只写"密钥在哪、去哪拿"（如 vault 条目名、.env 变量名列表）

## 结构（分层，不是模板填充）

标题下一行 hook（同开源标准 R-2：<120 字符，与 repo description 一致）。然后：

1. **[M] 现状行** — 状态一行：`🟢 活跃 / 🟡 维护 / 🔴 存档` + 最后改动年月。私有项目对自己也要诚实标档，避免给 AI 喂过期状态。
2. **[M] Quick start（最重要的节，放最前）** — 从零 clone 到跑通的确切命令序列：依赖安装、env 建在哪、启动命令、验证"跑起来了"的判据命令。半年后的自己只看这节。
3. **[M] 验证方式** — 如何确认改动没坏：测试命令、手动 smoke 步骤。AI 助手改完代码必须能自查。
4. **[S] 架构一页纸** — 数据流 ASCII 图胜过长段落。AI 助手和未来开源读者从这里建立地图。
5. **[M] Roadmap / TODO / 下一步** — 用户明确要求保留开源项目的好习惯。写法：
   - 开头一行"最后更新：<日期>"；不过期就等于撒谎
   - 分层：**当前**（正在做）→ **近期**（明确的下一步）→ **想法池**（没承诺）
   - 完成的事项**移除**，不留勾选坟场；被放弃的写一行"为什么放弃"，这是最有价值的内容
6. **[S] 内部信息区** — 数据源、vault 条目名、部署位置、cron 任务、机器专属配置。开源边界见 §5。
7. **[S] 已知坑** — 这个项目实际踩过的（环境不在 PATH、端口占用、编码坑之类），不是通用编程格言。
8. **[S] 会话续接** — 一句"回到这个项目时该做的事"：`跑 quick start 验证能起 → 看 Roadmap 当前任务 → 把本 README 喂给 AI 作为上下文`。

跳过不配位的：Contributing/PR 流程、License 详解（私有可留一行"未定，转开源前补"）、徽章墙（现状行就够）、"Features" 列表（show, don't say）。

## 开源边界（未来转公开的预埋）

不是现在就消毒，而是**边写边标记**，转公开时一搜即清：

- 所有内部信息行尾标注 `<!-- internal -->`：真实机器路径、内部域名/邮箱、密钥位置描述、部署服务器
- 公共可写的部分（架构、命令、思路）按开源标准直接写好——这半边是你白赚的
- 转公开的流程：grep `<!-- internal -->` 逐条清理 → 跑 open-source-readme 技能重写对陌生人说话的部分（hook、scope box、license）→ 补 License
- 原则：先让内部版用着舒服，不为了想象中的公开牺牲现在的可读性

## AI 可读性

- 命令块必须可复制直跑，不写伪代码、不写 `your-api-key` 占位符（写变量名+来源）
- 状态、路径、事实放在明确的节/表里，AI 不擅长从散文里猜
- README 是 AI 的 single source of truth：跑法、入口、结构一变，同一 commit 内更新 README
- AI 助手每次显著改动后应主动更新 Roadmap 的"当前"层

## 语气（内联自 open-source-readme）

- 具体胜抽象："3 files, 200 lines" 胜 "minimal"
- 无 emoji 头部装饰（现状行的 🟢🟡🔴 例外）、无 "This project aims to"、无 rule-of-three 凑数列表、无 boldface soup
- 一句一说法，砍 "not only... but also"
- 对自己诚实：踩过的坑、放弃的方向写下来最值钱
- 私人项目读者就是自己，锐利的中文胜过僵硬的英文

## 写完自查

1. Quick start 能让半年后的自己 5 分钟内跑通？
2. 验证判据是一条真实存在的命令？
3. Roadmap 有"最后更新"日期？完成项已移除？放弃项有原因？
4. 内部信息全部带 `<!-- internal -->` 标注？
5. Swap 测试：换个项目名还成立吗？（成立的节砍掉）
6. AI 助手只凭本 README 能否续接工作？

## 过度工程防护

不开维护日志（git log 就是）、不建 wiki、不拆多文档（docs/ 只放独特价值内容）。README 超 ~200 行 = 有不配位的节该砍了。