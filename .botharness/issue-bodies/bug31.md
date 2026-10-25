## What happens

On Android, tapping the model switcher in a chat crashes the app immediately — the model list opens and the app dies before a model can be picked.

- Platform: Android
- App version: 1.5.1
- Entry point: chat screen → model switcher

## Expected

The model list should open normally; if a model cannot be loaded, show an error and keep the current model. The app must not crash.

## Steps to reproduce

1. Open the Android app (1.5.1).
2. Open any chat.
3. Tap the model switcher.
4. App crashes as the list opens.

## Impact

Model switching is impossible on Android, and the crash interrupts whatever the user was typing.

Reported 2026-10-25. Crash log / device model would help if available.
