## What happens

When a user quotes an earlier message and then mentions the Bot in the same message, the Bot cannot read the quoted content — it only sees the new sentence. Asked to answer "this", it has no idea what "this" refers to.

## Expected

The quoted message body (and its attachments, if any) should be available to the Bot as context.

## Impact

Quoting is the most natural way to carry context in a group chat. Without it every follow-up has to be retyped or re-sent as a screenshot.

## Workaround

Users retype the original text or re-send it as an image.

## Notes

Maintainer confirms the behaviour and says it is fixed in 1.6.0.
