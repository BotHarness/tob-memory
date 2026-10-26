## What happens

On a self-hosted QQ channel, two shapes of inbound loss have been reported in the same group:

1. **Quote + mention.** User A posts a message; user B quotes A's message **and** @s the Bot in the same message. The Bot never receives it; nothing appears in its Inbox.
2. **Empty body.** A member @s the Bot and the received message has no text at all — the Bot gets an envelope with no user input, so it cannot answer.

Both look like bridge-side (dsh-im) losses rather than model behaviour: in case 1 nothing is admitted at all, and in case 2 an admission arrives with the content stripped.

## Expected

- A quote-plus-mention message should be admitted like any other mention, with the quoted context available.
- If a message arrives without text, that should be visible as a malformed admission rather than an empty turn.

## Impact

Messages silently vanish, so users conclude the Bot is ignoring them or is broken; case 2 additionally burns a turn with nothing to work on.

Reported from a QQ group in late October; exact dsh-im and client versions not captured.
