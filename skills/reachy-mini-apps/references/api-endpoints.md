# REST and WebSocket Endpoints

Use these endpoints when building web UIs or non-Python clients.

## Base URL

- Lite local daemon: `http://localhost:8000/api`
- Wireless daemon: `http://reachy-mini.local:8000/api` (or robot IP)

Interactive API docs:
- `http://<daemon-host>:8000/docs`

## Movement

- `POST /move/goto`
- `POST /move/set_target`
- `POST /move/play/wake_up`
- `POST /move/play/goto_sleep`
- `POST /move/stop`

## State

- `GET /state/full`
- `GET /state/present_head_pose`
- `GET /state/present_body_yaw`
- `GET /state/present_antenna_joint_positions`
- `GET /state/doa`

## Motor mode

- `GET /motors/status`
- `POST /motors/set_mode/{mode}` where mode is one of:
  - `enabled`
  - `disabled`
  - `gravity_compensation`

## WebSocket streams

- `ws://<daemon-host>:8000/api/state/ws/full`
- `ws://<daemon-host>:8000/api/move/ws/updates`
- `ws://<daemon-host>:8000/api/move/ws/set_target`

## SDK vs REST rule

- Prefer Python SDK for tight control loops and advanced media behaviors.
- Prefer REST/WebSocket for browser clients, dashboards, and non-Python stacks.
