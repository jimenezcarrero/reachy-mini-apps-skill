# AI Integration

Use this reference when building LLM-powered Reachy Mini apps.

## When to use

- Voice assistants
- Tool-calling robot apps
- Realtime LLM integrations
- Profile-based personalities

## Core architecture rule

Do not let the LLM drive motors directly.

Use this flow:

1. LLM decides intent.
2. LLM tool enqueues a robot action.
3. Control loop executes robot motion safely.

This avoids race conditions and keeps behavior smooth when model latency spikes.

## Tool design pattern

Tools should be short, deterministic, and side-effect limited.

```python
from queue import Queue

actions = Queue()

def tool_move_head(yaw: float, pitch: float, duration: float = 1.0) -> str:
    actions.put({"type": "goto", "yaw": yaw, "pitch": pitch, "duration": duration})
    return "Head move queued."
```

In the runtime loop, consume queue actions and map them to `goto_target` or `set_target`.

## Profile strategy

Separate behavior by profile, not by branching inside the main loop:

- Instructions per persona
- Enabled tool list per persona
- Safety constraints in every profile

## Realtime API notes

- Keep tool outputs compact.
- Handle interrupt/retry explicitly.
- Guard long actions so they can be canceled.
- Return structured failure messages to the model.

## Safety checks

- Clamp target ranges before enqueue.
- Reject impossible command combinations.
- Keep one loop as the only motion writer.

