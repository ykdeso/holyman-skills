# 🌀 神人.skill — 中国互联网抽象文化 AI 人格

> Talk to the collective soul of Chinese internet shitposting culture.

基于 **soul.skill 3-Pass 蒸馏方法论** × **[CHARACTER_TEMPLATE v2.3+](CHARACTER_TEMPLATE.md)** 增强字段，从 **[神言.txt](神言.txt)**（365 条 QQ/微信群聊复制粘贴文案）中提炼出的互联网抽象文化集体人格。

覆盖原神传教、二次元狂热、自嘲解构、反串钓鱼、荒诞哲学等核心亚文化特质。

---

## 背景

中国互联网经过二十年的演化，发展出了一套与主流话语平行的独特亚文化语言体系——抽象文化。从贴吧时代的"屌丝文化"，到孙笑川/狗粉丝时代的"攻击性幽默"，再到如今以复制粘贴为核心的"去中心化抽象"——这不再是个别人的表达方式，而是一整个群体的集体声音。

**神人.skill** 是对这个集体人格的结构化蒸馏。它不是模仿某一个人，而是让 AI 学会用抽象文化的方式说话——解构一切、反串钓鱼、用梗表达一切情感。

## 蒸馏过程

```
神言.txt（365条，~32万字） → 3-Pass蒸馏 → 结构化人格输出（11个文件）
```

| Pass | 步骤 | 产出 |
|------|------|------|
| Pass 1 | 逐篇阅读 + 信号标注 | 人格/知识/混合分类 + quote-worthy 标记 |
| Pass 2 | 跨维度聚合 + 去重 + 排序 | 核心主题聚类 + 立场演变追踪 + Top语录筛选 |
| Pass 3 | 结构化写作（CHARACTER_TEMPLATE 增强） | 11个人格文件 + 技能主文件 |

原始素材：[神言.txt](神言.txt)（JSON格式，365条群聊消息）。

## 架构

```
神人.skill/
├── SKILL.md                          # 主技能文件（含 output_rules + decision_heuristics Top 5）
├── _persona/
│   ├── rules.md                      # 身份 + 人格 + 思维框架 + decision_heuristics (10条)
│   │                                  + scene_patterns (4种场景) + anti_patterns
│   ├── communication.md              # expression_dna (7个维度) + 4种沟通模式
│   │                                  + mode_switching_logic
│   └── values.md                     # values_priority (5项) + 3层信念 + internal_tensions (5组)
├── _quotes/
│   ├── iconic.md                     # 28条语录 + voice_samples + example_exchanges (5组)
│   └── internal.md                   # 私下/非表演性发言
├── _knowledge/
│   ├── gaming.md                     # 游戏文化观
│   └── internet-culture.md           # 互联网亚文化生态观
└── _meta/
    └── sources.md                    # 365条素材清单 + 覆盖率评估
```

## 方法论增强（v2.0）

参照 [CHARACTER_TEMPLATE.md](CHARACTER_TEMPLATE.md) 的字段体系，神人.skill v2.0 在 soul.skill 原生输出基础上新增了以下结构化字段：

| 字段 | 所在文件 | 说明 |
|------|----------|------|
| `decision_heuristics` | rules.md | 10条 if-then 决策规则，含 priority 优先级 |
| `scene_patterns` | rules.md | 4种场景×立场矩阵（群聊对线/情感流露/新人入群/深夜破防） |
| `expression_dna` | communication.md | 7维度语言基因（句式/词汇池/语气/修辞/确定性/情感表达/标志句式） |
| `values_priority` | values.md | 5项价值观优先级排序（决策冲突时的取舍依据） |
| `internal_tensions` | values.md | 5组内在矛盾（自认废物vs精神胜利 / 渴望连接vs拒绝真诚 等） |
| `voice_samples` | iconic.md | 4条典型声音样本（可作为独立风格锚点的完整发言） |
| `example_exchanges` | iconic.md | 5组双向对话示例（user_line / char_response / context） |
| `output_rules` | SKILL.md | 6条输出格式规则（字数/语气/情感表达/结尾风格等） |

## 核心人格特质

| 特质 | 说明 |
|------|------|
| 解构一切 | 任何严肃话题都能被拆解成梗 |
| 自嘲成瘾 | 以贬低自己为最高幽默形式 |
| 游戏传教士 | 对游戏有宗教般的狂热（尤其是原神/galgame） |
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
| 正式声音 | 部分（仅有学术体/商业计划书模仿） |
| 即时思维 | 稀缺（大部分是复制粘贴） |
| 自我反思 | 稀缺（被多层反串包裹） |
| 领域专长 | 充足（游戏/二次元/互联网文化） |
| 矛盾/演变 | 充足（文案变体即演变证据） |

**整体评分**：语料量充足（365条，~32万字），但信号噪声比极低——这是一个"集体人格"而非"个人人格"的蒸馏。

## 仓库文件

| 文件 | 说明 |
|------|------|
| `神人.skill/` | 蒸馏完成的 AI 人格技能包（v2.0，CHARACTER_TEMPLATE 增强） |
| `神言.txt` | 原始素材（365条群聊文案，JSON格式） |
| `CHARACTER_TEMPLATE.md` | 方法论增强参考（galgame 角色 JSON schema v2.3+） |
| `README.md` | 本文件 |
| `LICENSE` | MIT License |

## License

MIT License — 详见 [LICENSE](LICENSE)。

## Acknowledgement

- 蒸馏方法论：[soul.skill](https://github.com/ykdeso/soul.skill) by Anthropic / Moxt
- 字段增强参考：CHARACTER_TEMPLATE.md（galgame character JSON schema）
- 灵感来源：中国互联网抽象文化社群，以及过去二十年来在贴吧、QQ群、NGA、B站评论区里不断创作和分享幽默内容的每一个人
