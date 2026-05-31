# offroad
MATLAB utilities and analysis scripts for off-road navigation log inspection.

## Repository structure
- `common/`: shared MATLAB helpers (constants, plotting helpers, and utilities).
- `merlo/row_filter/`: row-filter analysis entry script and helper functions/plots.
- `merlo/bags/`: default folder used by scripts to pick `.mat` logs.
- `MATLAB-graphic-tools/`: git submodule with plotting helpers used by analysis scripts.
- `Offroad.prj`: MATLAB project file for opening the repository as a project.

## Requirements
- MATLAB (recent release with Project support).
- A row-filter log exported as `.mat`.
- Git submodules initialized (required for `graphics_options` and related plotting tools).

## Setup
If you already cloned the repo without submodules, run:

```bash
git submodule update --init --recursive
```

## Start as a MATLAB project
1. Open MATLAB.
2. Open the project file:
   - `Offroad.prj` from MATLAB UI, or
   - from MATLAB command window:
     ```matlab
     openProject('/absolute/path/to/offroad/Offroad.prj');
     ```
3. Ensure MATLAB current folder is the project root (`.../offroad`).

## Run the row-filter analysis
Main entry point:

- `/absolute/path/to/offroad/merlo/row_filter/RowFilterAnalysis.m`

Typical flow:
1. Open `RowFilterAnalysis.m`.
2. Configure script options at the top:
   - `compare` (`false`/`true`) to compare one or two logs.
   - `line_form` (`'normal'` or `'explicit'`).
3. Run the script.
4. When prompted, select a `.mat` log file (default dialog starts in `merlo/bags`).

The script loads the log, parses row-filter/vehicle topics, and generates multiple analysis plots (state, chunks, line equations, distances, map, and angle estimates).

## Expected log fields
The loaded `.mat` structure is expected to contain row-filter and vehicle-state topics, including:
- `perception__row_filter__line_equations`
- `perception__row_filter__debug__equation_meas`
- `localization__vehicle_state`

Optional:
- `supervisor__vehicle_status` (used for additional in-row status overlays when available).

## Notes
- `merlo/bags/` is intentionally empty in the repository (`.gitkeep` only). Add your own logs locally.
- `RowFilterAnalysis.m` uses `currentProject`, so running it from an open MATLAB project is the supported workflow.
