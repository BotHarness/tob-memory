## What happens

On a **source-built** DSH (run as `pnpm run dsh --profile <name>` from the repo), asking the Bot to create a Bot fails immediately:

```
运行来源：Orchestrator
tool-subagent-list-agents (@deepseek-ai/dsh-tool-subagent-control/list-agents): never started
```

The tool entry is present, not missing. `dsh --profile <name> --dump-config` lists `tool-subagent-control` (alongside `subagent`, `subagent-spawn-in-process`, `subagent-fork-in-process`, `tool-subagent`, `tool-subagent-fork`), so it is mounted but its start never completes.

## Reproduced on a clean profile

`dsh --profile rescue --from-default-profile web` → fresh profile, no patch errors, model account resolves (`llm-deepseek-account … loaded 2 model(s)`), then installing Tobs and creating a Bot still produces `never started`.

So this is not the user's stale `cordis.patch.yml` and not a missing package.

## Environment

- DSH: built from source (`node --import tsx/esm apps/cli/src/bin.ts`), repo revision late October
- Tobs / DeepSeekBot: 1.5.2
- OS: Windows (win32 x64)
- Model path: `llm-deepseek-account` resolves models; a separate `llm-deepseek-api-key` entry returns HTTP 401 for `/models` and is unused here

## Expected

- If the tool cannot start, say why (missing dependency, failed activation, model unavailable) instead of reporting `never started`.
- Creating a Bot should work in a default profile from source builds.

## Workaround

Run an npm-installed DSH (pinned release) rather than the source checkout; the packaged runtime ships the tool in a working state.

Note: `pnpm -r build` on this repo also fails with `ERR_PNPM_TASK_CYCLE` under pnpm 11; the top-level `pnpm build` works.
