# Setup Environment

Use this reference for first-time local setup.

## Quick prerequisite check

```bash
git --version
python3 --version
pip --version
```

Optional fast path:

```bash
uv --version
```

## Recommended workspace

Use a persistent folder, for example:

```bash
mkdir -p ~/reachy_mini_resources
cd ~/reachy_mini_resources
```

## Create environment

With `uv`:

```bash
uv venv .venv
source .venv/bin/activate
uv pip install "reachy-mini"
```

With standard `venv`:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install "reachy-mini"
```

## Platform caveats

- Wireless from a laptop/desktop may need GStreamer packages for stable remote media.
- Lite on Linux may require USB serial permissions (`udev` rules and `dialout` group).
- Simulation validates logic and APIs well, but does not fully represent real media latency or physical interaction.

## Clone core references

```bash
git clone https://github.com/pollen-robotics/reachy_mini
git clone https://github.com/pollen-robotics/reachy_mini_conversation_app
git clone https://github.com/pollen-robotics/reachy_mini_dances_library
```

## Verify install

```bash
python3 -c "from reachy_mini import ReachyMini; print('ok')"
```

## Persist local context

Create `agents.local.md` in your active project with:

- Robot type (`Lite`, `Wireless`, or `None`)
- OS and shell
- Python environment tool
- Resource folder path
