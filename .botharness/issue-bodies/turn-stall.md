## What happens

A task stops halfway and nothing continues until the user @s the Bot again and repeats the request. Users describe it as "it changes half, then stops".

## Possible causes (unverified)

- the turn ends while waiting for approval
- a tool call times out and the turn closes
- a long turn is truncated by incoming messages
- the model simply ends its turn early

## Expected

Finish or fail visibly. If the turn is waiting, timing out or was interrupted, say so in the channel; a half-finished task with no status is worse than a clear failure.

## Impact

Users re-@ and restate instructions, wasting tokens; half-applied changes remain in files.

Reported 2026-10-26, single report without version, model or logs.
