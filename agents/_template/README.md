# Agent 模板

复制整个 `_template` 目录来新增 agent，然后把文件夹改成英文 kebab-case。不要把本目录当作正式 agent，也不要写进 [AGENTS.md](../../AGENTS.md)。

| 文件 | 放什么 |
| --- | --- |
| `profile.md` | 名称、头衔、一句话职责 |
| `prompts/system.md` | 主系统提示 |
| `docs/overview.md` | 较长说明与工作流 |
| `plugins/README.md` | 该 agent 使用的插件、连接器，以及导入笔记 |

复制后把占位改成该 agent 的内容，并在索引表增加一行。中文名只写在正文里。
