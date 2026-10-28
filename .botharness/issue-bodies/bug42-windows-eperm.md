## What happens

Installing a plugin on Windows fails at the last step of `pnpm`:

```
[ERR_PNPM_EPERM] [importPackage C:\Users\<user>\.dsh\profiles\desktop\node_modules\dsh-boot-animation]
EPERM: operation not permitted, rename
'...dsh-boot-animation_tmp_41392_13' -> '...dsh-boot-animation'
```

Everything before that succeeded — 376 packages resolved, 295 added — so the network and the registry are not the problem. Only the final rename from the temporary directory to the real one fails.

## Expected

Either the replace succeeds, or the error says the directory is in use and what to close.

## Likely cause

On Windows, renaming a directory fails with EPERM while a process still holds a handle to it. Typical holders: the running DSH process for that profile, a file watcher, an antivirus scanner, or a leftover `*_tmp_*` directory from an earlier failed attempt.

## Workaround

1. Fully quit DSH for that profile (including tray and background processes).
2. Delete the stale `node_modules\dsh-boot-animation` and `node_modules\dsh-boot-animation_tmp_*`.
3. Install again. If it still fails: reboot, retry from an elevated terminal, or exclude `.dsh` from antivirus scanning.

Installing into a fresh profile also works around it.

## Environment

Windows, `%USERPROFILE%\.dsh\profiles\desktop`; DSH version not captured.
