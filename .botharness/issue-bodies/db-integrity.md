## What happens

The app refuses to load the Bot roster and reports:

```
活动同步已中断…正在重新连接…
名册加载失败：Operational database is in recovery mode: integrity-failed
OperationalDatabaseError: Operational database is in recovery mode: integrity-failed
```

The main pane shows "还没有 Bot" and a toast offers "重新检查并继续", which does not help. Retry produces the same error. From the user's side it looks like the app is simply "disconnected" or out of quota.

A related case: after a Chinese-speaking user asked the Bot to fix context compaction and granted it permission to restart, the phone lost connection, DSH failed with "无法新建会话", all Bots disappeared, and the instance only recovered after an external agent repaired the local state database.

## Expected

- A corrupt operational database should be reported as such, with an actionable message: where the data lives, how to back it up, and what repair path exists.
- The app should not present the failure as "no Bots" or "reconnecting".
- A failed/aborted restart should not leave the state database unopenable.

## Steps to reproduce

1. Use the app normally.
2. At some point (unclear trigger; possibly unclean shutdown or a restart while writing) the operational database fails its integrity check.
3. Open the app: roster fails to load, Bots are gone, new sessions cannot be created.

Exact trigger is unknown. Two reports so far; both resolved by repairing the state database externally.

## Suggested temporary workaround (for docs)

Before any repair or reinstall, quit the app and copy the whole data directory (`botharness.db`, `-wal`, `-shm`, logs DB). Then run `sqlite3 .recover` (or an equivalent) on a copy, rather than deleting the database.

## Impact

Total loss of access: no Bot list, no sessions, and no obvious recovery path inside the UI. Users are likely to reinstall and lose data.

Reported 2026-10-25/26 from a community group. Versions not captured for both reports; screenshots available on request.
