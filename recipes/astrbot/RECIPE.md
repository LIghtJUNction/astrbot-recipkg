# AstrBot 软件配方

```toml
format = "recipkg/1"

[package]
name = "astrbot"
version = "0.1.0"
kind = "software"
description = "多消息平台 AI 助手、Agent 与插件开发平台的重建配方"
entry = "BUILD_PROMPT.md"
```

观察基线：AstrBot 4.29.3，提交 [`abf683071952375ec36baa4cad6b6f3d9c9bb03f`](https://github.com/AstrBotDevs/AstrBot/tree/abf683071952375ec36baa4cad6b6f3d9c9bb03f)，上游许可证 AGPL-3.0-or-later。本配方版本不是上游软件版本。

当前只做了源码、文档和部分 issue 的静态观察；[BUILD_PROMPT.md](BUILD_PROMPT.md) 是重建要求，[ACCEPTANCE.md](ACCEPTANCE.md) 是验收计划，[UPSTREAM.md](UPSTREAM.md) 记录提案与问题。尚未进行独立重建或逐接口完整性审核，不应把本配方视为完整行为清单。

没有声明 Recipkg 子配方：上游插件、模型服务、聊天平台、数据库及系统工具属于外部运行依赖，不是已经审核通过的配方；插件隔离 SDK 在 RFC 中是提案，不能据此假定为必需的现成依赖。若重建确定需要自行实现的独立组件，应先查找并审核配方，缺失时递归补齐，不能用普通源码仓库冒充配方依赖。
