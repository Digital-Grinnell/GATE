# HUMANS.md - Working With AI On GATE

This guide is for project maintainers and contributors. AGENTS.md is the companion file for AI coding assistants.

Use this file to define intent, write high-quality prompts, and review whether edits support the actual product goal.

## Project Purpose

GATE exists to support digital ingest preparation for Digital Grinnell.

Primary workflow:
1. Select a GCCB CollectionBuilder deployment, for example https://black-sky-0a5891010.7.azurestaticapps.net/
2. Build ingest-ready inputs for Alma-Digital from the selected deployment's objects/metadata
3. Import those objects into Pending Review:
	https://grinnell.primo.exlibrisgroup.com/discovery/collectionDiscovery?vid=01GCL_INST:GCL&collectionId=81313013130004641
4. Support processing for https://digital.grinnell.edu

If a proposed change does not improve this workflow directly or indirectly, question whether it belongs.

## How To Prompt The AI

Prefer outcome-based requests over file-only instructions.

Good prompt pattern:
- Goal: what ingest step should improve
- Input: deployment URL pattern, metadata source, folder assumptions
- Output: exact files/format expected for Alma-Digital ingest
- Constraints: keep encryption behavior, preserve existing function IDs, update docs
- Validation: what success should look like in UI/status/log output

Example:
Add a new function that accepts a GCCB deployment URL, validates reachability, and writes a normalized ingest-input file set to the selected working/output folder. Keep Function 0 encryption unchanged and add help documentation for the new function.

## Reference Repositories

When asking for implementation help, you can point the AI at these repositories for patterns:
- https://github.com/Digital-Grinnell/common-DG-utilities
- https://github.com/Digital-Grinnell/manage-digital-ingest-flet-Alma

Ask the AI to adapt patterns rather than copy blindly, and keep naming/behavior coherent with this repo.

## Review Checklist

Confirm all of the following:
- Changes advance deployment selection and/or Alma ingest-input generation.
- app.py remains the runtime source of truth unless you explicitly requested otherwise.
- app.py.bak, app_from_ohm.py, and app_ohm_full.py were not edited unintentionally.
- Sensitive settings encryption behavior was not weakened.
- Function behavior changes are reflected in matching FUNCTION_*.md docs.
- README.md and QUICKSTART.md are updated if onboarding changed.

## Typical Change Boundaries

Most clean changes should stay within one boundary:
- Runtime behavior in app.py plus matching FUNCTION_*.md
- Docs-only updates (FUNCTION_*.md, README.md, QUICKSTART.md)
- Packaging/launcher updates (run.sh, run.bat, build_dmg.sh, build_windows_zip.sh)
- Dependency updates in python_requirements.txt with corresponding imports/guards

## Ask For A Plan First When

Request a plan before edits for:
- Large refactors
- Settings/encryption model changes
- Broad dependency upgrades
- Cross-platform packaging changes
- Renaming function IDs or changing core workflow terminology

## Lightweight Validation

Use focused validation for touched areas:

```bash
python3 -m py_compile app.py
bash -n run.sh build_dmg.sh build_windows_zip.sh
```

For docs-only work, review the diff for accuracy and workflow alignment.

## Suggested Prompt Templates

Feature request template:

Goal: Improve [deployment selection | metadata mapping | ingest output generation].
Input assumptions: [GCCB URL format, metadata endpoints, local folders].
Output required: [file names, schema, destination folder].
Constraints: [no encryption regressions, keep existing functions, update docs].
Validation: [specific status/log messages and sample output expectations].

Docs request template:

Rewrite AGENTS.md and HUMANS.md so they prioritize selecting a GCCB deployment and generating Alma-Digital Pending Review ingest inputs, and include guidance for using Digital-Grinnell reference repositories.
