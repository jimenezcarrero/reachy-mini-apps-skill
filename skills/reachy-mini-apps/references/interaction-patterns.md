# Interaction Patterns

Use this reference for physical UX patterns.

## Antennas as buttons

Antennas are useful as safe physical inputs.

Basic detection pattern:

```python
import time

ANTENNA_THRESHOLD = 0.3
DEBOUNCE_SECONDS = 0.25
last_press_t = 0.0

def detect_antenna_press(mini):
    global last_press_t
    _, antennas = mini.get_current_joint_positions()
    now = time.monotonic()
    if now - last_press_t < DEBOUNCE_SECONDS:
        return None
    left, right = antennas
    if abs(left) > ANTENNA_THRESHOLD:
        last_press_t = now
        return "left"
    if abs(right) > ANTENNA_THRESHOLD:
        last_press_t = now
        return "right"
    return None
```

## Head as controller

Use head orientation as joystick-like input for games and navigation.

- Extract yaw/pitch from current head pose.
- Normalize to `[-1, 1]`.
- Apply deadzone and rate limits before acting.

## No-GUI flow

Simple interaction sequence:

1. Signal ready state (antenna twitch or short move).
2. Wait for antenna press.
3. Start main loop.
4. Expose stop gesture/button.

## State signaling

Use visible motion cues:

- Ready: gentle antenna twitch
- Busy: slow oscillation
- Success: short double bounce
- Error: brief shake and return neutral

## Loop ownership

Even with many interaction inputs, keep one loop as the only place that sends target commands.

