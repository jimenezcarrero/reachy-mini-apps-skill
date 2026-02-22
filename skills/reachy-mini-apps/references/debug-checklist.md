# Debug Checklist

Use this order to isolate failures quickly.

## 1) Check daemon availability

```bash
curl -fsS http://localhost:8000/api/daemon/status
```

If this fails:
- Start daemon with `reachy-mini-daemon` or `reachy-mini-daemon --sim`.
- Confirm host/IP for Wireless target.

## 2) Verify basic motion

Run a minimal SDK script that only opens `ReachyMini()` and executes one `goto_target`.

## 3) Validate app package

```bash
reachy-mini-app-assistant check <app_path>
```

Fix entry points and metadata first if check fails.

## 4) Separate motion model issues

- If scripted motions fail, test only `goto_target`.
- If reactive behavior is jerky, enforce one-loop ownership for `set_target`.

## 5) Check logs

- Run daemon in a visible terminal with `--log-level DEBUG` when needed.
- Capture app stderr for traceback and last failing command.

## 6) Platform caveats

- Simulation cannot validate camera hardware behavior.
- Wireless local execution has tighter CPU and memory budgets.
