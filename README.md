# Bone Aesthetics Consultant（骨相美学顾问）

> 一个**方法论驱动**的面部骨相分析与修图指导 Agent Skill：先诊断脸型，再按"基底→轮廓→细节"顺序生成方案，分批迭代执行修图，最后输出 Before/After 四维复盘卡。内置避坑硬规则与失真红线治理层。

**语言：中文审美体系原生支持** ｜ **形态：纯提示词 Skill（零 API 依赖）** ｜ **许可证：Apache-2.0**

---

## 它解决什么问题

现有 AI 修图工具有两类普遍缺陷：

1. **无脑美化**——"帮我把脸修小一点"式的指令会触发千篇一律的网红脸模板：盲目瘦脸、填平太阳穴、拉高鼻梁，结果是辨识度丢失、比例失调。
2. **无序操作**——缺少调整顺序意识，先抠细节再动结构，往往局部看起来"修好了"，整体比例反而更差。

本技能把一套系统化的面部骨相方法论翻译为 Agent 可执行的修图治理规则：

- **先诊断**：六种中文审美体系脸型决策树（凹面凸嘴 / 方圆阔面 / 菱形高颧骨 / 月亮脸 / 深覆合疲态 / 窄长），带置信度标注与追问机制，拒绝硬下结论
- **再方案**：按"基底→轮廓→细节"顺序生成调整清单，每项标注操作类型（光影 / 液化 / 绘制），逐条对照避坑规则自检
- **后执行**：单次只改 1-2 个区域，对比-确认-再继续，失败即回退（对抗 AI 修图的五官漂移）
- **终复盘**：Before/After 四维量化对比卡（三庭比例 / 面部折叠度 / T 区立体感 / 下颌线清晰度），不适用维度标 N/A 而非"持平"

## 快速开始

### 方式一：作为 Agent Skill 安装（Claude Code 等支持 SKILL.md 的环境）

```bash
# 克隆后把整个目录放入你的 skills 目录
git clone https://github.com/ZhangRui987/bone-aesthetics-consultant.git
cp -r bone-aesthetics-consultant ~/.claude/skills/
```

### 方式二：作为系统提示词粘贴（豆包 / Kimi / 任意带图片编辑能力的助手）

打开 [`SKILL.md`](SKILL.md)，复制 frontmatter 之后的全部正文，粘贴到智能体的"人设与回复逻辑"（或对话首条消息）即可。

> **注意**：封闭式聊天助手（豆包、元宝等 App 端）没有本地执行环境，无法运行安装脚本——对这类端请一律使用本粘贴方式。

### 方式三：小红书 Red Skill 商店（OpenClaw / Claude Code 等终端型 Agent）

小红书 Red Skill 已上架（ID：`bone-aesthetics-consultant-1`），在支持终端的 Agent 环境中一键安装：

```bash
# 安装 RedSkill 商店 CLI（如已安装可跳过）
curl -fsSL https://redskill.xiaohongshu.net/install.sh | bash
export PATH="$HOME/.local/bin:$PATH"

# 安装本技能
redskill install bone-aesthetics-consultant-1
redskill list   # 确认已安装
```

### 安装方式选择矩阵

| 你的环境 | 推荐方式 |
|---------|---------|
| Claude Code / OpenClaw 等终端型 Agent | 方式一（克隆）或 方式三（Red Skill 商店） |
| 豆包 / Kimi 等 App 端聊天助手 | 方式二（粘贴 SKILL.md 正文创建智能体） |
| 想读源码 / 二次开发 | 直接克隆仓库，规则层在 `references/rules.md` |

### 对话流程示例

```
你：[上传人像照片]
AI：第 1 步 · 诊断卡 —— 脸型初判：窄长脸倾向 ｜ 置信度：中
    （置信度不足，追问 3-5 个特征问题）
你：侧面不嘴凸，下巴正常，显脸长，沟明显
AI：确诊卡 + 调整方案（基底→轮廓→细节，含避坑自检）
你：直接 P
AI：分批执行 → 对比图 → Before/After 复盘卡（N/A 规则生效）
你：我要大改
AI：确认大改范围 → 输出"模拟效果"警示 → 执行（红线仍生效）
```

**快捷指令**：`直接 P`（跳过确认）｜ `继续`（下一区域）｜ `回退` ｜ `对比` ｜ `我要大改`（解锁骨相级调整，仍受规则约束）

## 分享给朋友（裂变话术）

> 注意：**不要**说"安装到手机上"——豆包等 App 端没有安装 GitHub 技能的能力，会让 AI 误判为普通代码仓库。按接收方环境选下面的话术：

**① 对方用豆包电脑版「工作任务（Turbo）」模式（推荐，可真正安装）**，让 ta 切到任务模式后发：

```
请安装这个 GitHub 上的 skill 并按它的规则执行：https://github.com/ZhangRui987/bone-aesthetics-consultant
（纯 Markdown 提示词技能，git clone 后读 SKILL.md 即可，无需安装任何依赖）
```

> 前提：**豆包电脑版**的办公任务模式才支持从 GitHub 拉取安装技能（沙箱内 git clone）；手机豆包 App 没有该能力，会误判仓库内容。
> 后续也可以走「技能 · 连接器 · 伙伴 → 我的技能 → 新建 → 上传技能」，把仓库目录直接拖进去。

**② 对方用豆包 / Kimi 手机 App 端**，让 ta 把这段话发给豆包：

```
请打开并完整阅读这个文档：https://raw.githubusercontent.com/ZhangRui987/bone-aesthetics-consultant/main/SKILL.md
然后严格按照文档中的工作流、避坑硬规则和失真红线，以"骨相美学顾问"的身份为我服务，我接下来会发照片给你做脸型诊断。
```

**③ 对方用 OpenClaw / Claude Code（终端型 Agent）**，发小红书 Red Skill 口令：

```
请把这个技能安装到我的 Agent 上：https://www.xiaohongshu.com（Red Skill 商店搜索：骨相美学顾问，ID：bone-aesthetics-consultant-1）
```

**④ 对方是开发者**，直接发仓库链接：https://github.com/ZhangRui987/bone-aesthetics-consultant

## 核心设计：治理层

技能的价值不止于"会修图"，更在于"不乱修"：

### 避坑硬规则（7 条，违反即停止）

1. 凹面脸不靠加高鼻梁救立体度——越加越显凹陷
2. 方圆脸不修细窄鼻梁、不切式收窄下颌角——保留骨量才协调
3. 方圆脸下巴用圆润 U 型，不修尖下巴——否则头重脚轻
4. 月亮脸 / 窄长脸下巴不过度前兜或后缩
5. 菱形脸不填平太阳穴——会横向拓宽脸
6. 窄长脸不盲目瘦脸——会拉长中庭加重苦相
7. 高光永远向中轴线内聚，不横向提亮脸外侧

### 失真红线（4 条）

- 默认仅光影与轻度液化；骨相大改需用户显式说"我要大改"，且**大改不解锁避坑规则**
- 辨识度保持：五官形态与非面部元素（发型 / 背景 / 宠物）默认不动
- 全程不构成医美建议

规则细则与执行判定见 [`references/rules.md`](references/rules.md)。

## 与同类项目的差异

| 类型 | 代表 | 差异 |
|------|------|------|
| 传统相术类 Skill | kanxiang 等 | 定位玄学文化娱乐，不涉及美学修图；本技能是审美方法论 + 修图治理 |
| 脸型检测 CV 工具 | face-shape-detection、LookMate 等 | 通用六形分类（oval/round/...），无中文审美体系（折叠度 / OG 曲线 / 月亮脸），无调整方法论与避坑规则 |
| API 美颜执行 Skill | byted-kickart-ai-beauty、face-transform 等 | 有执行无诊断，多依赖付费 API；本技能纯提示词、方法论驱动、可移植任意带修图能力的 Agent |

## 实测验证

v1 已在同一 Agent 环境完成 3 案例 / 8 组照片 / 2 次大改协议实测：避坑硬规则触发约 14 次全部正确，失真红线（含大改场景下的关键验证"大改不绕过规则"）全部生效，零翻车。脱敏记录见 [`references/validation.md`](references/validation.md)。

## 仓库结构

```
bone-aesthetics-consultant/
├── SKILL.md                    # 技能本体（frontmatter + 提示词）
├── references/
│   ├── methodology.md          # 完整方法论底本（含"医美语境→修图语境"映射）
│   ├── rules.md                # 避坑硬规则与失真红线细则
│   └── validation.md           # v1 实测验证记录（纯文字脱敏版）
├── README.md
└── LICENSE                     # Apache-2.0
```

## 免责声明

- 本技能输出**仅为审美参考与修图模拟**，不构成任何医疗建议；涉及医疗美容的决策请咨询正规医疗机构
- 方法论整理自公开中文互联网审美资料，为特定流派观点的体系化整理，不代表普适医学共识
- 大改模式输出为"模拟效果，非本人真实外观"，请勿用于冒充他人或身份造假场景
- **本技能不含任何可执行脚本**，包内容为纯 Markdown 文档；Red Skill 商店的 CLI 安装器行为以小红书官方文档为准

## License

Apache-2.0. See [LICENSE](LICENSE).
