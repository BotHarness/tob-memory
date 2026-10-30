## 现象

升级到 Tobs 1.6.0 之后，QQ 群里发送的**图片与文件**消息到达 Bot 时只剩下占位文本：

- 图片：`[Image not readable by the Bot]`
- 文件：`[File not readable by the Bot]`

对应的 Source Event 里 `attachments` 为空，Bot 既无法 `read_image`，也无法保存附件，只能回复「图/文件没过来」。

## 对照（同时段、同群）

更早的一条**引用消息里的图片**在同一群里是正常的：事件带完整 `attachments`（`id`、`name`、`sizeBytes`、`mediaType` 均有值），Bot 成功保存为本地文件并用 `read_image` 读取（1672×941 PNG）。

## 影响

- Bot 在群里完全「看不见」用户发的图和文件，会被当成装死或能力缺失；
- 依赖附件的工作流（看图排错、读日志文件、审截图）整条断掉；
- 纯文本消息不受影响，所以很容易被误判成单个用户操作问题。

## 环境

- Tobs `@botharness/tobs@1.6.0`（配套 `im-provider 4.32.0-botharness.23`、DSH `0.2.1-rc.3`）
- 通道：QQ 群（官方机器人账号）
- Bot 侧：DSH PersonaBot（Orchestrator），`bot_send_message` / 附件工具均正常

## 复现步骤

1. 群成员在群里直接发送一张图片（不带引用）；
2. 观察 Bot 收到的 Source Event：body 为 `[Image not readable by the Bot]`，`attachments` 字段缺失；
3. 同一群里改用「回复引用一条消息 + 附图」发送，则 `attachments` 完整、可正常读取。

## 疑似原因

纯图片 / 纯文件的 QQ 消息在 im-provider 的解包路径上丢了附件字段；带引用的消息走的是另一条路径，所以正常。与 #2895（QQ 引用、图片和图文混合消息不再丢失）相关但未覆盖「独立图片消息」这一路。

## 补充

- 1.6.0 之前（1.5.2）群里的图片消息是能被 Bot 读取的，属回归；
- 累计观察到十余条图片/文件消息全部为空附件。

---

*由 Bot 自动整理，已去除昵称、群号与内部 ID；原始证据保留在维护者侧 Memory 记录中。*
