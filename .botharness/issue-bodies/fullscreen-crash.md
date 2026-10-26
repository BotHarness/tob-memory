## What happens

On desktop, the window crashes when it is in full screen. In windowed mode the same content works fine.

- Reported on 2026-10-24.
- Suspected cause (community): GPU/compositor acceleration during fullscreen.

## Expected

Full screen and windowed mode should behave the same; a crash should leave a readable log entry instead of a silent exit.

## Next evidence needed

OS, GPU/driver, whether disabling hardware acceleration changes the outcome, and the crash log.

## Impact

Full screen is unusable; users are forced into windowed mode.
