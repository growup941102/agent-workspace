# Agent 维护仓库

这个仓库用来维护左侧 agents：提示词、文档，以及插件导入说明。它是文档与配置工作区，不包含应用代码。

每位 agent 单独一个目录。基础职责已按主人描述填写；系统提示是初稿，插件说明仍待补。罗德曼仍在设计，先空着。

## 如何新增一个 agent

1. 复制 `agents/_template`，把文件夹改成英文 kebab-case（例如 `bird`）。
2. 编辑其中的 `profile.md`，填上中文显示名。职责和提示词可以先留「待填写」。
3. 在 [AGENTS.md](AGENTS.md) 增加一行：目录、显示名、职责、状态。
4. 若该 agent 使用共享插件，在 [shared/plugins-catalog.md](shared/plugins-catalog.md) 登记，并在它自己的 `plugins/README.md` 写下导入笔记。

中文名只出现在档案和索引正文里，不要用作文件夹名。`agents/_template` 只作复制起点，不要把它写进索引。

## 目录约定

```
agents/_template/          新 agent 的复制起点
agents/<name>/             单个 agent
  profile.md               名称、头衔、一句话职责
  prompts/system.md        主系统提示
  docs/overview.md         较长说明与工作流
  plugins/README.md        该 agent 的插件与导入笔记
shared/conventions.md      命名、提示词写法、插件文档约定
shared/plugins-catalog.md  共享插件清单与导入维护笔记
AGENTS.md                  全部 agent 的索引
```

更细的写法见 [shared/conventions.md](shared/conventions.md)。

## 当前 agent

基础职责已按主人描述填写，详见 [AGENTS.md](AGENTS.md)。波波维奇是产品经理，状态为「基础已填」。罗德曼除外，状态是「设计中 / 暂空」，内容待确认。各 agent 的系统提示是初稿，主人可以继续改。

## 填写节奏

档案、概览和系统提示初稿里已有基础职责。插件导入说明，以及主人之后补充的细节，按实际使用再写。不要把密钥、令牌或私人凭据提交到本仓库。
