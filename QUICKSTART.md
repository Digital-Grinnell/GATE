# GATE Quick Start

GATE prepares Alma-Digital ingest inputs from a selected GCCB/CollectionBuilder deployment.

## 1) Launch

macOS/Linux:

```bash
cd /Users/mcfatem/GitHub/GATE
./run.sh
```

Windows:

```bat
cd \path\to\GATE
run.bat
```

## 2) Choose folders

- Set Input Directory.
- Set Working/Output Directory.

The Working/Output Directory stores per-project settings in gate_settings.json.

## 3) Select deployment

In CollectionBuilder Deployment:

1. Enter the deployment URL.
2. Click Validate URL.
3. Click Save Deployment.

Save Deployment writes gccb_deployment_url into gate_settings.json in the selected Working/Output Directory.

## 4) Use functions

- Function 0: App Settings (includes encrypted sensitive fields and deployment URL setting)
- Function 1: List Files
- Function 2: Count Files by Extension
- Function 3: System Information

Enable Help Mode to view FUNCTION_*.md documentation instead of executing functions.

## 5) Check status and logs

- Use Status output for immediate feedback.
- Use Log Output for timestamped actions.
- Runtime logs are saved under ~/GATE-data/logfiles/.

## Validation Commands

```bash
python3 -m py_compile app.py
bash -n run.sh build_dmg.sh build_windows_zip.sh
```

## Alma-Digital Context

Target collection for ingest review:
https://grinnell.primo.exlibrisgroup.com/discovery/collectionDiscovery?vid=01GCL_INST:GCL&collectionId=81313013130004641

Destination environment:
https://digital.grinnell.edu

Example GCCB deployment:
https://black-sky-0a5891010.7.azurestaticapps.net/
