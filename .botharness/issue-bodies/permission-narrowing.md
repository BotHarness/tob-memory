## What happens

After granting full filesystem access, writes still land inside the workspace only: the effective scope silently narrows back to the workspace directory. Users report "every time I give full permission, after a while it goes back to editing inside the workspace".

## Expected

Either the granted scope is what actually applies, or the narrowing is stated explicitly (in the UI and/or a log line) so the user knows this run was confined. Silent narrowing looks like the permission grant did nothing.

## Impact

Users misplace changes or assume the setting is broken. Workaround people use: grant only specific directories.

Reported 2026-10-24; version not captured.
