## What happens

On Android (App 1.5.2, Tobs Connect), turning the VPN off and back on breaks the existing pairing with the desktop. The phone cannot reconnect until it is paired with the desktop again.

- Platform: Android
- App version: 1.5.2
- Network: third-party "airport" (subscription proxy) VPN

## Expected

Pairing should survive a network change. Switching VPN on/off, or moving between Wi-Fi and cellular, should at worst require a retry or a re-handshake — not a fresh pairing.

## Suspected cause (not verified)

Pairing may bind to the connection address or session key captured at pair time, so a changed egress IP invalidates it, with no automatic re-negotiation. Alternatively the handshake times out and is never retried.

## Steps to reproduce

1. Pair the phone with the desktop (Tobs Connect) while the VPN is on.
2. Turn the VPN off, then on again.
3. Try to connect from the phone: it fails until re-paired.

## Impact

Users who keep a proxy on permanently cannot move between networks without re-pairing; on a flaky line this effectively means every session needs re-pairing.

Reported 2026-10-25. VPN client/protocol and phone model not captured yet.
