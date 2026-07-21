<div align="center">

# helipod

**The open-source, self-hostable reactive backend.**

Write TypeScript functions. Get a transactional database, live-updating queries,
auth, file storage, scheduling, and durable workflows — on your own infrastructure.

</div>

---

```ts
// helipod/messages.ts
export const send = mutation({
  args: { channel: v.id("channels"), body: v.string() },
  handler: async (ctx, { channel, body }) => {
    await ctx.db.insert("messages", { channel, body });
  },
});

// Every subscribed client sees the new message instantly. No polling, no cache juggling.
const messages = useQuery(api.messages.list, { channel });
```

## Why helipod

- ⚡ **Reactive by default** — queries are live subscriptions; when data changes, connected clients are pushed fresh results over WebSocket
- 🔒 **Transactional** — every mutation is one serializable transaction with optimistic concurrency
- 🧰 **Batteries included** — auth (OAuth, passkeys, MFA), file storage, crons, durable workflows with compensation, triggers, notifications
- 📴 **Offline-ready client** — optimistic updates and a durable outbox with exactly-once replay
- 📦 **Deploy anywhere** — `docker compose up`, a single compiled binary, or your own Postgres; SQLite for zero-config local dev
- 🔓 **No lock-in** — your data, your infra, fully portable

## Get started

| | |
|---|---|
| 🚀 **[helipod](https://github.com/helipod-sh/helipod)** | The monorepo — engine, CLI, client SDK, dashboard, and docs |

```bash
bun add -g @helipod/cli   # or: npm i -g @helipod/cli
helipod dev               # local engine + dashboard + hot reload
```

## License

Free to use and self-host under [FSL-1.1-Apache-2.0](https://fsl.software) — converts to Apache 2.0 after two years.
