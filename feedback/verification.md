# 群反馈收集验收

- 2026-10-19（Asia/Tokyo）：维护者在群 1125565676 发送真正的 @ 消息 `DSB目标群定位1019`；Host 保存 Source Event `im-73b0b54b48f5e38d3115cede44a05fbdb9efa7fda75dbd599c21c0ecec0239d4`，由此确认该群的内部会话与独立 Grant。该消息不是 bug。
- 随后维护者发送新的普通群消息，当前接收器通过 ordinary delivery 验证，并成功将该精确单群的 collection 设置为 all。此时仅验证投递资格和配置，新的普通消息落盘仍需后续 canonical Source Event 证明。
