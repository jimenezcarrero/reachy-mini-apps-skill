# Testing Apps

Use this reference before publishing or handing off an app.

## Test target matrix

Always state what was tested:

- Lite vs Wireless vs Simulation
- Local vs remote control path
- Camera/audio used or not used

## Preflight

1. Daemon is running.
2. App installs and entrypoints validate.
3. Basic movement command succeeds.

## Minimum smoke test

```bash
reachy-mini-app-assistant check <app_path>
```

Run the app briefly and verify:

- no immediate crash
- no repeated traceback spam
- stop path exits cleanly

## Behavior checks

- Motion smoothness and responsiveness
- Antenna input debounce and false trigger rate
- Recovery from temporary sensor or network interruption

## Simulation limits

Simulation is useful for logic and API checks, but does not fully validate:

- Real camera behavior
- Real microphone/speaker latency
- Physical interaction dynamics

## Release gate

Before release, confirm:

1. Tested environments are listed.
2. Known limitations are documented.
3. Failure modes and recovery path are documented.

