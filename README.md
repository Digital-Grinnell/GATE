# GATE

GATE is a Flet desktop workflow tool for preparing Alma-Digital ingest inputs from GCCB/CollectionBuilder deployments.

Primary objective:
- Select a GCCB deployment, such as https://black-sky-0a5891010.7.azurestaticapps.net/
- Build ingest-ready inputs for Alma-Digital
- Support import into the Pending Review collection:
  https://grinnell.primo.exlibrisgroup.com/discovery/collectionDiscovery?vid=01GCL_INST:GCL&collectionId=81313013130004641
- Support publishing workflows for https://digital.grinnell.edu

## Current Capabilities

- Persistent UI state in ~/FLAT-data/persistent.json
- Per-folder application settings in flat_settings.json
- Sensitive settings encryption (api_key, api_secret, password)
- Selectable GCCB deployment presets
- GCCB deployment URL validation (requires https and host)
- Save validated deployment URL to per-folder app settings
- Function-driven workflow model with help mode
- Status and log output with clipboard support

## Quick Run

macOS/Linux:

```bash
./run.sh
```

Windows:

```bat
run.bat
```

The launch scripts create a virtual environment, install dependencies, and run the app.

## Key Workflow

1. Choose Input Directory and Working/Output Directory.
2. In CollectionBuilder Deployment:
   - Choose a preset or enter a custom GCCB URL
   - Click Validate URL
   - Click Save Deployment to persist to flat_settings.json in the Working/Output Directory
3. Use functions to perform workflow steps and inspect status/log output.

## Settings Model

Settings are saved per Working/Output Directory in flat_settings.json.

Current keys include:
- auto_save_enabled
- auto_save_format
- api_key (encrypted)
- api_secret (encrypted)
- password (encrypted)
- gccb_deployment_url

Encryption key is stored in ~/FLAT-data/encryption_key.

## Project Files

- app.py: Main runtime application
- FUNCTION_0_APP_SETTINGS.md: Settings behavior and field definitions
- FUNCTION_1_LIST_FILES.md: Function 1 help
- FUNCTION_2_COUNT_FILES.md: Function 2 help
- FUNCTION_3_SYSTEM_INFO.md: Function 3 help
- QUICKSTART.md: Fast onboarding
- AGENTS.md: AI coding guidance
- HUMANS.md: Human prompting/review guidance

## Reference Repositories

Useful implementation references:
- https://github.com/Digital-Grinnell/common-DG-utilities
- https://github.com/Digital-Grinnell/manage-digital-ingest-flet-Alma

Reuse patterns thoughtfully and keep licensing/attribution expectations.

## Validation

```bash
python3 -m py_compile app.py
bash -n run.sh build_dmg.sh build_windows_zip.sh
```

## Roadmap Direction

Near-term work should prioritize:
- Metadata retrieval from selected GCCB deployment
- Mapping to Alma-Digital ingest structures
- Deterministic ingest file generation
- Better pre-ingest validation and reporting

## License

MIT License. See LICENSE or LICENSE.md.
