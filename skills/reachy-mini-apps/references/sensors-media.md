# Sensors and Media

Use this reference for camera, microphone, speaker, and IMU handling in apps.

## Camera

```python
from reachy_mini import ReachyMini

with ReachyMini(media_backend="default") as mini:
    frame = mini.media.get_frame()
    # numpy array, BGR order
```

Notes:

- Frames are usually BGR (`cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)` for RGB models).
- Avoid expensive processing directly in the motion control loop.

## Microphone

```python
samples = mini.media.get_audio_sample()
# float32 array, usually stereo at 16kHz
```

Useful checks:

```python
in_rate = mini.media.get_input_audio_samplerate()
out_rate = mini.media.get_output_audio_samplerate()
```

## Speaker Output

```python
mini.media.push_audio_sample(samples)
```

Use non-blocking playback carefully: if your app needs sync behavior,
track duration from sample count and sample rate.

## IMU (Wireless Only)

```python
if hasattr(mini, "imu"):
    imu = mini.imu.get_data()
    accel = imu.acceleration
    gyro = imu.gyroscope
    orient = imu.orientation
```

If IMU is absent, you are likely on Lite or simulation.

## Media Backend Notes

- `default`: good default for local development.
- `webrtc`: typically used in remote/Wireless setups.
- `gstreamer`: useful for advanced streaming pipelines.

Pick one backend and keep it stable for a run; dynamic switching mid-session can
make timing/debugging harder.

## App Design Rules

- Keep one owner loop for `set_target` (motion loop only).
- Process camera/audio in separate worker loops when possible.
- Add timeouts/retries around media reads for unstable links.
- Degrade gracefully when camera or audio temporarily fails.

## Minimal Pattern

```python
from reachy_mini import ReachyMini
from reachy_mini.utils import create_head_pose

with ReachyMini(localhost_only=False, media_backend="default") as mini:
    frame = mini.media.get_frame()
    # decide behavior from frame/audio
    mini.goto_target(head=create_head_pose(z=5, mm=True), duration=0.6)
```
