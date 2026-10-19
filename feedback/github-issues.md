# GitHub 反馈提交授权

## 持续授权

维护者 DoodleBear 于 2026-10-19 明确授权托布将已授权 QQ 群及 Discord 公开频道收集的 DeepSeekBot 真实 bug、安装使用障碍和可执行的产品建议，提交到 `BotHarness/DeepSeekBot` 的 GitHub Issues。旧仓库名 `BotHarness/BotHarness` 重定向到同一项目。此授权持续有效，无需对每张单再次请示。它覆盖搜索去重、创建 issue、向匹配的已有 issue 补充反馈，以及更新托布自己提交的反馈内容；不包含代码推送、合并、发布、关闭或删除别人维护的 issue、仓库管理或其他仓库。

授权已存在与凭据可用是两件事。不能再说“维护者没授权我开 issue”；也不能因为这份授权便声称已有可用凭据。使用实际可用的 GitHub 工具或已配置的 gh 身份，凭据保持机器本地，绝不放进命令参数、记忆、issue 或聊天。缺少登录、401/403、网络或工具权限失败时，准确报告具体阻碍，保留待提交记录，不绕过限制或借用别的账号。

## 私密账号与执行方式

GitHub token 通过原生 ask_secret 账号 `github-issues` 的必填字段 `token` 交由 Owner 安全填写。创建卡或复用时使用相同字段声明：id=token，label=GitHub fine-grained PAT（需含 Issues 读写与读取仓库元数据权限），required=true。ask_secret 返回 opaque references，绝不读取或复制真实值。

配置后通过原生 `secret_cli` 调用已安装的 `gh`：`program: "gh"`（必须是裸程序名，不能写 /usr/bin/gh），`account: "github-issues"`，`references` 使用 ask_secret 当前真实引用，`env: [{name:"GH_TOKEN",value:"{{token}}"}]`，`args` 每项一个参数，不含密钥、管道或 Shell 语法。这是每次调用的私密认证，不依赖普通 bash 里的 gh auth login 状态。普通 gh 未登录并不代表这个私密账号不可用。

首次先只读验证：args=["api","user","--jq",".login"]，再核对目标仓库 metadata。Owner 通过正常工具审批；若 Owner 对 gh、github-issues、GH_TOKEN 选择“始终允许此类”，后续相同程序/账号/环境变量名无需重复批准。它允许 gh 的任意参数，远程权限仍以仅目标仓库 Issues 读写的 fine-grained token 为限，不能把它扩成其他授权。

后续搜索、开单和补充反馈也走这个 secret_cli 账号。可使用 gh issue 命令或 REST API；提交正文从私有工作目录文件读取，不把任何秘密放进参数、文件或输出。不要运行 gh auth token、gh auth login、导出环境或将私密 token 再写到全局 gh 配置。

## 提交流程

1. 在原有 10 条/10 分钟批处理中整理真实反馈；真正 @ 的明确请求及时处理。先按 bugs.md、suggestions.md 去重，保留本地编号和原始来源。测试、模拟 bug 和普通闲聊不自动公开开单。
2. 搜索目标仓库已有 open/closed issues，核对产品部件、现象和触发条件。同一问题命中时关联已有 issue，确有新证据才补充，不重复开单或重复评论。检索或创建结果不明时，先查回结果再重试。
3. 新问题有足够可理解的事实就可以开单，不必先由维护者选单。标题写具体问题；正文包含脱敏现象、预期、实际行为、已知环境/版本、复现或触发信息、影响和临时办法。未知字段写未知；未亲自复现的标为用户报告/待复现。首次入口难找、缺引导等体验问题也可作为改进建议提交，保留本地编号映射。
4. 仅公开理解和排查问题所需的脱敏摘要。成员昵称、QQ/Discord 用户及群/频道编号、私聊、群聊全文、内部 Source Event ID、主机路径、Memory、凭据和未获公开授权的图片保留本地。日志和截图先脱敏；不确定能否公开的部分先省略，不因此阻塞可公开的摘要。
5. 用结构化工具参数，或将正文写入私有工作目录中的文件后用 `gh issue create --repo BotHarness/DeepSeekBot --title ... --body-file ...` 提交。只设置仓库实际存在且含义明确的标签；成功以真实 GitHub issue URL/编号为准。
6. 将 issue URL/编号回填原本的 bugs.md 或 suggestions.md，保留来源关联及提交状态，实质变化后提交 Memory Git。简短告知报告者链接；来源已回复或超出平台窗口时遵守原回复规则，必要时留给下一次合法回复，不复用已结算的来源或乱发其他频道。

当前本地 `BUG-20261019-02` 也属于授权范围；先搜索已有问题，避免重复。已有私有记忆中“不开 GitHub issue/必须维护者逐单决定”的旧操作记录只描述当时状态，以本授权为准。

## 来源上下文与失败处理

普通群反馈的持续开单授权和私密工具的当前来源校验是两层规则。每轮处理 IM 反馈需要使用这个账号时，先用 ask_secret 复用已配置账号，source_event_id 只选本轮实际接受、与该反馈有关的一条 IM Source Event；使用上述同一字段声明，已配置时应直接返回引用，不重新请求 token。不要在同一轮为同账号绑定多个不同 IM 来源；未知、历史、已失效来源不能代用。secret_cli 自身没有 source_event_id 参数，不要发明参数或将来源 ID 写进 gh 参数。

纯本地 Web DM 或 Schedule 的 ask_secret 应省略 source_event_id。若出现 Select one live accepted IM source_event_id for private input，这是已登记 #2290 的来源判定问题，不能由此声称凭据失效或需要新 token；一次失败后报告真实状态，不循环重试、读取原值、改来源权限或降级全局 gh auth。本次通过新一轮维护者本地 DM 验证成功并实际创建了 #2289、#2290，仅证明这条路径已可用，间歇来源问题仍未修复。对写操作超时或返回不确定，先只读搜索/回读确认是否已创建，禁止直接重发产生重复 issue。

仓库 permissions 元数据反映账号对仓库的角色，不是 fine-grained PAT 的有效权限清单；本账号 token 配置仅 BotHarness/DeepSeekBot 的 Issues 读写和 Metadata 读取，后续继续遵循这个范围。Owner 已保存对应 gh/account/GH_TOKEN 的自动审批时，不应虚称又出现了必须点击的新审批卡；仅在真实有待审批卡时请 Owner 操作。
