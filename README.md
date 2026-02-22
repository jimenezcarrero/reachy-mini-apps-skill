# Reachy Mini Apps Skill

Codex skill for building, debugging, and publishing Reachy Mini apps safely.

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
  --repo <github-user>/reachy-mini-apps-skill \
  --path skills/reachy-mini-apps
```

Option 2: using your `$skill-installer` command wrapper.

```bash
$skill-installer install https://github.com/<github-user>/reachy-mini-apps-skill/tree/main/skills/reachy-mini-apps
```

After installation:

```text
Restart Codex to pick up new skills.
```

## Publish This Repo

1. Create an empty GitHub repository named `reachy-mini-apps-skill`.
2. Push this local repo:

```bash
cd /tmp/reachy-mini-apps-skill
git init -b main
git add .
git commit -m "Add Reachy Mini Apps Codex skill"
git remote add origin https://github.com/<github-user>/reachy-mini-apps-skill.git
git push -u origin main
```

## Notes

- The skill content is intentionally compact and uses `references/` for progressive loading.
- This repository contains only the skill so it can be shared independently from app source code.
