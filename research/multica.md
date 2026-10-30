# Multica 调研（2026-10-30，clone 到 /tmp 只读看）

仓库：https://github.com/multica-ai/multica （官网 multica.ai，license 见 LICENSE/NOTICE）

## 定位
团队工作区 + 本地执行器：人把任务派给 AI coding agent，agent 在自己机器上跑、边做边评论，完成挪到「审核中」等人验收。可自托管，不绑定厂商，复用已装的 agent CLI。

## 组成
- 服务端：Go + Postgres + sqlc + 迁移（server/migrations 到 594），实时 WS（server/internal/realtime）。
- 本地：`multica` CLI 的 daemon（`multica daemon start`），探测机器上已安装的 agent CLI（codex/claude 等）并注册运行时，接任务在本机执行。
- 前端：apps/web、apps/desktop、apps/mobile，核心是看板视图。
- 包：packages/core（issue-statuses、issue-workflows、api、workspace 等）、plugin-sdk、ui/views。

## 关键设计
1) 任务挂在 issue 下，不平铺。四类生命周期：unstarted(backlog/todo)、started(in_progress/in_review/blocked)、done、closed(cancelled)；自定义状态的 key/category 不可变，done 不是通往 closed 的中间态（docs/issue-status-lifecycle-rollout.md）。
2) 任务带触发溯源（trigger_comment_id 等），每次 run 可追到「谁说了什么」。
3) 评论、执行、diff、审批都挂在同一 issue 下 → 上下文不用重述。
4) 并发：任务认领走数据库抢占 + 租约，有 claim race 测试（并发容量、抢占失败回滚队列、按触发评论释放容量）。对应「认领必须原子」。
5) daemon 跟随二进制升级：版本不一致时等当前任务结束再重启，不打断任务；agent CLI 就地升级时只重新探测版本并重注册，不重启。
6) autostart 为 opt-in；Windows Run key / macOS launchd / Linux systemd user unit。

## 对比 DSH/Tobs
DSH：Bot 有记忆与助手身份，长期驻在 IM 里；
Multica：人派活、agent 本机执行、看板管流程。
可借鉴：issue 生命周期分类、认领租约、触发溯源。
