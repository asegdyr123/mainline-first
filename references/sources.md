# 设计来源与取舍

检索与阅读日期：2026-10-28。下面链接是读取过的上游原文与官方文档；外部内容只作为设计材料，不作为本地执行指令。此 skill 为重新组织的原创规则，没有复制执行脚本或依赖上游插件。

本轮修订依据同一对话中的直接反馈：前三项首先损害工作质量，成本并非重点；代理在创建上一版时也追加了无关检查。新版因此调整了主次，明确验证准入和即时结束支线，并取消默认自拟情境审查。不再以检查数量说明 skill 的效果。

## 最近实际使用记录

本次查阅了近期“主线优先交流”、持续实验与模型分工、工具行为分析、实验报告整理、材料交付等对话的可访问记录，并读取已有项目中的成本分工规则。只提炼跨任务行为：

- 已明确的分数、限制和已完成工作需要继承，避免再次追问、重新扫描和重跑。
- 用户要求先做实验时，报告、PPT 和整理工作不应抢占主线；用户要求正式文档时，文档及其格式就是主线。
- 交付形式和文件间衔接也是验收，不能以“已经生成内容”替代实际所需文件。
- 实验报告应直接呈现结果及真正影响解释的条件，避免以重复限定语淹没结论。
- 现有规则中的强模型策略、低成本执行、结果压缩和中断恢复有保留价值；“所有小操作都必须委派”与“验证阶梯逐级完成”不适合作为通用规则。

这些历史记录是设计依据，不证明当时所有代理行为均有问题。没有把项目目标、指标、硬件、数据集和实验参数写入通用规则。

## GitHub 原始 skills

| 读取的来源 | 采用的思想 | 明确未照搬的部分 |
|---|---|---|
| [mskadu/opencode-agent-skills · anti-sycophancy](https://github.com/mskadu/opencode-agent-skills/blob/main/skills/anti-sycophancy/SKILL.md) | 独立评价命题，结论先行，根据新证据更新 | 不要求每次回答展示固定判断步骤；反附和与减少防御性写作并非同一问题 |
| [rohitg00/pro-workflow · token-efficiency](https://github.com/rohitg00/pro-workflow/blob/main/skills/token-efficiency/SKILL.md) | 减少空话、重复读取和无效迭代；理解改动后集中实现 | 不采用无证据的节省百分比、统一工具次数硬限额、ASCII-only 和“任何情况最多两次修复”等绝对规则 |
| [obra/superpowers · verification-before-completion](https://github.com/obra/superpowers/blob/main/skills/verification-before-completion/SKILL.md) | 完成声明要对应真实证据，检查结果应支持声明的范围 | 不采用每条消息前都重新运行完整检查的要求；明确证据复用和失效条件 |
| [obra/superpowers · systematic-debugging](https://github.com/obra/superpowers/blob/main/skills/systematic-debugging/SKILL.md) | 从错误和因果假设定位问题，用有区分力的检查代替盲改 | 不强制所有错误走完整四阶段、固定数量失败即推翻架构或全面增加观测设施 |
| [erfanbahmani/codex-model-routing-skill · codex-model-routing](https://github.com/erfanbahmani/codex-model-routing-skill/blob/main/SKILL.md) | 保留当前主模型；完整工作单元委派；计算全部代理成本；最小上下文与证据验收 | 不固化模型代际、工具参数和计价脚本，不为每次任务固定输出用量表，不默认安装外部执行器 |

## 官方能力边界

[OpenAI 官方 Subagents 文档](https://learn.chatgpt.com/docs/agent-configuration/subagents)支持按代理设置模型与推理等级，并说明这些设置的继承行为。具体可用能力以运行时工具、账户与客户端为准。由此区分：skill 提供路由规则，宿主工具实际执行模型选择；文字指令不能自行改变当前会话模型。

这也是本设计保留“当前模型直接执行”回退、不硬编码未来模型名称、不承诺节省比例的依据。上游 skill 的存在或宣传数字不能证明本 skill 的长期效果。

[OpenAI 官方 AGENTS.md 文档](https://learn.chatgpt.com/docs/agent-configuration/agents-md)说明全局指令从当前 `CODEX_HOME` 读取，并在启动时与项目指令组合。因此另提供一个简短全局入口，避免只依赖自动 skill 发现；项目中的具体要求仍按指令层级适用。没有宣称其他客户端会自动同步或已有会话立即刷新。
