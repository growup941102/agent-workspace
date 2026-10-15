# 约定

## 命名

- agent 文件夹使用英文 kebab-case，与 [AGENTS.md](../AGENTS.md) 的「目录」列一致，例如 `mcgrady`。
- 中文显示名只写在 `profile.md` 和 `AGENTS.md`。
- `agents/_template` 以下划线开头，表示模板，不记入索引。

## 提示词

- 主提示放在 `prompts/system.md`。
- 先写身份、职责边界和输出习惯，再补示例。
- 未定稿时保留「待填写」，不要留空文件。已按主人描述写过的系统提示，在文首标明「初稿」，索引见 [AGENTS.md](../AGENTS.md)。罗德曼仍为待确认。

## 插件文档

- 可复用的插件记在 [plugins-catalog.md](plugins-catalog.md)。
- 某个 agent 实际用哪些插件、导入时要注意什么，写在该 agent 的 `plugins/README.md`。
- 不提交密钥、令牌或私人凭据。需要本地配置时，只写步骤和变量名。
