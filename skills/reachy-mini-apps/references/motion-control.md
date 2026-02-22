# Motion Control

Use this decision rule first:

- Use `goto_target()` for scripted, smooth transitions.
- Use `set_target()` only inside a high-frequency control loop for reactive behavior.

## Default path: goto_target

Use for gestures, choreography, and state transitions.

```python
from reachy_mini import ReachyMini
from reachy_mini.utils import create_head_pose

with ReachyMini() as mini:
    pose = create_head_pose(yaw=20, pitch=8, degrees=True)
    mini.goto_target(head=pose, duration=1.0)
```

## Reactive path: set_target in one loop

Keep a single control loop as the only writer of robot targets.

```python
import time
from reachy_mini import ReachyMini
from reachy_mini.utils import create_head_pose

with ReachyMini() as mini:
    while True:
        pose = create_head_pose(yaw=10, pitch=0, degrees=True)
        mini.set_target(head=pose)
        time.sleep(0.01)  # ~100 Hz
```

## Torque safety

Before disabling motors, move to a safe pose (for example sleep pose).

Before enabling motors:
1. Read current pose and antennas.
2. Set goal to current values with very short duration.
3. Then enable motors.

This avoids sudden jumps when torque is re-enabled.

## Interpolation note

Prefer SDK enum constants instead of string literals for interpolation mode.
This avoids naming drift between docs/comments and implementation values.
