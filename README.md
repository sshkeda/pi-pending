# pi-pending

Tiny Pi TUI helper for one-line pending job widgets above the editor.

Use `pi-pending` from Pi extensions that start background jobs, multi-model requests, long-running tasks, or any asynchronous operation that should stay visible while the agent continues working.

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

## Install

Use as a GitHub dependency from another Pi package:

```json
{
  "dependencies": {
    "pi-pending": "github:sshkeda/pi-pending#v0.1.1"
  }
}
```

## Development

```bash
npm install
npm test
```

## License

MIT
