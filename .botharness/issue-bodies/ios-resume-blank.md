## What happens

On iOS, backgrounding the app and returning to it leaves the chat area blank. Tapping the Bot to open the conversation then flickers endlessly ("无限闪屏"), and the app only recovers after going back to the home screen and entering the Bot again.

- Device: iPhone 17
- iOS: 26.6.2
- App: mobile build (exact TestFlight/production version not captured)

## Expected

- Returning from background keeps the conversation and scroll position.
- If a render failure happens, show a reload affordance instead of a blank pane, and never loop on flicker.

## Suspected areas (not verified)

- View measurement loss after the app resumes (related in-flight work: "preserve measured chat dimensions after initial placement").
- Navigation stack rebuilding on resume ("reset workspace history and cancel stale navigation").

## Impact

Every trip out of the app requires a full re-entry through the home screen; the app is effectively single-foreground only.

Reported 2026-10-26 from a community group.
