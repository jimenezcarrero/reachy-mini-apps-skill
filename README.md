<div align="center">
  <h1>Reachy Mini Apps Skill for Codex</h1>
  <img src="Reachy_mini_Codex_skill.png" alt="Reachy Mini Codex Skill" width="760" />
</div>

<p align="center">
  <strong>Codex-installable skill for building, debugging, and publishing Reachy Mini apps with official SDK and daemon workflows.</strong>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg" alt="License"></a>
  <a href="https://developers.openai.com/codex/skills"><img src="https://img.shields.io/badge/Codex-Skills-black.svg" alt="Codex Skills"></a>
  <a href="https://github.com/pollen-robotics/reachy_mini"><img src="https://img.shields.io/badge/Reachy%20Mini-SDK-orange.svg" alt="Reachy Mini SDK"></a>
</p>

---

## Codex Skill Context

This repository is focused on a single Codex skill at:

- `skills/reachy-mini-apps`

It is structured for installation through Codex skill tooling, not as a full robot app/source monorepo.

Codex skill format and behavior reference:

- https://developers.openai.com/codex/skills

## Install in Codex

Option 1, install with the official installer script:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo jimenezcarrero/reachy-mini-apps-skill \
  --path skills/reachy-mini-apps
```

Option 2, install with your `$skill-installer` wrapper:

```bash
$skill-installer install https://github.com/jimenezcarrero/reachy-mini-apps-skill/tree/main/skills/reachy-mini-apps
```

After installation, restart Codex to load new skills.

## How to Get Good Results

When asking Codex to use `$reachy-mini-apps`, include:

- Robot target: `Lite`, `Wireless`, or `Simulation`
- Current issue or goal in one sentence
- Whether you want app scaffolding, debugging, or pre-release checks

Prompt template:

```text
Use $reachy-mini-apps. I am using <Lite/Wireless/Simulation>. My goal is <goal>. Please give exact commands and a safe step-by-step plan.
```

## Practical Prompt Examples

1. Create a new app

```text
Use $reachy-mini-apps. I am using Reachy Mini Wireless. Create a new app named "hello_reachy" with the official app assistant, then give me exact commands to check and publish it.
```

2. Fix jerky movement

```text
Use $reachy-mini-apps. My app movement is jerky and I suspect bad set_target usage. Show me how to refactor to a single control loop and keep scripted gestures on goto_target.
```

3. Add camera-driven behavior safely

```text
Use $reachy-mini-apps. Add a camera-based behavior that tracks a person, but keep motion smooth and include safe motor enable/disable handling.
```

4. Validate before release

```text
Use $reachy-mini-apps. Build a practical release checklist for Lite and Simulation, including commands, expected outputs, and how to recover from common failures.
```

5. Build a browser client

```text
Use $reachy-mini-apps. I want a small web dashboard that controls head and antennas through REST/WebSocket. Propose endpoints, flow, and a minimal architecture.
```

## What This Skill Covers

- App creation, checking, and publishing with `reachy-mini-app-assistant`
- Motion architecture (`goto_target` vs `set_target`)
- Safe motor torque handling
- REST and WebSocket endpoint usage
- Quick command/snippet lookup for common tasks
- Camera/audio/IMU handling patterns for app flows
- AI integration patterns for Reachy Mini apps
- Interaction patterns (antennas as buttons, head-as-controller)
- Symbolic motion composition
- Setup and testing checklists
- Debug workflow and source mapping

## When to Use Upstream Docs

This skill is focused on getting apps built and shipped quickly.

If you need complete low-level SDK coverage, detailed hardware internals, or broader API material, use the official Reachy Mini repositories and docs listed in Data Sources.

## Skill References

| File | Purpose |
|------|---------|
| `skills/reachy-mini-apps/SKILL.md` | Entry instructions and routing |
| `skills/reachy-mini-apps/references/app-lifecycle.md` | Create/check/publish workflows |
| `skills/reachy-mini-apps/references/motion-control.md` | Motion, control loops, torque safety |
| `skills/reachy-mini-apps/references/api-endpoints.md` | REST/WebSocket endpoint map |
| `skills/reachy-mini-apps/references/api-quick-reference.md` | Fast SDK/REST command lookup |
| `skills/reachy-mini-apps/references/sensors-media.md` | Camera/audio/IMU usage patterns |
| `skills/reachy-mini-apps/references/debug-checklist.md` | Troubleshooting sequence |
| `skills/reachy-mini-apps/references/ai-integration.md` | LLM and tool-calling patterns |
| `skills/reachy-mini-apps/references/interaction-patterns.md` | Physical interaction design |
| `skills/reachy-mini-apps/references/symbolic-motion.md` | Formula-based move design |
| `skills/reachy-mini-apps/references/setup-environment.md` | First-run machine setup |
| `skills/reachy-mini-apps/references/testing-apps.md` | Pre-release validation |
| `skills/reachy-mini-apps/references/source-map.md` | Canonical source file map |

## Repository Layout

```text
.
├── .gitignore
├── LICENSE
├── NOTICE
├── README.md
├── Reachy_mini_Codex_skill.png
└── skills/
    └── reachy-mini-apps/
        ├── SKILL.md
        ├── agents/openai.yaml
        └── references/
            ├── ai-integration.md
            ├── api-endpoints.md
            ├── api-quick-reference.md
            ├── app-lifecycle.md
            ├── debug-checklist.md
            ├── interaction-patterns.md
            ├── motion-control.md
            ├── sensors-media.md
            ├── setup-environment.md
            ├── source-map.md
            ├── symbolic-motion.md
            └── testing-apps.md
```

## Data Sources

This skill was authored from the following public sources:

- Reachy Mini official repository (SDK, daemon, examples):
  https://github.com/pollen-robotics/reachy_mini
- Reachy Mini agent guidance (`agents.md`):
  https://github.com/pollen-robotics/reachy_mini/blob/develop/agents.md
- Reachy Mini in-repo skill references (`skills/*.md`):
  https://github.com/pollen-robotics/reachy_mini/tree/develop/skills
- Reachy Mini official documentation:
  https://huggingface.co/docs/reachy_mini
- OpenAI Codex Skills documentation/spec:
  https://developers.openai.com/codex/skills
- OpenAI skills installer reference repository:
  https://github.com/openai/skills

## Inspiration

This Codex skill was inspired by the Claude-oriented Reachy Mini skill project:

- https://github.com/jjmartres/reachy-mini-sdk-skill

This repository adapts that idea for Codex installation and Codex-oriented workflows.

## License

Licensed under **Apache License 2.0**. See `LICENSE`.

Attribution notices for adapted guidance are listed in `NOTICE`.
