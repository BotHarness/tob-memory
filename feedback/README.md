# DSB 群1反馈记录

授权群：1125565676。精确接收范围为 conversationId `3DDEF310E4FA9BBD6989C062797E9131`，接收 Grant `56b3f9a1-10ad-4717-b266-5bc6b222a8e3`；原群主动发送只用保存目标 `dsb-group-1125565676-feedback`。

- `bugs.md`：真实 bug，保留编号、状态、时间、现象、预期、环境、复现、影响、临时办法及 Source Event ID。
- `suggestions.md`：功能建议。
- `processing.md`：已处理 Source Event ID、处理时间、条目对应关系及确认回复的 Outbox/request ID，避免漏记、重复处理或重复发言。
- `verification.md`：定位、验收和模拟故障，不计入真实 bug。

Host 全量保存未来符合权限的普通文字；普通消息满 10 条或 10 分钟聚合调用 DeepSeek V4.1 Flash high，先到者触发。被真实 @ 时即时回答。平时保持安静，仅主动回答 DeepSeekBot 相关问题；真实 bug 先记录，再在原群简短回复报告者。无关话题不回答。遵循 SOUL.md 的精确回复与发送规则。

写入后提交 Memory Git。文件保存在此 Bot 私有 Memory Repository，不自动发布。群媒体、全量启用前或断线期间历史尚未验收。

## Discord 范围（2026-10-19 开通）

- 服务器 `1556718520186839251`（DeepSeekBot），当前仅 `1556723306873491537`（#bot-playground），以 DeepSeekBot Mascot 应用接入，身份同一只托布。
- 实际可接收频道以 Host 下发的 Grant 为准；其他 Discord 频道尚未开通，出现新频道需维护者单独授权。
- 规则与 QQ 相同：普通消息 10 条或 10 分钟聚合、平时安静、真正 @ 及时回答；可答疑、记 bug、执行已授权的公开搜索与发图。
- 来源隔离：QQ 与 Discord 的对话内容不相互转贴，回复只留在来源频道。记录时注明平台与原始 Source Event，便于区分 QQ 群与 Discord #bot-playground 的反馈。
- 带 `TOB-DISCORD` 验收标识的消息视为模拟，只记入 `verification.md`，不计真实 bug。

