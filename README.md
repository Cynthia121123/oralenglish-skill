# oralenglish-skill

英语专四（TEM-4）口语思辨陪练 Skill：AI 以一轮一轮的方式陪练口语思辨表达，先给出英文思辨话题与一正一反两句参考句型，用户口头作答后，AI 原样转写、给出唯一一版口语化优化句并简短点评，支持同一话题下的深度追问与重答循环。

## 项目解决什么问题

- 专四口语考的是"能开口、有观点、说得清"，但多数人缺少能即时反馈的陪练：自己练不知道哪里是中式英语、怎么说更地道。
- 常见口语问题（中文直译语序、中式搭配、逻辑断层、母语负迁移）需要逐句诊断，而不是笼统的"多练多说"。
- 本 Skill 提供"出题 → 作答 → 转写/优化/点评 → 追问或重答"的闭环训练，每次反馈都点明具体问题，帮用户逐步减少中式英语、提升口语思辨表达。

## 主要功能

- **逐轮思辨出题**：每轮给出 1 个英文思辨话题（教育、科技、环保、社会、文化、生活方式等），并附 2 句纯英文参考句型——一句肯定立场（Affirmative）、一句否定立场（Negative），可套用、可模仿。
- **原样转写**：【我的原句】逐字保留用户口述内容，不做任何纠正。
- **口语化优化**：【优化句】仅生成 1 版适配专四口语的改写，优先修正中式英语（中文直译语序、中式搭配、逻辑断层、母语负迁移），拒绝浅层同义词替换；改动的核心内容加粗；句子简短、连接自然，不过度书面化。
- **简短点评**：点明本次中式英语问题，并从逻辑、句式、用词地道度三方面简要评价。
- **训练循环**：反馈后给出【继续】【重新回答】两个选项：
  - 【继续】：在当前话题下深度追问（新的子问题/更具体角度），开启新一轮；
  - 【重新回答】：不换话题，重新作答并重新反馈，循环直到【继续】。
- **纯对话式**：不支持网页抓取、PDF、图形界面。

## 安装方法

本 Skill 是供 AI 智能体（Agent）加载的技能包，不是独立程序，无需编译、无需第三方依赖。

1. 将 `oralenglish-skill/` 目录复制到你的 Agent Skill 根目录，例如：
   - `workspace/.user_skills/oralenglish-skill/`（豆包/通用 Agent 工作区）
   - 或平台规定的其他 skill 根目录（`<skill_root>/oralenglish-skill/`）
2. 保持目录结构完整：

   ```
   oralenglish-skill/
   ├── SKILL.md             # 技能主文件（流程规则与示例）
   └── agents/
       └── openai.yaml      # Agent 接口配置
   ```

3. 重启/刷新 Agent，使其发现新 Skill（按所用平台的技能加载方式）。

> 校验：可用官方 skill-creator-for-work 的 `quick_validate.py` 检查结构：
> `python quick_validate.py <skill_root>/oralenglish-skill`（需 PyYAML）。

## 使用方法

1. 对 AI 说"开始专四口语思辨训练"（或"开始练口语"）即可开始。
2. 每轮：
   - AI 先给出 **Topic** 与 **Affirmative / Negative** 两句参考句型，等待你作答；
   - 你口头作答后，AI 依次输出【我的原句】【优化句】【简短点评】，并给出两个选项；
   - 回复【重新回答】：不换话题重答，AI 重新反馈（可多次，直到你满意）；
   - 回复【继续】：AI 在当前话题下深度追问并给出新的参考句型，开启新一轮。
3. 训练话题会逐步加深（例如"大学是否该免费"→"免费的钱从哪来"→"文凭是否贬值"）。
4. 回复其他内容时，AI 会提示只需回复【继续】或【重新回答】。

## 输入输出示例

**用户**：开始专四口语思辨训练

**AI 出题**：

> **Topic:** Should university education be free for everyone?
>
> **Affirmative:** I believe higher education should be free because it gives students from different family backgrounds an equal starting point.
>
> **Negative:** In my view, free university education would put a heavy financial burden on the government and may lower the value of a degree.

**用户作答**：

> I think free university education is good for poor students. Because if the university is free, more people can go to it. The society also can get more talent people.

**AI 反馈**：

> ①【我的原句】
> I think free university education is good for poor students. Because if the university is free, more people can go to it. The society also can get more talent people.
>
> ②【优化句】
> I think free university education benefits students from poor families, because it allows more people to receive higher education. **In the long run, this also provides society with more skilled workers.**
>
> ③【简短点评】
> 本次主要是中式英语问题：一是 "get more talent people" 属中文直译搭配，英文不说 talent people，应说 skilled workers / talented graduates；二是 "Because..." 单独成句造成逻辑断层。逻辑上"观点→原因→延伸"链条完整，但缺少衔接；句式偏简单直白，结构略显单调；用词整体口语自然，除 talent people 这一搭配外问题不大。
>
> 请回复【继续】进入当前话题的深度追问，或【重新回答】重答本题。

**用户**：继续

**AI（深度追问，同一话题更具体角度）**：

> 你刚才支持免费大学教育，那么——
>
> **Topic:** If university education became free, where should the money come from — higher taxes or cuts in other spending?
>
> **Affirmative:** I think the government should raise taxes slightly, because education is a long-term investment that benefits the whole society.
>
> **Negative:** I would rather the government cut spending elsewhere, because higher taxes would put more pressure on ordinary families.

**用户**：重新回答（重答上题，不换话题）

**AI**：等待并接收新的作答后，重新输出【我的原句】【优化句】【简短点评】与两个选项，循环直到用户回复【继续】。
