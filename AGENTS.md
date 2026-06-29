# GATE - AI Agent Instructions

GATE is a Flet desktop workflow app used to prepare ingest inputs for Alma-Digital from GCCB/CollectionBuilder deployments.

Primary purpose:
- Allow selection of a GCCB CollectionBuilder deployment, for example https://black-sky-0a5891010.7.azurestaticapps.net/
- Generate Alma-Digital-ready ingest inputs so collection objects can be imported into the Pending Review collection at https://grinnell.primo.exlibrisgroup.com/discovery/collectionDiscovery?vid=01GCL_INST:GCL&collectionId=81313013130004641
- Support ingest preparation for https://digital.grinnell.edu

Companion guide:
- HUMANS.md is the human-facing workflow and prompting guide.

## Product Direction

When proposing or implementing changes, prioritize work that strengthens this pipeline:

1. Select GCCB deployment (URL, validation, persistence)
2. Retrieve or map deployment object metadata
3. Transform/map metadata to Alma-Digital ingest shape
4. Produce repeatable output files for ingest staging and review
5. Keep process transparent with logs, status, and recoverable settings

Do not treat this project as a generic template unless explicitly requested.

## External Reference Repositories

Use these as implementation references when needed:
- https://github.com/Digital-Grinnell/common-DG-utilities
- https://github.com/Digital-Grinnell/manage-digital-ingest-flet-Alma

Guidance for reuse:
- Prefer adapting patterns and data mapping logic over direct copy/paste.
- Preserve licensing and attribution requirements for reused code or text.
- Keep this repo's behavior and naming consistent even when borrowing ideas.

## Change Priority Order

Make the smallest change at the highest appropriate layer first:

1. FUNCTION_*.md, README.md, QUICKSTART.md, and related docs
2. Launch/packaging scripts (run.sh, run.bat, build_dmg.sh, build_windows_zip.sh)
3. python_requirements.txt for dependency changes
4. app.py for runtime behavior and UI
5. Backup or generated artifacts only if explicitly requested

If the issue is wording, workflow explanation, or help text, do not edit app.py first.

## Source Of Truth And Scope

- Treat app.py as the active runtime source.
- Do not edit app.py.bak, app_from_ohm.py, or app_ohm_full.py unless explicitly requested.
- Keep behavior docs synchronized with visible UI/runtime behavior.

## Settings, Security, And Data Handling

- Function 0 settings are per working/output folder in gate_settings.json.
- Sensitive fields are encrypted by app logic; do not weaken or remove that behavior casually.
- Do not hardcode credentials, API keys, or environment-specific secrets.
- Runtime state/logs are stored outside the repo under ~/GATE-data/.
- Do not treat runtime artifacts as repository source files.

## Function Documentation Sync

When changing function behavior, update matching docs in the same change:
- FUNCTION_0_APP_SETTINGS.md
- FUNCTION_1_LIST_FILES.md
- FUNCTION_2_COUNT_FILES.md
- FUNCTION_3_SYSTEM_INFO.md

If new ingest-oriented functions are added, create matching FUNCTION_X_*.md files.

## Ask Before These Changes

Explain plan and ask for confirmation before:
- Refactoring large sections of app.py for a small behavior tweak
- Changing encryption handling for settings
- Renaming function IDs/labels that affect existing documentation or workflow
- Broad dependency upgrades with packaging/runtime impact
- Deleting historical or backup files

## Definition Of Done For Workflow Features

A workflow feature is complete when all are true:
- User can select or enter a deployment target clearly.
- Validation/error messages are actionable.
- Generated outputs are deterministic and stored in the selected working/output folder.
- Status/log output clearly states what was generated and where.
- Relevant FUNCTION_*.md and onboarding docs are updated.

## Validation

Use focused validation for touched areas:

```bash
python3 -m py_compile app.py
bash -n run.sh build_dmg.sh build_windows_zip.sh
```

For docs-only edits, focused diff review is sufficient.

## Working Instructions

1. Confirm whether request is docs, runtime behavior, packaging, or dependencies.
2. Read the nearest relevant files before broad edits.
3. Prefer minimal changes and preserve existing function model unless asked to restructure.
4. Keep docs and runtime behavior aligned.
5. Validate the changed slice before finishing.
