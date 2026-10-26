## What happens

Channel message cleanup fails, and the UI shows no error at all: no reason, no counts, no indication of which messages remain.

## Expected

- failure states a readable reason (permission, partial failure, in-use, limit)
- report how many messages were removed and how much space was reclaimed
- success also shows the result, so the user can trust it happened

## Impact

Users believe the space was reclaimed while messages are still stored; with no error they cannot diagnose or work around it.

Reported 2026-10-26 by a maintainer; App version and entry point not captured.
