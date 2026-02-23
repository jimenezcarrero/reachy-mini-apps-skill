# API Quick Reference

Fast lookup for common Reachy Mini app actions.

## Connect

```python
from reachy_mini import ReachyMini

# Lite/local daemon
with ReachyMini() as mini:
    pass

# Wireless/remote daemon
with ReachyMini(localhost_only=False) as mini:
    pass
```

## Motion Basics

```python
import numpy as np
from reachy_mini.utils import create_head_pose

# Smooth movement for scripted gestures
mini.goto_target(
    head=create_head_pose(z=10, mm=True),
    antennas=np.deg2rad([30, 30]),
    duration=1.0,
    method="minjerk",
)

# Direct target updates for control loops only
mini.set_target(
    head=create_head_pose(yaw=5, degrees=True),
    antennas=np.deg2rad([5, -5]),
)
```

## Motor Mode

Prefer safe pose transitions before disabling motors.

```bash
# Get status
curl http://localhost:8000/api/motors/status

# Enable active control
curl -X POST http://localhost:8000/api/motors/set_mode/enabled

# Disable (compliant)
curl -X POST http://localhost:8000/api/motors/set_mode/disabled

# Gravity compensation
curl -X POST http://localhost:8000/api/motors/set_mode/gravity_compensation
```

## REST Movement

```bash
# Smooth move
curl -X POST http://localhost:8000/api/move/goto \
  -H 'Content-Type: application/json' \
  -d '{
    "duration": 1.0,
    "interpolation": "minjerk",
    "body_yaw": 0.2
  }'

# Stop current move
curl -X POST http://localhost:8000/api/move/stop
```

## State Endpoints

```bash
curl http://localhost:8000/api/state/full
curl http://localhost:8000/api/state/present_head_pose
curl http://localhost:8000/api/state/present_antenna_joint_positions
```

## WebSocket Streams

- `ws://<daemon-host>:8000/api/state/ws/full`
- `ws://<daemon-host>:8000/api/move/ws/updates`
- `ws://<daemon-host>:8000/api/move/ws/set_target`

## App Workflow Commands

```bash
# Create app
reachy-mini-app-assistant create <app_name> <path> --publish

# Validate app metadata/package
reachy-mini-app-assistant check <app_path>

# Start daemon (hardware)
reachy-mini-daemon

# Start daemon (simulation)
reachy-mini-daemon --sim
```

## Debug Fast Path

1. Confirm daemon is up: `curl http://localhost:8000/docs`
2. Verify one basic `goto` succeeds.
3. If motion is jerky, check for multiple `set_target` loops.
4. If jumps occur after enable, sync target to present pose first.
