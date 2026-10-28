## What happens

Creating a new session fails immediately:

```
Session failed: INVALID_REQUEST: tools: at least one tool must have defer_loading=false.
All tools cannot be deferred. (request_id: ...)
```

Error details show `运行来源：Orchestrator`, HTTP 400.

## Expected

A session should be creatable. If some plugin marks every tool as deferred, the host should keep at least one resident tool, or refuse the plugin with a message that names it.

## Likely cause (unverified)

Some installed plugin marks the whole tool catalog `defer_loading=true`. The upstream validator requires at least one tool with `defer_loading=false`, so the request is rejected while the session is being created. This matches reports of "after installing a plugin I can no longer open a new conversation".

## Impact

Blocking: no new session can be created at all.

## Workaround

Disable the most recently installed plugin and retry; the plugin author should mark its core tools as non-deferred.

## Notes

User exported the failing session (`session.zip`) and sent it to the maintainer for inspection. Related: the "Orchestrator permission differs" report (same `Session failed` surface).
