# Coffee Work

Coffee Work 是一个面向 Hermes 的插件和可复用 skill，用来协调 Codex、Kimi Code、Claude Code、OpenCode、Gemini CLI 以及 tmux session 等本地 coding agent。

它的目标不是替代这些工具，而是让 Hermes 负责调度：选择合适的 backend、构造清晰的任务 prompt、监控执行过程、收集证据，并把命令、diff、产物、测试结果、失败点和剩余风险汇总回来。

[English](README.md)

## 安装

从当前仓库安装插件：

```bash
hermes plugins install https://github.com/Dcx-swjtu/Coffee-Work --enable
```

然后在 Hermes 里使用：

```text
/coffee-work 用 Codex 审查我当前的 diff。只读，不要改文件。重点看 bug、安全风险和缺失的测试。
```

如果只想安装 skill 文件：

```bash
hermes skills install https://raw.githubusercontent.com/Dcx-swjtu/Coffee-Work/main/SKILL.md --name coffee-work
```

## 为什么需要它

真实的 AI coding 工作流经常不只依赖一个助手：

- Codex 适合聚焦实现和调试；
- Claude Code 适合做细致 review；
- Kimi Code 适合长上下文仓库理解；
- OpenCode 适合本地项目导航；
- Gemini CLI 适合快速检查和轻量 review；
- tmux 或类似工具适合保留长期运行的交互式 session。

没有桥接流程时，用户自己会变成 router：复制 prompt、记住哪个 terminal 里有什么上下文、确认测试是否真的执行过，再把结果粘回主助手。Coffee Work 把这套流程变成明确、可复查、带证据的工作流。

## 它能做什么

Coffee Work 教 Hermes：

- 发现本地已经安装的 coding CLI；
- 有意识地选择 backend、工作目录和 session；
- 在合适的时候复用已有 session；
- 构造包含角色、背景、任务、约束、成功标准和汇报格式的 prompt；
- 调用用户指定的真实 CLI，不用别的助手冒充；
- 通过 terminal、tmux 或 process log 监控长任务；
- 收集原始输出、diff、产物和验证结果；
- 汇报实际发生了什么，包括失败和不确定性。

## 示例请求

实现并复查：

```text
/coffee-work 用 Codex 为这个失败测试实现最小修复。然后用 Claude Code 做只读 review。最后汇报两个 agent 的证据。
```

合并前复查：

```text
/coffee-work 用另一个本地 coding agent 审查我最新的 diff。不要改文件。重点找正确性 bug、安全问题和测试缺口。
```

长上下文理解：

```text
/coffee-work 用 Kimi Code 检查这个仓库，并说明这个功能应该放在哪里。只读。
```

继续已有 session：

```text
/coffee-work 继续这个项目已有的 Codex session。除非找不到匹配 session，否则不要新开。
```

## 安全模型

Coffee Work 对证据和副作用保持严格：

- 汇报实际使用的命令或 session；
- 不在公开输出里泄露 secret、私人路径、真实 session ID 或私有项目名；
- 对 push、删除数据、花费额度、绕过 sandbox 等高风险动作先确认；
- 不编辑 coding-agent 的数据库、transcript 或隐藏 session 内部文件；
- 声称成功前先验证文件、产物和测试；
- 阻塞就说明阻塞，不编造成功结果。

## 仓库结构

```text
Coffee-Work/
  README.md
  README_zh.md
  LICENSE
  plugin.yaml
  __init__.py
  after-install.md
  SKILL.md
```

## 发布前检查

发布改动前，先扫描仓库里是否误提交了私有信息：

```bash
rg -n "(/Users/|/home/|API_KEY|TOKEN|SECRET|PRIVATE|@)" .
```

人工检查每一条命中。占位符可能是有意保留的；真实密钥、私人路径和私有账号标识不应该进入提交。

## License

MIT
