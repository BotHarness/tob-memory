## What happens

When the dsh-im plugin calls the DSH 0.2.1 gateway to create a session, the request body omits the `peer` object. The host fails its first validation line with `Cannot read properties of undefined (reading 'signal')`, wraps it as an internal error, and the plugin does not recognise that code, so it surfaces as `INTERNAL_UNKNOWN`.

Visible behaviour: QQ messages are received and can be marked read, but **no session can be created**, so the Bot never replies. It also means the default working directory has to be used, because customising it goes through the same path.

## Expected

- The request should include a `peer` object (or the host should validate it with a clear error instead of throwing on `undefined`).
- An unrecognised host error should not be flattened into `INTERNAL_UNKNOWN`; the plugin should surface the underlying message and code.
- Custom work paths should work once the request is well formed.

## Current workaround (community, unsupported)

Patch the plugin bundle in two places: inject the local owner peer into the gateway request, and force session creation through the `cwd` branch. After a restart QQ sessions can be created and replies work.

## Impact

QQ channel is unusable for anyone hitting this: no sessions, no replies, and the error text points at nothing actionable.

Reported with DSH 0.2.1 and the dsh-im plugin; platform QQ, OS (Windows or Linux) not captured.
