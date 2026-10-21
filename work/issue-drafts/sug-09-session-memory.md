## Summary

Users want a PersonaBot to be able to inherit or import the memory and context of an existing DSH session, instead of manually re-summarising the conversation into the Bot's Memory or passing a file.

## Actual behaviour

- Bot sessions and ordinary DSH sessions are separate; there is no entry point that attaches an existing session to a specific Bot.
- The only workaround today is manual: summarise the conversation into the Bot's Memory, or hand over a file/attachment.

## Expected behaviour

An explicit, reviewable way to import selected context from an existing session into a Bot's Memory, with a clear scope and redaction step, or a documented handoff flow.

## Why this matters

People build context in a long session and then want a specific Bot to continue the work without explaining everything again.

## Notes

This is a feature suggestion from community discussion; there is no reproduction. Related but distinct: #2091 (cross-Bot Memory reading) and #896 (Memory erasure on delete).
