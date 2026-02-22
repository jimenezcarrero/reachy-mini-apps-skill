# App Lifecycle

Use this flow for any new Reachy Mini app.

## 1) Create

Prefer non-interactive commands in automation contexts:

```bash
reachy-mini-app-assistant create <app_name> <path> --publish
```

Use conversation template only when LLM, speech, or profile tooling is required:

```bash
reachy-mini-app-assistant create --template conversation <app_name> <path> --publish
```

Notes:
- Provide both `<app_name>` and `<path>` to avoid interactive prompts.
- Use `--private` if the Space must not be public.
- Run `hf auth login` first when using `--publish`.

## 2) Expected structure

```text
my_app/
├── index.html
├── style.css
├── pyproject.toml
├── README.md
├── .gitignore
└── my_app/
    ├── __init__.py
    ├── main.py
    └── static/
        ├── index.html
        ├── style.css
        └── main.js
```

## 3) Validate before publish

```bash
reachy-mini-app-assistant check <app_path>
```

Validation should confirm:
- Valid `pyproject.toml` and app entry point.
- Expected package and class naming.
- Required metadata tags in `README.md`.

## 4) Update and publish existing app

```bash
reachy-mini-app-assistant publish <app_path> "<commit message>"
```

Optional flags:
- `--nocheck` to skip checks (avoid unless necessary).
- `--private` or `--public` to force visibility.
- `--official` to request app-store inclusion workflow.
