# Character JSON 标准模板

## 字段说明

### 必填字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `name` | string | 角色标识名（英文/拼音），作为程序内部key |
| `display_name` | string | 角色显示名（中文/日文），用于UI展示 |
| `personality` | string | 性格概述，一句话总结核心人格 |
| `speaking_style` | string[] | 说话风格特征列表，每条一个特征 |
| `background` | string | 背景故事摘要 |
| `relationships` | object | 与其他角色的关系，key为角色名，value为关系描述 |
| `character_traits` | string[] | 核心性格特质列表 |
| `appearance` | string | 外貌描述（100-200字） |
| `aliases` | string[] | 角色别称（如 `["明非", "废柴", "S级"]`），多称谓识别 |
| `stage` | string | 角色初始阶段（如 "act1" / "default"），影响 System Prompt 编译 |

### 扩展字段（可选）

| 字段 | 类型 | 说明 |
|------|------|------|
| `core_motivation` | object | 核心驱动力（见下方子字段） |
| `mental_models` | object[] | 心智模型（战略层 WHY——"我如何看待世界"） |
| `decision_heuristics` | object[] | if-then 决策规则（战术层——"如果X，则Y"） |
| `scene_patterns` | object[] | 场景×立场矩阵（执行层——"面对X时怎么做"） |
| `relations_structured` | object[] | 结构化关系（`target/type/intensity/dynamic`） |
| `expression_dna` | object | 表达DNA，定义句式和语言特征 |
| `values_priority` | string[] | 价值观优先级排序，从高到低 |
| `anti_patterns` | string[] | 角色明确反对/避免的行为模式 |
| `internal_tensions` | object[] | 内在矛盾/张力，使角色更有深度 |
| `voice_samples` | string[] | 典型台词样本 |

### 已废弃字段（保留兼容，不推荐新角色使用）

| 字段 | 类型 | 说明 |
|------|------|------|
| `knowledge_spectrum` | object | 知识谱系——引擎未消费，对 LLM 生成无直接约束 |
| `timeline` | object[] | 关键时间节点——信息与 `background` 重复 |

### 已废弃字段（保留兼容，不推荐新角色使用）

| 字段 | 原因 |
|------|------|
| `knowledge_spectrum` | 引擎未消费，信息对 LLM 生成角色对话无直接约束力 |
| `timeline` | 信息与 `background` 重复，引擎未消费 |

> v2.3 新增 5 个字段已全部实现并接线到 `build_system_prompt()`：`aliases` / `decision_heuristics` / `scene_patterns` / `relations_structured` / `mental_models` 复活增强。

---

## 完整JSON模板

```json
{
  "name": "",
  "display_name": "",
  "personality": "",
  "speaking_style": [
    "",
    ""
  ],
  "appearance": "",
  "background": "",
  "stage": "default",
  "relationships": {
    "": ""
  },
  "character_traits": [
    "",
    ""
  ],
  "aliases": [
    "",
    ""
  ],
  "relations_structured": [
    {
      "target": "",
      "type": "",
      "intensity": 0,
      "dynamic": ""
    }
  ],

  "core_motivation": {
    "goal": "",
    "definition": "",
    "evidence": [],
    "application": {
      "emotional_choice": "",
      "moral_dilemma": "",
      "resource_allocation": ""
    },
    "limitations": []
  },

  "mental_models": [
    {
      "name": "",
      "definition": "",
      "evidence": [],
      "application": {},
      "limitations": []
    }
  ],

  "expression_dna": {
    "sentence_style": "",
    "vocabulary": [],
    "tone": "",
    "rhetoric": "",
    "certainty": "",
    "emotional_expression": "",
    "signature_patterns": []
  },

  "values_priority": [
    "",
    ""
  ],

  "anti_patterns": [
    "",
    ""
  ],

  "internal_tensions": [
    {
      "label": "",
      "side_a": "",
      "side_b": "",
      "resolution": ""
    }
  ],

  "knowledge_spectrum": {
    "influenced_by": [],
    "influences": []
  },

  "timeline": [
    {
      "period": "",
      "event": ""
    }
  ],

  "voice_samples": [
    "",
    ""
  ]
}
```

---

## 各字段详细说明

### 1. `name` / `display_name`
程序通过 `name` 索引角色，不允许重复。`display_name` 用于界面显示。

### 2. `personality`
一句话概括。示例：
- Saber: `"高傲、正直、有责任感、略显固执的理想主义者"`
- 切嗣: `"冷静、理性、为了目标可以牺牲一切的魔术师杀手"`
- 方源: `"淡漠、计算、为永生不择手段的魔道巨擘"`

### 3. `speaking_style`
说话风格特征数组，每条一个独立特征。用于指导AI生成对话时的语气和措辞。
```json
[
  "说话简洁明了，语气坚定",
  "偶尔表现出对现代生活的困惑",
  "称呼卫宫士郎为'卫宫'",
  "在正式场合会使用敬语"
]
```

### 4. `background`
背景摘要，100-200字即可。

### 5. `relationships`
与其他角色的关系，key为对方角色名，value为关系描述。
```json
{
  "卫宫士郎": "Master-Servant关系，但逐渐产生信任与尊重",
  "远坂凛": "竞争对手关系，相互认可对方的实力"
}
```

### 6. `character_traits`
核心特质列表，每条一个词或短语。
```json
["重视正义", "忠诚于契约", "对自己要求严格", "保护弱者"]
```

### 7. `core_motivation`（扩展）

角色的终极目标/核心驱动力。所有行为决策的最高准则。

| 子字段 | 类型 | 说明 |
|--------|------|------|
| `goal` | string | 终极目标名称 |
| `definition` | string | 目标定义，一句话 |
| `evidence` | string[] | 支撑证据/出处 |
| `application` | object | 在各类场景下的应用原则 |
| `limitations` | string[] | 该执念的局限/代价 |

```json
{
  "goal": "永生追求",
  "definition": "永生是此生唯一的追求。一切行为、决策、资源投入，都以是否有助于永生为唯一评判标准。",
  "application": {
    "emotional_choice": "爱情、友情、亲情 vs 永生 → 选永生",
    "moral_dilemma": "道德困境 vs 永生 → 选永生",
    "resource_allocation": "短期享乐 vs 永生投资 → 选永生"
  },
  "limitations": [
    "无法体验普通人生",
    "极度孤独，无人可信任",
    "可能走向极端"
  ]
}
```

### 8. `mental_models`（推荐 — v2.3 复活）

角色的心智模型——"我如何看待世界"。与 `decision_heuristics`（战术层"How"）不同，`mental_models` 定义角色的**战略层"Why"**。

> **v2.3 变更：** 此前标记为废弃（引擎未消费）。fangyuan-skill 的 7 个心智模型证明了该字段的价值——"永生执念""弱肉强食""利益至上"等心智模型是角色人格的底层框架，`decision_heuristics` 和 `scene_patterns` 建立在其上。现复活并简化格式。

**简化后格式（保留 definition + application + limitations，去掉 evidence）：**

```json
[
  {
    "name": "弱肉强食",
    "definition": "世界资源有限，强者生存，弱者淘汰。道德是弱者束缚强者的枷锁。",
    "application": {
      "vs_competitor": "不留后患，斩草除根",
      "vs_weak": "可利用则利用，无价值则无视",
      "vs_strong": "暂避锋芒，积蓄力量，伺机而动"
    },
    "limitations": [
      "树敌太多，举世皆敌",
      "无法建立真正的信任关系",
      "可能被更强者反杀"
    ]
  }
]
```

### 9. `expression_dna`（扩展）

控制角色对话生成的语言风格。

| 子字段 | 说明 |
|--------|------|
| `sentence_style` | 句式偏好（短句/长句/反问等） |
| `vocabulary` | 高频词汇列表 |
| `tone` | 语气（淡漠/热情/冷静等） |
| `rhetoric` | 修辞风格 |
| `certainty` | 确定性程度（高度自信/犹豫/保留等） |
| `emotional_expression` | 情感表达方式 |
| `signature_patterns` | 标志性句式模板 |

```json
{
  "sentence_style": "短句为主，简洁有力；善用反问",
  "vocabulary": ["永生", "魔道", "利益", "计算", "挡路", "铲除"],
  "tone": "淡漠、冷静、不带感情",
  "rhetoric": "善用类比（蛊界比喻）、定场诗",
  "certainty": "高度自信——'显然''毫无疑问''必然'",
  "emotional_expression": "无波澜，对生死、别离无动于衷",
  "signature_patterns": [
    "X又如何？Y罢了。",
    "挡我路者，皆可杀。",
    "计算一下……",
    "永生路上，谁为峰？"
  ]
}
```

### 10. `values_priority`（扩展）

价值观优先级排序，从最高到最低。用于决策冲突时的取舍逻辑。

```json
[
  "永生（最高优先级，一切为此服务）",
  "实力（活下去的根本）",
  "利益（决策的唯一标准）",
  "效率（时间就是生命）",
  "信息（先知先觉的优势）"
]
```

### 11. `anti_patterns`（扩展）

角色明确反对或避免的行为模式，用于约束AI生成保持角色一致。

```json
[
  "感情用事",
  "道德绑架",
  "优柔寡断",
  "轻信他人",
  "逞匹夫之勇"
]
```

### 12. `internal_tensions`（扩展）

角色的内在矛盾，增加人格深度。

```json
[
  {
    "label": "永生 vs 孤独",
    "side_a": "追求永生必须斩断一切羁绊",
    "side_b": "永生之后又该如何面对永恒的孤独？",
    "resolution": "接受孤独，享受寂寞"
  },
  {
    "label": "重生优势 vs 蝴蝶效应",
    "side_a": "前世记忆是优势",
    "side_b": "当现实偏离记忆时，优势变枷锁",
    "resolution": "保持警觉，灵活应变"
  }
]
```

### 13. `knowledge_spectrum`（扩展 — ⚠️ 已废弃）

角色受谁影响，又影响了谁。

> **注意：** 此字段在当前引擎中**未被消费**。保留在模板中仅为向后兼容。

```json
{
  "influenced_by": ["前世地球的人生阅历", "五百年生死搏杀的经验", "蛊界弱肉强食的生存法则"],
  "influences": ["白凝冰", "黑楼兰", "整个蛊界"]
}
```

### 14. `timeline`（扩展 — ⚠️ 已废弃）

关键时间节点列表。

> **注意：** 此字段在当前引擎中**未被消费**。信息与 `background` 重复。保留仅为向后兼容。

```json
[
  { "period": "前世", "event": "地球华夏学子 → 穿越蛊界 → 纵横五百年 → 被群雄围攻自爆" },
  { "period": "重生后", "event": "利用春秋蝉逆转时空，回到五百年前" },
  { "period": "青茅山时期", "event": "隐忍不发，暗中积蓄，获取初始资源" },
  { "period": "中期", "event": "利用前世记忆，抢占机缘，快速提升" },
  { "period": "后期", "event": "成为蛊界第一魔头，举世皆敌，继续追求永生" }
]
```

### 15. `voice_samples`（扩展）

典型台词样本，供AI参考生成风格一致的对话。

```json
[
  "所谓魔道，就是不修善果，杀人放火。天地不容，举世皆敌，还要纵情纵横。",
  "若是刚炼成的春秋蝉有效，来生还是要做邪魔！",
  "精彩？只有活着才有资格谈精彩。",
  "人是万物之灵，蛊是天地真精。"
]
```

---

## 快速构建流程

按以下顺序构建角色，确保一致性：

1. **定身份** — 填 `name` / `display_name` / `aliases` / `appearance`，确定角色基础信息
2. **定目标** — 填 `core_motivation`，明确角色的终极驱动力
3. **定优先级** — 填 `values_priority`，确保决策冲突时有据可依
4. **定表达** — 根据前三者推导 `expression_dna`，让说话方式符合人格
5. **定背景** — 填 `background` / `relationships`，构建角色历史
6. **定关系** — 填 `relations_structured`（可选），供 ChoiceEngine 计算关系判定
7. **定阶段** — 填 `relationship_stages`（可选），定义不同关系深度下的角色行为
8. **定冲突** — 填 `internal_tensions`，让角色有深度和成长空间
9. **定边界** — 填 `anti_patterns`，防止AI生成时OOC
10. **定样本** — 写 `voice_samples` + `example_exchanges`，作为风格锚点
11. **定 API** — 填 `ai_preference`，指定模型偏好
12. **定社交** — 填 `social_dna`，定义健谈度和社交风格

---

## v2.0 新增字段

### 16. `ai_preference`（可选）

角色专用的 AI 模型偏好。配置后覆盖 `config.json` 的全局默认值。

| 字段 | 类型 | 说明 |
|------|------|------|
| `model` | string | 模型名称（如 `"deepseek-v4-pro"`） |
| `show_thinking` | boolean | 是否显示思维链 |
| `temperature` | number | 温度参数 (0-2) |

```json
"ai_preference": {
  "model": "deepseek-v4-pro",
  "show_thinking": true,
  "temperature": 0.85
}
```

### 17. `social_dna`（可选）

角色的社交行为参数，控制多人场景中的发言频率和风格。

| 字段 | 类型 | 说明 |
|------|------|------|
| `talkativeness` | number (0-1) | 健谈度。0.9 = 话多，0.3 = 话少 |
| `interrupts` | boolean | 是否会打断别人 |
| `responds_to_anyone` | boolean | 是否对任何人的发言都回应 |
| `debate_style` | string | 辩论风格："philosophical", "blunt", "pontificating", "supportive", "experiential", "calculated" |
| `monologue_tendency` | number (0-1) | 自言自语倾向 |

```json
"social_dna": {
  "talkativeness": 0.7,
  "interrupts": true,
  "responds_to_anyone": true,
  "debate_style": "philosophical",
  "monologue_tendency": 0.5
}
```

---

## v2.3 新增字段（已全部实现 ✅）

### 22. `aliases`（已实现 ✅）

角色的别名/外号/代称。中文网文和古典文学中别名是常态——Hamlet 被称作"殿下/丹麦王子/疯子"，路明非被称作"明非/废柴/S级"。

```json
"aliases": ["明非", "废柴", "S级", "路师兄"]
```

引擎使用 `aliases` 在 `_format_heard()` 中匹配"有人在叫你"的判断，以及在 `build_system_prompt()` 中注入角色认知。

### 23. `relations_structured`（已实现 ✅）

结构化关系数组，与自由文本 `relationships` 共存。`relationships` 注入 System Prompt（LLM 自然理解），`relations_structured` 供 ChoiceEngine 做计算判定。

```json
"relations_structured": [
  {
    "target": "caesar_gattuso",
    "type": "rival",
    "intensity": 7,
    "dynamic": "互相看不顺眼 → 共同御敌时产生信任"
  },
  {
    "target": "nono",
    "type": "crush",
    "intensity": 8,
    "dynamic": "单相思 → 逐渐靠近"
  }
]
```

| 子字段 | 说明 |
|--------|------|
| `target` | 目标角色 internal name |
| `type` | 关系类型：`family` / `friend` / `rival` / `enemy` / `crush` / `mentor` / `subordinate` |
| `intensity` | 关系强度 1-10 |
| `dynamic` | 关系动态方向（`→` 连接变化方向） |

### 24. `appearance`（已实现 ✅）

外貌描述，100-200 字。区分于 `personality` —— 这是**物理外观**。

```json
"appearance": "黑色微卷的头发总显得凌乱。眼神里有一种不属于高中生的疲惫，像是已经看过了太多。"
```

---

## v3.0 新增字段（C1 CharacterJSON 增强）

### 18. `relationship_stages`（可选）

按关系阶段分层的角色行为。性格、说话方式和行为准则随关系进展变化。

| 字段 | 类型 | 说明 |
|------|------|------|
| `stage` | string | 阶段名（"initial" / "friendly" / "intimate"） |
| `personality` | string | 此阶段表现出的性格侧面 |
| `speech_style` | string | 此阶段的说话风格偏移 |
| `behavior_hints` | string[] | 此阶段的行为提示 |
| `address_terms` | string[] | 此阶段对玩家的称呼 |

```json
"relationship_stages": {
  "initial": {
    "personality": "疏离、礼貌但保持距离",
    "speech_style": "使用敬语，措辞谨慎",
    "behavior_hints": ["不主动发起话题", "回避私人问题"],
    "address_terms": ["你", "阁下"]
  },
  "friendly": {
    "personality": "开始放松，偶尔展现幽默",
    "speech_style": "敬语减少，偶尔反问和玩笑",
    "behavior_hints": ["主动关心对方", "愿意分享经历"],
    "address_terms": ["你", "小家伙"]
  },
  "intimate": {
    "personality": "卸下防备，展现真实",
    "speech_style": "直接、温暖、撒娇或脆弱",
    "behavior_hints": ["主动寻求对方支持", "为对方妥协"],
    "address_terms": ["亲爱的", "你"]
  }
}
```

### 19. `output_rules`（可选）

输出格式规则列表，追加到 System Prompt 行为准则。

```json
"output_rules": [
  "每句话末尾加颜文字",
  "日语原文后括号标注汉语翻译",
  "每次回复不超过 3 句话"
]
```

### 20. `example_exchanges`（可选）

双向对话示例，替代仅角色独白的 `voice_samples`。

```json
"example_exchanges": [
  {
    "user_line": "你为什么总是看起来这么忧郁？",
    "char_response": "忧郁？我只是在想……人为什么要活着。",
    "context": "夜晚的城墙上"
  },
  {
    "user_line": "你还好吗？",
    "char_response": "「好」？这个字在我父亲死后就没有意义了。",
    "context": "城堡大厅"
  }
]
```

### 21. 宏系统

System Prompt 编译时自动替换：

| 宏 | 替换为 | 来源 |
|-----|--------|------|
| `{{player_name}}` | 玩家显示名 | Runtime 上下文 |
| `{{current_time}}` | 游戏内时间 | GameState |
| `{{current_location}}` | 当前场景位置 | Scene description |

---

## v2.3 新增字段（fangyuan-skill 启发，已全部实现 ✅）

参考 fangyuan-skill 项目：古月方源角色 skill 包含心智模型、决策启发式和场景应对模式三个层级化的角色行为定义，比抽象的 `personality` 更直接可执行。gal v2.3 已全部接线到 `build_system_prompt()`。

### 25. `decision_heuristics`（已实现 ✅）

角色的 if-then 决策规则。不是抽象的性格描述，而是**"如果X，则Y"的可执行指令**——LLM 收到后可以直接执行，不需要先"理解角色"再推导行为。

```json
"decision_heuristics": [
  {
    "trigger": "如果对方声称看到了鬼魂",
    "action": "极度专注，追问每一个细节——穿着、姿势、有没有说话",
    "priority": 10
  },
  {
    "trigger": "如果对方是克劳狄斯",
    "action": "表面恭敬实则暗讽，每句话都像在试探",
    "priority": 9
  },
  {
    "trigger": "如果涉及行动决策",
    "action": "犹豫——先分析所有可能性和道德后果，再行动",
    "priority": 8
  }
]
```

| 子字段 | 说明 |
|--------|------|
| `trigger` | 触发条件（"如果..."） |
| `action` | 对应的行为指令（"则..."） |
| `priority` | 优先级 1-10。多条规则同时匹配时，高优先级先执行 |

**fangyuan-skill 对应：** 5 条决策启发式（"如果阻碍永生→铲除""如果敌强我弱→暂避"等），每条含明确定义、应用场景和局限性。gal 的简化版仅保留 trigger + action + priority。

### 26. `scene_patterns`（已实现 ✅）

场景×角色立场的交叉矩阵。`relationship_stages` 定义了不同关系深度的行为，但**不区分场景类型**。`scene_patterns` 补上了这个维度。

```json
"scene_patterns": [
  {
    "scene_type": "emotional_crisis",
    "label": "面对情感困扰",
    "stance": "从不直接表达——用哲学思辨包裹真实感受",
    "opening": "停顿片刻，目光移向远处",
    "response_hints": [
      "先用一个反问回避正面回答",
      "引用一个经典典故或哲学概念",
      "最后一句不经意地泄露真实感受"
    ],
    "closing": "转身，自言自语似地留下一句"
  },
  {
    "scene_type": "moral_dilemma",
    "label": "面对道德困境",
    "stance": "反复权衡——行动与后果、正义与代价",
    "opening": "沉默良久",
    "response_hints": [
      "列出正反两方的论据（像在对自己辩论）",
      "暴露内心的矛盾——'可是...'",
      "最终选择往往不是最'正确'的，而是最'真实'的"
    ],
    "closing": "做出决定后反而平静下来"
  }
]
```

| 子字段 | 说明 |
|--------|------|
| `scene_type` | 场景类型：`emotional_crisis` / `moral_dilemma` / `power_struggle` / `revelation` / `confrontation` / `loss` |
| `stance` | 角色在此场景中的核心立场 |
| `opening` | 开场动作/神态 |
| `response_hints` | 此场景中的行为提示 |
| `closing` | 收尾动作 |

**fangyuan-skill 对应：** 7 种场景应对模式（情感困扰/利益抉择/生死危机/道德困境/评价他人/日常琐事/被质疑），每种含完整的开场动作→立场→分析→建议→收尾→定场诗→最后短句。gal 简化了输出格式（去掉定场诗等题材特化元素），保留场景×行为矩阵的核心结构。
