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
