## What happens

A direct @ sometimes gets no response; a second @ usually does. Separately, a Bot may legitimately choose not to answer, and from the user's side that is indistinguishable from a lost message.

## Expected

Some visible state for the addressed message: received / processing / intentionally skipped. Users should not have to re-@ to find out, which also costs tokens.

Community discussion suggested exactly this ("add a read state"), and splitting it into two levels: 1. received, 2. processed.

## Impact

Repeated @s, wasted tokens, and reports that look like "the Bot ignores me".

Reported 2026-10-25; version not captured.
