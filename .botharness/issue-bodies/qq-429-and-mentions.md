## What happens

Two related QQ-channel behaviours:

1. **Concurrency → 429.** When several messages in a group are handled at once, the send path hits a 429 rate limit and the whole turn fails, including replies that had nothing to do with the burst.
2. **Mentions-only mode leaks.** With a Bot set to "only direct @", Bots that were not @-ed still reply to ordinary messages, so the setting does not actually restrict who answers.

## Expected

- A 429 should be retried with backoff per message, and should not fail unrelated replies in the same turn; the failure should be attributable to rate limiting in the UI.
- "Only direct @" should be enforced before a turn starts, not after the model has already produced an answer.

## Impact

Busy groups see whole turns fail; in multi-Bot groups the mentions-only expectation is broken, so several Bots answer the same message (and burn tokens doing it).

Reported in late October from a QQ group; versions and the exact 429 body not captured.
