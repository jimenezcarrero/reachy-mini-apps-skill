# Reachy Mini Apps Skill

Repository containing a **Codex skill** for building, debugging, and publishing Reachy Mini apps safely.

## Codex Skill Context

This repository is designed for Codex skill installation and usage.

For official skill concepts and format, see:
- https://developers.openai.com/codex/skills

## What This Skill Covers

- Reachy Mini app creation with official `reachy-mini-app-assistant` workflows.
- Motion architecture (`goto_target` vs `set_target`) and control-loop patterns.
- Safe motor torque handling to avoid jumps and unstable behavior.
- REST/WebSocket endpoint references for non-Python clients.
- Troubleshooting checklist for daemon, app, and runtime issues.

## Repository Layout

```text
.
├── README.md
└── skills/
    └── reachy-mini-apps/
        ├── SKILL.md
        ├── agents/openai.yaml
        └── references/
            ├── api-endpoints.md
            ├── app-lifecycle.md
            ├── debug-checklist.md
            ├── motion-control.md
            └── source-map.md
```

## Install

Option 1: using the installer script directly.

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo jimenezcarrero/reachy-mini-apps-skill \
  --path skills/reachy-mini-apps
```

Option 2: using your `$skill-installer` command wrapper.

```bash
$skill-installer install https://github.com/jimenezcarrero/reachy-mini-apps-skill/tree/main/skills/reachy-mini-apps
```

After installation:

```text
Restart Codex to pick up new skills.
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

## Notes

- The skill content is intentionally compact and uses `references/` for progressive loading.
- This repository contains only the skill so it can be shared independently from app source code.
