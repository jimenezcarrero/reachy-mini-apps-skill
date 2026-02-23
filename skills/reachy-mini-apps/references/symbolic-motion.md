# Symbolic Motion

Use this reference when moves are better defined by formulas than recordings.

## When to use

- Repeating rhythmic motion
- Parameterized dances
- Dynamic expressions driven by runtime inputs

## Concept

Model motion as functions of time:

- `yaw(t)`
- `pitch(t)`
- `roll(t)`
- `antenna_left(t)`, `antenna_right(t)`

Then evaluate at fixed frequency in a single control loop.

## Minimal pattern

```python
import math
import time
from reachy_mini.utils import create_head_pose

def symbolic_pose(t: float):
    yaw = 12.0 * math.sin(2 * math.pi * 0.25 * t)
    pitch = 4.0 * math.sin(2 * math.pi * 0.50 * t)
    return create_head_pose(yaw=yaw, pitch=pitch, degrees=True)

def run_symbolic(mini, stop_event):
    t0 = time.monotonic()
    while not stop_event.is_set():
        t = time.monotonic() - t0
        mini.set_target(head=symbolic_pose(t))
        time.sleep(0.01)
```

## Composition

Combine layers by summing small offsets:

1. Base pose
2. Breathing offset
3. Gaze or tracking offset
4. Expression offset

Apply clamps after composition.

## Timing

Use `time.monotonic()` for phase stability.
Avoid wall-clock time to prevent jumps due to NTP or system clock adjustments.

