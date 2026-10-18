# 群反馈收集验收

- 2026-10-19（Asia/Tokyo）：维护者在群 1125565676 发送真正的 @ 消息 `DSB目标群定位1019`；Host 保存 Source Event `im-73b0b54b48f5e38d3115cede44a05fbdb9efa7fda75dbd599c21c0ecec0239d4`，由此确认该群的内部会话与独立 Grant。该消息不是 bug。
- 随后维护者发送新的普通群消息，当前接收器通过 ordinary delivery 验证，并成功将该精确单群的 collection 设置为 all。此时仅验证投递资格和配置，新的普通消息落盘仍需后续 canonical Source Event 证明。
- 2026-10-19 03:34（Asia/Tokyo）：维护者在本地 DM 正式启用反馈记录任务；Bot 实际重读 SOUL.md 与 feedback/*.md，并以 bridge_group_policy_list 复核配置：单群 Grant `56b3f9a1-10ad-4717-b266-5bc6b222a8e3`、conversationId `3DDEF310E4FA9BBD6989C062797E9131`、collection=all、wake=digest(5 条/600 秒)、ordinaryDelivery=verified。启用时 Inbox 内该群仅上述定位消息，无普通反馈来源。
- 2026-10-19 03:40（Asia/Tokyo）：群内收到 `不 @ 发 【模拟Bug1019】DeepSeekBot设置页白屏，重启后恢复（仅验收，不是真实bug）`，Source Event `im-cc93db7397d0707b0923630f86369ae05d339bbc1b3e644b80de1444900caee9`。按规则只记入本验收文件：现象=设置页白屏；临时办法=重启后恢复；性质=模拟/验收，不计入真实 bug，bugs.md 不新增。
- 2026-10-19 03:40（Asia/Tokyo）：随后真实 @ 消息要求确认该模拟反馈已记录并回复「群反馈验收通过」，Source Event `im-a513b18a2042ade6bd6fd6a7df854b366b0df7703207a159b6bafa5cc6675ee6`；已按 @ 即时回答，未进入长时间聚合等待。
