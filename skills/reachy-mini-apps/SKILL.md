---
name: reachy-mini-apps
description: Build, debug, and publish Reachy Mini applications with the official SDK, daemon, and app assistant. Use when tasks involve Reachy Mini Lite, Wireless, or Simulation app creation, motion design (`goto_target` vs `set_target`), safe motor torque handling, REST or WebSocket control, or troubleshooting connectivity and runtime issues.
---

# Reachy Mini Apps

Build Reachy Mini apps with the official workflows and safety patterns.

## First checks

- Ask which target is in scope: `Lite`, `Wireless`, or `Simulation`.
- Confirm daemon availability before coding behaviors.
- Prefer app scaffolding with `reachy-mini-app-assistant`; do not handcraft app folders.

## Route by task

- For create, check, and publish workflows, read `references/app-lifecycle.md`.
- For motion architecture, control loops, and torque safety, read `references/motion-control.md`.
- For non-Python or remote control, read `references/api-endpoints.md`.
- For connectivity and runtime failures, read `references/debug-checklist.md`.
- For canonical source entry points, read `references/source-map.md`.

## Non-negotiables

- Use Python app templates for app-store compatible apps.
- Keep exactly one control loop as the only place that calls `set_target`.
- Use `goto_target` for scripted gestures and transitions.
- Move to a safe pose before disabling motors.
- Sync target to current pose before enabling motors to avoid jumps.
- Verify method signatures in source before using an SDK function.

## Standard commands

```bash
# Create app (default template)
reachy-mini-app-assistant create <app_name> <path> --publish

# Create app (conversation template)
reachy-mini-app-assistant create --template conversation <app_name> <path> --publish

# Validate app package and metadata
reachy-mini-app-assistant check <app_path>

# Start daemon
reachy-mini-daemon
reachy-mini-daemon --sim
```

## Delivery checklist

- Confirm hardware and connection assumptions.
- Confirm whether tests ran on physical robot, simulation, or both.
- Keep safety limits explicit when proposing motion.
- State what was validated and what remains untested.
