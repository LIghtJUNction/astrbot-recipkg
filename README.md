# AstrBot Recipkg

![软件与依赖汇聚为可重建的配方](https://raw.githubusercontent.com/recipkg/recipkg/main/assets/recipkg-cover.png)

以 [AstrBot](https://github.com/AstrBotDevs/AstrBot) 为观察对象，建立可独立重建的软件配方；这不是 AstrBot 的运行源码或官方发行版。

- 配方入口：[recipes/astrbot/RECIPE.md](recipes/astrbot/RECIPE.md)
- 重建要求：[BUILD_PROMPT.md](recipes/astrbot/BUILD_PROMPT.md)
- 验收：[ACCEPTANCE.md](recipes/astrbot/ACCEPTANCE.md)
- 上游 issue、RFC 和决策边界：[UPSTREAM.md](recipes/astrbot/UPSTREAM.md)
- `source/` 是固定版本的上游观察子模块，不是配方依赖或配方内容。

配方目前是初始化版本：核心能力和重要风险已有要求，但公开 API 的完整字段、所有平台和插件兼容性、界面视觉、性能基线及独立重建尚未逐项核实，不能宣称已经完整复刻。实际使用前应补齐这些内容并执行验收。

```sh
git submodule update --init --recursive
recipkg check recipes/astrbot
recipkg build recipes/astrbot --lang zh-CN
```

配方是 Markdown 负载；源代码及共享技能子模块均不打包。将来若发布 GitHub 配方仓库，应添加 `recipkg` topic。上游 AstrBot 采用 AGPL-3.0-or-later；重建和分发前应检查适用许可及第三方依赖许可。
