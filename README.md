# pi-pending

Small Pi TUI helper for rendering forced one-line pending-operation rows above
the editor.

```ts
import { createPiPending } from "pi-pending";

const pending = createPiPending({ namespace: "zcouncil" });

pi.on("session_start", (_event, ctx) => {
  if (ctx.hasUI) pending.attach(ctx.ui);
});

pending.start({
  id: "job_1",
  label: "Claude",
  text: "roast this architecture plan",
  details: { timeoutMs: 120_000 },
});

pending.finish("job_1");
```

Default visible row:

```txt
(003s) Claude: roast this architecture plan
```

Details stay in metadata; only elapsed seconds, label, and text are visible.
Rows are always normalized to one terminal line, truncated to width, padded to
width, and styled with Pi's `toolPendingBg` + `toolTitle` theme colors.
