# Source Map

Use these files as source of truth when answers must be exact.

- Main SDK class and signatures:
  - `src/reachy_mini/reachy_mini.py`
- App base class and assistant CLI:
  - `src/reachy_mini/apps/app.py`
  - `src/reachy_mini/apps/assistant.py`
- App runtime management:
  - `src/reachy_mini/apps/manager.py`
- Daemon API entry point:
  - `src/reachy_mini/daemon/app/main.py`
- Movement API router:
  - `src/reachy_mini/daemon/app/routers/move.py`
- State API router:
  - `src/reachy_mini/daemon/app/routers/state.py`
- Pose and interpolation helpers:
  - `src/reachy_mini/utils/__init__.py`
  - `src/reachy_mini/utils/interpolation.py`
- Official AI-agent guidance in repo:
  - `agents.md`
  - `skills/*.md`
