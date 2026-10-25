## What happens

On mobile, when a Bot reply contains a table, the table renders wider than the viewport and the overflow is clipped. Columns on the right are invisible and there is no way to scroll horizontally to reach them.

## Expected

A table in a narrow viewport should either scroll horizontally inside its own container, wrap cell content, or degrade to a card/list layout. Silent clipping loses information.

## Steps to reproduce

1. On the mobile app, ask a Bot to output a table with several columns (or one long cell).
2. Look at the right edge of the message.

Reported 2026-10-25. App version, OS and device are not captured yet; please attach a screenshot/device info if you have it.

## Impact

Reading table-shaped answers on mobile loses data; users cannot tell that content was cut.
