## What happens

QQ private chat is one-way. The Bot receives the message and produces a reply, but the reply never reaches QQ: the user sees nothing.

- Phone side: "connection failed"
- DSH side: reply generated, delivery not confirmed
- After restarting DSH the symptom can worsen: inbound stops working too, so nothing arrives at all.

## Expected

If a reply cannot be delivered, the Bot side should record a visible failure (and ideally retry once). Silence on both sides makes "reply lost" indistinguishable from "Bot offline" or "out of quota".

## Impact

Users conclude the Bot is broken; some reinstall. Reported 2026-10-24/25 on a self-hosted QQ channel.
