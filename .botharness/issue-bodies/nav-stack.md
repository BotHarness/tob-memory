## What happens

Opening a channel from a notification pushes a new page onto the navigation stack instead of replacing the current one. Repeated notifications for the same channel (or opening the same channel again) stack duplicate pages, so the back gesture has to walk through copies and the user loses track of where they came from.

## Expected

Notification deep links should preserve back behaviour without stacking duplicates:

- push when the target is not already on the stack;
- `popTo` (or equivalent) when the same channel is already on the stack, instead of pushing a second copy;
- `replace` only when the intent is to swap the current page (detail → detail);
- `reset` / `replaceAll` stays for account or Bot switches, and tab changes.

## Suggested stack vocabulary

| Operation | Use for |
| --- | --- |
| push | normal forward navigation |
| replace | swap the top page, no back entry |
| replaceAll / reset | login, Bot/account switch, clean slate |
| popTo / popUntil | return to a page already in the stack |
| modal / dismiss | overlays that should not live on the stack |

## Impact

Back navigation becomes confusing and deep links multiply pages; users end up in the wrong place after following a notification.

Reported 2026-10-25 from a design discussion; exact platform/version not captured yet.
