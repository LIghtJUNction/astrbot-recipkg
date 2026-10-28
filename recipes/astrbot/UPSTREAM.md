# 上游 issue 与 RFC

检索时间：2026-10-28；公开 GitHub issue 列表按更新时间和 `RFC` 关键词检索。这里是有针对性的初始筛选，并非所有开放问题的完整审计。状态会变化；开始实现前重新读取原帖、评论、关联 PR 和固定基线代码。以下是报告或提案，不等于本项目已复现，亦不自动等于上游接受或修复。

## RFC 和演进

| 来源 | 当时状态 | 本配方如何处理 |
| --- | --- | --- |
| [#1948 pipeline/workflow 草案](https://github.com/AstrBotDevs/AstrBot/issues/1948) | open；原文更新说实际落地简化为 chain，并尽量兼容插件 | 记录会话隔离、钩子和状态迁移风险；基线实际实现仍须逐项验证，不以草案要求整个 DAG 工作流。 |
| [#3210 插件与核心隔离](https://github.com/AstrBotDevs/AstrBot/issues/3210) | open，修订中 | 研究独立进程、SDK、通信、旧插件迁移；协议和安全边界未定，不把提案写成默认实现。 |
| [#6728 插件分类](https://github.com/AstrBotDevs/AstrBot/issues/6728) | open | 分类、筛选和历史插件“未分类”是候选设计；字段是否强制及分类体系未定。 |
| [#3497 原生主动消息](https://github.com/AstrBotDevs/AstrBot/issues/3497) | closed | 区分主动触发和伪造用户输入；核实实际已实现部分，关闭不代表原提案全部完成。 |

## 候选回归场景

| 来源 | 上游报告的风险 | 重建验收方向 |
| --- | --- | --- |
| [#10833](https://github.com/AstrBotDevs/AstrBot/issues/10833) | stall 限流下会话等待任务可能无界积压 | 有界排队、过期与清晰溢出策略。 |
| [#10805](https://github.com/AstrBotDevs/AstrBot/issues/10805) | stop 后排队任务仍准备请求，重复停止重复计数 | 取消检查覆盖等待和建请求边界；重复操作幂等。 |
| [#10819](https://github.com/AstrBotDevs/AstrBot/issues/10819)、[#10338](https://github.com/AstrBotDevs/AstrBot/issues/10338) | 图片打断工具调用与回执，或钩子删除回执导致历史不合法 | 严格匹配调用 ID 与回执，保留协议顺序和后续会话可恢复性。 |
| [#10822](https://github.com/AstrBotDevs/AstrBot/issues/10822) | 图片历史持久化与请求注入不对称，可能破坏缓存并反复发送 base64 | 审核多模态历史与缓存策略，限制资源占用并保持语义一致。 |
| [#10820](https://github.com/AstrBotDevs/AstrBot/issues/10820) | 沙盒同步可能忽略人格及停用状态 | 只上传当前明确启用且有权使用的技能。 |
| [#10824](https://github.com/AstrBotDevs/AstrBot/issues/10824) | MCP 2.x 接口不兼容被超时掩盖 | 遵守已支持版本约束、快速报告不兼容；当前基线声明 `mcp>=1.8.0,<2`。 |
| [#10322](https://github.com/AstrBotDevs/AstrBot/issues/10322) | 知识库 scope 白名单不一致可能产生 403 | API 权限声明与路由授权保持一致。 |
| [#10806](https://github.com/AstrBotDevs/AstrBot/issues/10806) | 知识库上传可能泄漏 aiosqlite 工作线程 | 成功、失败及取消时均释放资源。 |
| [#9545](https://github.com/AstrBotDevs/AstrBot/issues/9545) | 部分依赖已安装时，插件剩余依赖可能未安装 | 混合已安装/缺失依赖时完整解析并报告。 |
| [#10737](https://github.com/AstrBotDevs/AstrBot/issues/10737) | 主动任务期间对话历史提交滞后 | 交错对话与中途状态保持一致。 |

每项复现应固定具体版本和环境；不同 issue 的历史版本不一定等同于本配方基线，不能直接认定该提交存在同一缺陷。新 issue 应记录来源、日期、风险、对应行为和测试状态，定期核对关闭原因与合并提交。
