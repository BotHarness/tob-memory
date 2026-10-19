# DeepSeekBot 群反馈：Bug

每项记录：稳定编号；状态（用户报告/待补充/已复现/已修复）；首次与最近报告时间；问题现象；预期行为；版本与环境；复现步骤；影响；临时办法；来源 Source Event ID。定位与验收消息不计入真实故障。

---

## BUG-20261019-01 @ 消息正文丢失（待补充）

- 状态：用户报告（待补充，未复现）
- 首次报告：2026-10-19 03:43（Asia/Tokyo）；最近报告：2026-10-19 03:43
- 现象：群成员发送的 `@DeepSeekBot QQ QA` 消息在 Bot 接收端正文为空，没有携带用户输入内容；随后同一用户表示「我觉得这个消息处理机制还是有待修复」。
- 预期行为：@ 消息应完整携带发送者输入的正文，Bot 读取后正常应答。
- 版本与环境：未知。群为 QQ 1125565676；接收应用 DeepSeekBot QQ QA；客户端版本、Host 版本待补充。
- 复现步骤：未知。仅观察到一次空正文消息，未确认可复现。
- 影响：提问或反馈内容可能丢失，Bot 无法应答；用户对消息处理机制产生疑虑。
- 临时办法：发送者重发内容（本次已由 Bot 请其重发）。
- 来源 Source Event ID：
  - `im-6984319cc7cf90b171365cf39319795740975a4f5a71b90054def1c74ea9cf74`（正文为空的 @ 消息）
  - `im-e56a27b919c1752b0da33213b17bd6ceac4c1de3d91c7ab879f3862266176a7d`（用户称消息处理机制有待修复）
- 备注：无法区分是平台侧吞消息、发送端问题还是接收链路丢正文；未做复现验证，不得当作已确认缺陷。

---

## BUG-20261019-02 安装后找不到返回普通 Harness 的入口（用户报告，待补充）

- 状态：用户报告（待补充，未复现）
- 首次报告：2026-10-19 05:57（Asia/Tokyo）；最近报告：2026-10-19 05:58
- 现象：安装 DeepSeekBot 后启动即进入 Bot 界面，用户找不到回到原 DeepSeek Harness 页面的入口；群友指出入口在左上角 DeepSeekBot 图标处，并认为该入口「确实隐藏起来了」，建议补引导。
- 预期行为：首次进入或界面切换后，有可发现的入口/引导说明如何回到普通 Harness 模式。
- 版本与环境：未知（QQ 群 1125565676 讨论；平台/客户端版本待补充）。
- 复现步骤：未知；仅描述为安装后的默认打开行为。
- 影响：新用户可能误以为无法回到原界面，造成使用困惑。
- 临时办法：点击左上角 DeepSeekBot 图标切换。
- 来源 Source Event ID：
  - `im-46e430e7f89553964fbbaaccc9365917917fdda517f78b0d211118cb186fab1b`（默认直接打开 deepseekbot，没法打开之前的 harness 页面）
  - `im-fd183c75e08a5476c682c9d4d1d7682df8d3bba11b09b67b9d413bd2a8556be4`（没找到在哪儿回去）
  - `im-acb2303a71473d817ed6d0660953b98350ff614b9c9c2b4cf4b1c8bcaa55d75a`（左上角 DeepSeekBot icon 的位置）
  - `im-a669c05711fc969e9d546c893e37698c8e13bec5d1e517f6f18912b4d6632bdf`（感觉要补一个引导，确实隐藏起来了）
- GitHub Issue：#2289 https://github.com/BotHarness/DeepSeekBot/issues/2289（2026-10-19 创建，state=open，作者 DoodleBears；标题：Installed plugin opens in Bot mode with no discoverable way back to the standard workspace）
- 备注：群成员曾要求提 issue；2026-10-19 获得持续授权与可用凭据后已实际提交，正文脱敏、未含群聊原文/成员身份/路径/Source Event ID。

---

## BUG-20261019-03 UI 界面与部分皮肤冲突（用户报告，待补充）

- 状态：用户报告（待补充，未复现）
- 首次报告：2026-10-19 06:03（Asia/Tokyo）
- 现象：界面会与某些皮肤（主题）冲突；补充信息为「深海女仆工坊皮肤的侧边栏会和 bot 侧边对话栏冲突」，希望优化。具体平台/版本仍未说明。
- 预期行为：切换/启用皮肤后界面显示正常，不与 Bot 面板或聊天区域冲突。
- 版本与环境：未知（QQ 群 1125565676 讨论；客户端与平台待补充）。
- 复现步骤：未知。
- 影响：使用皮肤的用户可能出现显示异常；影响面待评估。
- 临时办法：未知。
- 来源 Source Event ID：`im-8f23d171b4984d60b49cf639b624db54a31eb50ffb5e85728f0dcbd141c8c11d`、`im-20e3d4a38ca03e4b5a15e9977fd82fc37b82507976cd4b1f9a3ef9eb90d86c20`
- GitHub 提交状态：待提交（gh 未登录），信息不足前不公开开单。

---

## BUG-20261019-04 定时任务弹窗串到其他 Bot 卡片（用户报告，待补充）

- 状态：用户报告（待补充，未复现）
- 首次报告：2026-10-19 06:07（Asia/Tokyo）
- 现象：在定时任务里点了创建后，只要还没关掉定时任务图标，点其他 Bot 卡片都会再弹一次「新建定时任务」。
- 预期行为：新建弹窗只属于当前 Bot/当前操作，切换 Bot 卡片不应重复触发，或关闭后不再出现。
- 版本与环境：未知（QQ 群 1125565676 讨论；客户端版本与平台待补充）。
- 复现步骤（用户描述）：打开定时任务 → 点创建 → 不关闭定时任务图标 → 切到其他 Bot 卡片 → 弹窗再次出现。
- 影响：误弹窗可能造成重复创建定时任务或误操作。
- 临时办法：先关闭定时任务图标再切换 Bot。
- 来源 Source Event ID：`im-23a9af6909063ed36277d3cca35755323a99f5c871d9c45ca69b5945cf958354`
- GitHub 提交状态：待提交（gh 注入验证受阻，见本地记录）。

---

## BUG-20261019-05 secret_cli 注入执行被拒「需要 IM source_event_id」（用户报告，待补充）

- 状态：用户报告（待补充；同一调用后来成功，疑似上下文判定问题）
- 首次报告：2026-10-19 06:16（Asia/Tokyo）；06:21 同参数重试成功
- 现象：用 `secret_cli`（program=`gh`，env `GH_TOKEN={{token}}`）做只读验证时，两次返回同一错误：`Select one live accepted IM source_event_id for private input`。此前把 program 写成 `/usr/bin/gh` 时另返回：`program must be a bare program name without a path`。
- 预期行为：已配置的私密账号在本地 DM 里也能直接注入执行，不需要 IM 来源标识。
- 版本与环境：未知（Bot 运行时；QQ/Discord 与本地 DM 并行存在多来源）。
- 复现步骤：本地 DM 中用 secret_cli 跑 gh 只读命令（带 {{token}} 引用）→ 被拒；同参数稍后重试 → exit 0，返回 DoodleBears。
- 影响：凭据已配置却无法验证或开单，属于可用性阻塞；已自行恢复。
- 临时办法：有限——在新一轮纯本地 DM 中同参数重试可成功一次；属间歇问题、根因未修复，不建议反复重试。
- 来源 Source Event ID：`im-b44f36bba34200d0e12c726a725e3e1c526d23aa151a2982443b473461b2e6ee`（群友要求记录报错）
- GitHub Issue：#2290 https://github.com/BotHarness/DeepSeekBot/issues/2290（2026-10-19 创建、同日按维护者要求更正正文；state=open，作者 DoodleBears；标题：secret_cli intermittently refuses local DM runs and demands an IM source_event_id）
- 备注：正文明确写「间歇性、未确认根因、未复现」，并把 /usr/bin/gh 的 bare program 报错列为另一条已知用法约束，不混为同一原因；未包含 token、路径或内部来源标识。

---

## BUG-20261019-06 上下文溢出表现为频道内「偶发失败」，错误不易识别（用户报告，待补充）

- 状态：用户报告（待补充，未复现）
- 首次报告：2026-10-19 07:28（Asia/Tokyo）
- 现象：在频道里对话偶发失败，用户误以为模型卡住；追问后才知道是上下文溢出。另有补充：会话太长后「怎么发都提示超出」，只能重新开会话；也有用户认为可能是 DSH 侧（思考+输出超限被截停）而非 DSB 独有，根因未确认。
- 预期行为：上下文达到上限时应给出明确、可操作的提示（例如建议新会话/compact），而不是表现为无响应的偶发失败。
- 版本与环境：未知（QQ 群讨论；客户端版本与频道类型待补充）。
- 复现步骤：未知；需要长会话累积。
- 影响：用户难以判断是网络、模型还是上下文问题，影响排障与信任。
- 临时办法：重新开一个会话；群内提到 `/new` 在 PR 中，未确认正式版可用；另有先 compact 再闲置的优化讨论。
- 来源 Source Event ID：`im-83df7e2719ee453810af1ed51128c0791346aacee347d74c4964881cf70f1ee7`、`im-0f08c7cdf1766d6ade381a45d010fc31476bcccecea73898ebb22597e44afe01`（上下文/compact 讨论）、`im-ff5b2da860096eb346e3a7ecb4248e4052886b3e15e3c326e3a720075ec07c56`、`im-b03e957e7e9e46fa027cc4d0e09666292a79a1335ba12401ef9211b98d644a76`、`im-adedecac2d6bfdc3c1bb91c2a681ee1aa7971be7b17ef457fe064d762d0f5009`、`im-19dd5fd1c7df715d87c3319d9d582b80998c36540b987efed5d617978d6a8aa3`、`im-fb95002b92e9eebeadeda9eb5dd81725a6dc7a13b1c66ee54ae4be7e98be86ac`、`im-0a1a9bb662fcbc60107855c75149a4652e6723e360a7e08e862db075cb9f7bae`、`im-2681d796c9520e57034337670a973dd578ee2f669c60bc526b091b661dcb590d`（多用户补充：可能属 DSH、会话过长只能新开）
- GitHub 提交状态：待提交。2026-10-19 07:30 在本轮去重搜索时 secret_cli 再次返回 `Select one live accepted IM source_event_id for private input`；按规则未循环重试，未开单。



