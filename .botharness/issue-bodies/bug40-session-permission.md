## What happens

Starting a new session fails with:

```
Session failed: Orchestrator Session permission differs from this PersonaBot's access setting
```

The user had simply sent a message to open a fresh conversation after a long one; the error repeats on every subsequent attempt, so the Bot becomes unusable for that person.

## Expected

A new session should be created with the Bot's current workspace-access setting, or the error should name the two conflicting values and how to reconcile them.

## Likely cause (unverified)

The Orchestrator carries a permission snapshot taken when the Bot was configured; if the Bot's access setting was changed afterwards (or the two defaults differ), the mismatch blocks session creation instead of being reconciled.

## Workaround (to verify)

Change the Bot's workspace access to the matching mode, then start a new session; or restart the host so the snapshot is refreshed.

## Notes

Maintainer says a fix is planned for 1.6.0. Related: #2727 (subagent permission boundaries), and the "permissions silently narrowed" report.

Reported from a QQ community group; app version and the exact access setting were not captured.
