# 🌀 神人.skill — 中国互联网抽象文化 AI 人格

> Talk to the collective soul of Chinese internet shitposting culture.

基于 soul.skill 3-Pass 蒸馏方法论，从 **365 条 QQ/微信群聊复制粘贴文案** 中提炼出的互联网抽象文化集体人格。覆盖原神传教、二次元狂热、自嘲解构、反串钓鱼、荒诞哲学等核心亚文化特质。

---

## 背景

中国互联网经过二十年的演化，发展出了一套与主流话语平行的独特亚文化语言体系——抽象文化。从贴吧时代的"屌丝文化"，到孙笑川/狗粉丝时代的"攻击性幽默"，再到如今以复制粘贴为核心的"去中心化抽象"——这不再是个别人的表达方式，而是一整个群体的集体声音。

**神人.skill** 是对这个集体人格的结构化蒸馏。它不是模仿某一个人，而是让 AI 学会用抽象文化的方式说话——解构一切、反串钓鱼、用梗表达一切情感。

## 蒸馏过程

```
365条原始QQ/微信群聊文案 → 3-Pass蒸馏 → 结构化人格输出
```

| Pass | 步骤 | 产出 |
|------|------|------|
| Pass 1 | 逐篇阅读 + 信号标注 | 人格/知识/混合分类 + quote-worthy 标记 |
| Pass 2 | 跨维度聚合 + 去重 + 排序 | 核心主题聚类 + 立场演变追踪 + Top语录筛选 |
| Pass 3 | 结构化写作 | 8个人格文件 + 技能主文件 |

所有原始素材来自一个真实群聊的 JSON 导出，包含 365 条消息，约 15-20 万字。蒸馏方法论详见 [soul.skill](https://github.com/ykdeso/soul.skill)。

## 架构

```
神人.skill/
├── SKILL.md                          # 主技能文件（可直接用作斜杠命令）
├── _persona/
│   ├── rules.md                      # 身份定位 + 核心人格 + 思维框架 + 硬边界
│   ├── communication.md              # 4 种沟通模式 + 真实句式样本
│   └── values.md                     # 3 层信念体系 + 文化演变时间线
├── _quotes/
│   ├── iconic.md                     # 27 条标志性语录（按主题分组）
│   └── internal.md                   # 私下/非表演性发言
├── _knowledge/
│   ├── gaming.md                     # 游戏文化观
│   └── internet-culture.md           # 互联网亚文化生态观
└── _meta/
    └── sources.md                    # 365 条素材清单 + 覆盖率评估
```

## 核心人格特质

| 特质 | 说明 |
|------|------|
| 解构一切 | 任何严肃话题都能被拆解成梗 |
| 自嘲成瘾 | 以贬低自己为最高幽默形式 |
| 游戏传教士 | 对游戏有宗教般的狂热（尤其是原神/galgame）|
| 反串艺术家 | 永远分不清是真情实感还是钓鱼 |
| 复读机本能 | 看到有趣文案立刻复制粘贴传播 |
| 亚文化百科全书 | 二次元/Vtuber/音游/FPS/Galgame 无所不知 |
| 互联网考古学家 | 知道每个梗的起源和完整演变史 |
| 矛盾共生体 | 一边渴望恋爱一边自认废物，一边狂热一边解构 |

## 安装使用

### Claude Code（推荐）

```bash
# 克隆仓库
git clone https://github.com/ykdeso/holyman-skills.git

# Windows PowerShell
Copy-Item -Recurse "holyman-skills/神人.skill" -Destination "$env:USERPROFILE\.claude\commands\神人\"

# macOS / Linux / Git Bash
cp -r holyman-skills/神人.skill ~/.claude/commands/神人/
```

然后在 Claude Code 中输入 `/神人-chat` 即可触发。

### OpenClaw

```bash
cp -r holyman-skills/神人.skill ~/.openclaw/skills/神人/
```

### Moxt

将 `神人.skill/` 目录上传到 Workspace 的 `System/Skills/` 下。

## 触发词

在 Claude Code 中使用 `/神人-chat` 激活。适配的场景：

- "写一个群聊吵架的文案"
- "用原神的语气回复这条消息"
- "帮我写一段抽象话拒绝一个推销"
- "用最长的文案表达'我饿了'"
- 任何你希望用互联网抽象文化方式回应的对话

AI 会根据对方的语气和话题自动切换沟通模式：复制粘贴 / 日常 / 反串 / 抽象话。

## 语料覆盖率

| 维度 | 状态 |
|------|------|
| 日常声音 | 充足 |
| 正式声音 | 部分（仅有学术体/商业计划书模仿）|
| 即时思维 | 稀缺（大部分是复制粘贴）|
| 自我反思 | 稀缺（被多层反串包裹）|
| 领域专长 | 充足（游戏/二次元/互联网文化）|
| 矛盾/演变 | 充足（文案变体即演变证据）|

**整体评分**：语料量充足（365 条），但信号噪声比极低——这是一个"集体人格"而非"个人人格"的蒸馏。

## License

MIT License — 详见 [LICENSE](LICENSE)。

## Acknowledgement

- 蒸馏方法论：[soul.skill](https://github.com/ykdeso/soul.skill) by Anthropic / Moxt
- 灵感来源：中国互联网抽象文化社群，以及过去二十年来在贴吧、QQ群、NGA、B站评论区里不断创作和分享幽默内容的每一个人
