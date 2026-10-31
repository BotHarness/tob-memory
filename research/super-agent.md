# Super-agent（DeepSeek Harness 团队，2026-10-31）

来源：《Super-agent 设计探索：迈向更自主的 Agent 系统》官方文章；IT之家转述 https://www.ithome.com/1/020/615.htm

## 一句话

把「一个会话一件事」换成「Router 接人 + Worker 干活」的双层结构，让 Agent 连续、并行、主动、持久。

## 架构

- 双层：Router 承接人类交互、维护全局上下文、分派任务；Worker 在隔离会话并发执行，结果汇报给 Router，不直接对外。
- 事件驱动：群消息、邮件/日程、PR 评论、CI 结果都是 Trigger；先程序规则过滤，再交模型判断是否行动。已分配任务的 Thread 可由程序直发 Worker，绕开 Router 降负载。
- Inline & Spill + 链式召回（Chain of Recall）：近期信息进窗口，超预算的留在窗口外按需读；靠 Trigger/Thread/Worker Session 的引用关系沿 ID 找回历史。
- 投机执行：根据环境信号后台预先开工（如收到会议邀约先查冲突备稿；群里讨论 bug 先复现），确认后再交付。
- 异步 ReAct Loop：耗时工具调用改为 start()/stop()，先回 Started，结果作为新事件进会话。**已在 DSH 中实现但未默认开启**。
- 计算与状态/环境分离：计算与状态在云端，执行环境可在用户本地，只放轻量 daemon，支持 BYOM。
- Watchdog：独立会话做外部控制回路，既看基础设施报错，也让模型判断 Worker 是否真在推进、方向是否偏。

## 实验（合成负载，只测调度）

- 每次约 300 条消息、其中约 20 条工作请求，各方案重复 5 次。
- Super-agent：p50 12.4 分钟、p95 15.7 分钟；中性提示的单 Session 方案 p95 29.5 分钟。
- Router 压测：Trigger 从约 1 条/分升到约 40 条/分，批处理从 1.0 到 2.8，单次请求 2.5→3.9 秒，单个决定分摊推理 6.4→1.6 秒（积压可合并、有效吞吐提升）。

## 自陈局限

Router 如何随规模扩展、跨月长程记忆、脱离 Session 后的人机协作、实例间 A2A 通信、以及云端接入本地设备后的提示词注入/端侧凭据/跨设备权限。

## 与 Tobs 的对照（我的判断）

- 骨架已对上：Orchestrator ≈ Router，Assignment ≈ Worker，且 Worker 结果回 Orchestrator 再对外。
- 缺的三块：真正的 Trigger 层（现在靠人 @ 唤醒，不是自己看群判断）、异步 ReAct 长工具不堵前台、Watchdog 级的外部监控。
- 原型仓库 `deepseek-ai/dsh-superagent-prototype`，官方声明为技术验证、非正式产品。
