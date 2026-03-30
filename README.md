# 3D Neuron Visualizer

Generate interactive 3D visualizations of neuron morphologies and connectivity from [neuPrint](https://neuprint.janelia.org/). Outputs are self-contained HTML files.

New to Python? See [README_IF_YOURE_LOST.md](README_IF_YOURE_LOST.md).

### Examples

- **EPG** (50 neurons) — [download](https://drive.google.com/file/d/1MpyMU-bE7-B6wzMu7Oewg9p3Y9eFSb87/view?usp=drive_link) | [notebook](Examples/EPG/)
- **FB** (601 neurons, custom colors) — [download](https://drive.google.com/file/d/1JEHjA27eSceIz5E_SPy_g1vUlZLB5H4A/view?usp=drive_link) | [notebook](Examples/FB/)

## Setup

```bash
git clone https://github.com/sauvolac1/neuron-visualizer.git
cd neuron-visualizer
pip install -r requirements.txt
```

Get a neuPrint token: https://neuprint-cns.janelia.org/ → Account → Auth Token.

## Usage

**Notebook**: Open `generate_viz.ipynb`, fill in your token and search pattern, run.

**Command line**:
```bash
export NEUPRINT_TOKEN='your_token'
python generate_visualization.py EPG
python generate_visualization.py FB --use-meshes --mesh-faces auto
```

Output is a standalone HTML — open it directly in Chrome.

## CLI Options

| Argument | Default | Description |
|----------|---------|-------------|
| `patterns` | required | Neuron type patterns (e.g. `FB`, `EPG`, `'^LNO\|GLNO.*'`) |
| `--server` | `neuprint-cns.janelia.org` | neuPrint server |
| `--dataset` | `cns` | neuPrint dataset |
| `--token` | `$NEUPRINT_TOKEN` | API token |
| `--continuous` | | Continuous color CSVs |
| `--categorical` | | Categorical color CSVs |
| `--use-meshes` | off | Include 3D surface meshes |
| `--mesh-faces` | `auto` | Faces per mesh (`auto`, number, or `0`) |
| `--max-file-mb` | `500` | Target file size for auto decimation |
| `--skip-synapses` | off | Skip synapse fetching |
| `--output-dir` | `Examples/` | Output directory |
| `--open` | off | Open in browser when done |

## Features

### Color modes

Built-in: **Cell Type**, **Instance**, **Predicted NT**, **Custom** (click swatches to edit).

Add more via CSV — continuous (numeric columns → colormapped) or categorical (shared values → shared colors). Right-click color buttons to change colormaps. Shuffle button (🔀) randomizes assignments.

### Meshes

`--use-meshes` fetches neuron surface meshes. Toggle Mesh/Skeleton in the sidebar. `auto` decimation keeps quality high while respecting the file size limit.

### Synapses

Right-click a partner in the Connections panel to show synapse positions as 3D spheres. Right-click a synapse group to split by instance.

### Session persistence

State auto-saves to localStorage. Export/import session JSON files (⬇/⬆ buttons) to share views.

### Video export

🎬 button — record rotations (full 360° or pivot). Choose axis, orbit center, format (AVI/WebM/GIF), and preview before recording.

## CSV Formats

**Continuous** — `type` column + numeric columns:
```
type,valence_score
FB2M_a,0.0926
```

**Categorical** — `type` column + category columns:
```
type,region
FB1A,dorsal
```

## Controls

| Action | Input |
|--------|-------|
| Rotate | Left-click drag |
| Pan | Right-click drag |
| Zoom | Scroll |
| Highlight | Double-click sidebar row |
| Connections | Single-click highlighted row |
| Synapses | Right-click partner row |
| Screenshot | 📷 button |
| Video | 🎬 button |
| Magnifier | 🔍 button |
| Reset camera | ↺ button |
