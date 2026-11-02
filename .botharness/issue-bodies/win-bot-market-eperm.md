## 现象

Windows 上从 Bot 市场导入任意 Bot 均失败；新建 Bot 正常。失败后临时目录内包内容完整，可正常删除。

## 环境

- 系统：Windows
- DSH：0.2.1-rc.5
- 触发路径：Bot 市场 → 导入 Bot（任意一个都失败；新建 Bot 正常）

## 报错

```
EPERM, Permission denied: \\?\C:\Users\Administrator\AppData\Local\Temp\tobs-install-review-XXXX
```

## 判断（待验证）

安装流程疑似为「解压到 `%TEMP%\tobs-install-review-<id>` → 再移动到最终位置」，Windows 上 `rename`/`move` 遇到打开着的句柄就会返回 EPERM，常见来源：

1. 杀毒软件 / Windows Defender 实时扫描短暂持有文件句柄；
2. 解压进程自己还持有目录句柄未释放；
3. 该目录被当作工作目录（cwd）占着——Windows 不允许 rename 正在被当作 cwd 的目录。

失败后残留目录完整可删，说明写入本身没问题，卡在「移动/替换」这一步。

## 建议

- 移动前显式释放所有句柄、并把 cwd 切走；
- 失败时清理残留目录，不要污染下一次安装；
- 明确提示用户「可能是杀软占用」，并给出把 TEMP 换到短路径（如 `C:\tmp`）的临时方案。

## 与其他问题

与 #3222 家族的 Windows `EPERM / rename` 属同类（pnpm 安装时无法重命名 node_modules 下的包目录），建议一并排查 Windows 上的文件句柄与重试策略。

---

*由 Bot 根据群内反馈整理，已去除昵称、群号与内部 ID。*
