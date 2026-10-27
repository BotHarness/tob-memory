## What happens

Compaction fires repeatedly in a single session instead of reducing the context once. A real trace (2026-10-27, desktop) shows a chain like:

```
上下文已压缩 · 已压缩 3 条历史记录（约 3847 tokens）
上下文已压缩 · 已压缩 1 条历史记录（约 3616 tokens）
工具调用 · inbox_list
上下文已压缩 · 已压缩 3 条历史记录（约 4229 tokens）
… (repeats with 3583 / 4391 / 3586 tokens)
```

Each compaction is a model call, and each one only frees ~3.5k–4.4k tokens — so the session lands right back above the threshold and compacts again on the next turn. Asking the agent to stop does not help: compaction is a synchronous step inside the turn and cannot be cancelled.

## Expected

- Compact in one pass to a target level (for example 50–60% of the window) instead of shaving a few thousand tokens at a time.
- Do not re-compact the same span; if the previous pass did not get under the threshold, say so instead of retrying silently.
- Surface "how full is the context" so the user can decide to start a new session.

## Impact

Users see "slow and wasteful": several extra model calls per turn, each rewriting history, with little progress. It also makes the session feel stuck even though work is happening.

## Workaround

Start a new session instead of letting a long one ride the threshold.

Reported from a QQ community group; desktop client, versions not captured.
