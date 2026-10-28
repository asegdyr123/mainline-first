# Mainline First｜主线交付与工作质量

用于改善 AI 在持续任务中的判断和交付质量，适用于代码、研究、分析、写作与文档工作。

优先解决三个问题：

- **防御性写作**：先形成有依据的判断，再直接表达；限制条件只在影响结论处说明。
- **无意义验证**：默认推进主任务，新增检查需要具体依据；不以测试数量和自拟情境证明工作质量。
- **细节偏航**：信息足够作决定时及时结束支线，把工作推进到用户需要的结果。

模型与成本分工是辅助安排。必要的正确性验证、研究试验和复杂推理仍应完成。

## 名称与入口

仓库名保留 `mainline-first`。新版 skill 的内部名称为 **`mainline-execution`**，本地安装目录与调用名称使用这个名字。旧版的 `$mainline-first` 调用应迁移到新版；本地只保留需要使用的一份版本。

核心指令见 [SKILL.md](SKILL.md)。参考文件按需加载，不是所有任务都要执行的流程。

## 在 Codex 中安装

对 Codex 说：

```text
$skill-installer
从 https://github.com/asegdyr123/mainline-first 安装 skill。
仓库根目录就是 skill，安装名称使用 mainline-execution。
```

也可以手动将本仓库的 `SKILL.md`、`agents/` 和 `references/` 放入当前 Codex 用户环境的 `skills/mainline-execution/`。使用自定义 `CODEX_HOME` 时，以该环境的位置为准。

## 调用

在任务前明确加入：

```text
$mainline-execution
继续完成当前任务。
```

出现偏航时可以直接说：

```text
回到主线，停止不能改变判断的重复验证，继续完成交付。
```

Codex 也可根据 skill 描述自动选择它。需要长期默认应用时，在当前 Codex 用户目录的 `AGENTS.md` 中加入：

```markdown
持续工作应用 $mainline-execution；读取当前 Codex 用户目录下的 skills/mainline-execution/SKILL.md，同一上下文只需加载一次。简单请求直接完成。
优先保证有依据的直接判断、实质交付和主线推进。新增验证需要具体依据；已有信息足够就作决定并继续。模型分工仅作辅助。
```

仅安装 skill 不等于每次都会自动加载。全局入口负责长期提醒；项目具体要求继续适用。

## 更新

在仓库副本执行 `git pull --ff-only`，再将更新后的 skill 内容同步到本地安装目录。不要用旧副本覆盖正在进行的本地修改。GitHub 内容与本地安装不会自动互相同步。

如果更新尚未显示，重新启动 Codex。

## 在普通聊天中使用

让能够读取 GitHub 的助手读取本仓库 `SKILL.md`，并按需要读取其引用文件，再用于当前任务。只发送链接不代表已经安装，也不会自动应用到所有未来对话。

## 文件

- `SKILL.md`：核心规则。
- `agents/openai.yaml`：显示名称与调用设置。
- `references/verification.md`：仅在验证范围难以判断时读取。
- `references/model-routing.md`：仅在实际需要模型分工时读取。
- `references/calibration.md`：依据真实偏差修订规则的方法。
- `references/sources.md`：设计来源与取舍。
- `examples/`、`tests/`：初版保留的参考资料，不是默认必跑的验收流程。

[Codex 官方 skills 使用说明](https://learn.chatgpt.com/docs/build-skills)
