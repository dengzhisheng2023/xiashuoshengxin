# xiashuoshengxin

biomadic

## OpenClaw dashboard remote access

When `openclaw dashboard` is started on a remote host without GUI/clipboard support, token auto-auth may not be delivered automatically. In that case:

1. Create the SSH tunnel:

   ```bash
   ssh -N -L 18789:127.0.0.1:18789 <user>@<remote-host>
   ```

2. Open the dashboard locally and append the gateway token as a URL fragment:

   ```
   http://localhost:18789/#token=<OPENCLAW_GATEWAY_TOKEN>
   ```

This ensures authentication still works when the automatic browser/clipboard token handoff is unavailable.

### Why the token is not shown every time

`openclaw dashboard` can only auto-deliver the token when the runtime can open/copy the auth URL successfully. If you see messages like `Copy to clipboard unavailable`, `No GUI detected`, or `Token auto-auth not delivered`, this is expected in remote/headless sessions.

If startup logs show both `Token auto-auth included in browser/clipboard URL.` and later `Token auto-auth not delivered.`, treat the final result as **not delivered** and use manual URL fragment auth.

### How to make auto token login more likely next time

Automatic token display/login works best when `openclaw dashboard` runs in a local desktop session (with GUI + clipboard/browser access) on the same machine where you open the dashboard.

If you want the browser to auto-open and auto-login next time, avoid SSH/headless startup and run it directly in your local desktop terminal.

For SSH/headless remote sessions, auto-delivery is not guaranteed; keep using:

```text
http://localhost:18789/#token=<OPENCLAW_GATEWAY_TOKEN>
```

Use the token from `OPENCLAW_GATEWAY_TOKEN` (or `gateway.auth.token`) and append it manually:

```text
http://localhost:18789/#token=<your-token>
```
