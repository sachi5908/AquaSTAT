<p align="center">
  <a href="https://sachi5908.github.io/AquaSTAT_Documentation/">
    <img src="https://res.cloudinary.com/ylt4rk5l/image/upload/v1793853335/aquastat-documentation/assets/images/Logo--f28a084311b6dcf0.png" alt="AquaSTAT logo" width="460">
  </a>
</p>

<h1 align="center">AquaSTAT</h1>

<p align="center">
  <strong>Water chemistry, statistics and spatial analysis in one desktop workspace.</strong>
</p>

<p align="center">
  <a href="https://sachi5908.github.io/AquaSTAT_Documentation/">Documentation</a> &middot;
  <a href="https://sachi5908.github.io/AquaSTAT_Documentation/manual.html">User manual</a> &middot;
  <a href="https://sachi5908.github.io/AquaSTAT_Documentation/example-gallery.html">Examples</a> &middot;
  <a href="https://github.com/sachi5908/AquaSTAT/issues">Report an issue</a>
</p>

**AquaSTAT** is an open-source desktop application for water-chemistry analysis,
geochemical diagrams, multivariate statistics, spatial mapping and interactive
3D visualization. It brings data, analysis settings, figure styling and numerical
results together in a project-based workflow for research, teaching and publication.

## Overview

| | |
| --- | --- |
| **Version** | 1.0 |
| **Language** | Python 3.10+ |
| **Interface** | PySide6 (Qt) |
| **Plotting** | Matplotlib |
| **Analysis modules** | Groundwater, Statistics, Maps, 3D visualization and Assessment |
| **Project format** | `.aquastat` |
| **License** | GNU General Public License, version 3 (GPL-3.0) |

Data processing and scientific calculations run locally. Internet access is used
for online documentation and optional map backgrounds.

## Analysis workspaces

### Groundwater & contamination

Geochemical visualization and irrigation assessment, including:

- Triangle, rectangle, color-coded and contour-filled Piper diagrams
- Durov, Stiff, Chernoff face and Schoeller diagrams
- Gibbs, Chadha, Gaillardet and HFE-D diagrams
- USSL and Wilcox irrigation assessments
- Plot-specific inputs, unit selection, styling and figure export

### Statistics

Exploratory and multivariate analysis through:

- Pearson and Spearman correlation
- PCA scores, loadings, scree plots and correlation circles, with optional Varimax rotation
- Ward clustering, sample heatmaps and scatter matrices
- Boxplots, observed time series and bootstrap intervals
- Numerical results and recorded analysis settings

### Maps, kriging & contours

Spatial exploration and interpolation with:

- Sample-location maps and optional OpenStreetMap backgrounds
- Explicit source coordinate-system selection
- Ordinary kriging and prediction variance
- Inverse-distance weighting (IDW) and contour mapping
- Boundary layers, map styling and figure export

### 3D visualization

Interactive views of measurements and multivariate structure:

- XYZ sample scatter and linearly interpolated XYZ surfaces
- PCA sample scores and component loadings in three dimensions
- Isometric, XY, XZ and YZ camera presets
- Automatic rotation, perspective/orthographic projection and exact camera angles
- Coordinate guides and export of the current camera view

### Assessment & uncertainty

Measurement-quality review and analysis under declared assumptions:

- Measurement-quality and charge-balance checks
- Uncertainty propagation, sensitivity scenarios and chemical screening
- Detection-limit and censored-measurement controls
- Follow-up assay priorities and decision-model scenarios
- Compositional PCA, cluster stability, spatial validation and repeated-well analysis

Method definitions, input requirements and limitations are documented in the
[online module guides](https://sachi5908.github.io/AquaSTAT_Documentation/introduction.html).

## Applications

AquaSTAT supports workflows in:

- Groundwater chemistry and hydrogeology
- Water-quality assessment and contamination studies
- Irrigation-water evaluation
- Multivariate exploration of environmental measurements
- Spatial analysis and visualization of monitoring data
- Research and teaching in quantitative water analysis

## Documentation

Documentation is hosted separately at
**[AquaSTAT Documentation](https://sachi5908.github.io/AquaSTAT_Documentation/)**.
A local `docs/` folder is not required to install or run the software.

| Resource | Contents |
| --- | --- |
| [Getting started](https://sachi5908.github.io/AquaSTAT_Documentation/quickstart.html) | Create a project, import data, generate a plot and export. |
| [Workspace guide](https://sachi5908.github.io/AquaSTAT_Documentation/workspace.html) | Navigation, saved projects, analysis settings and figure styling. |
| [Illustrated workflows](https://sachi5908.github.io/AquaSTAT_Documentation/plot-workflows.html) | Worked plotting routes with screenshots and settings. |
| [Datasets](https://sachi5908.github.io/AquaSTAT_Documentation/datasets.html) | Example inputs and their source information. |
| [Example gallery](https://sachi5908.github.io/AquaSTAT_Documentation/example-gallery.html) | Geochemical, statistical, spatial and 3D examples. |
| [Methods and publication](https://sachi5908.github.io/AquaSTAT_Documentation/publication.html) | Figure exports, numerical outputs and reproducibility guidance. |
| [References](https://sachi5908.github.io/AquaSTAT_Documentation/references.html) | Scientific methods, citations and attribution. |
| [Complete user manual](https://sachi5908.github.io/AquaSTAT_Documentation/manual.html) | The full HTML manual; print or save as PDF from your browser. |

The application's **Support & Resources** page links to the hosted documentation,
manual, source repository and issue tracker. These addresses are configured in
[`resource_links.json`](aquastatpy/assets/resource_links.json).

## System requirements

| Component | Requirement |
| --- | --- |
| **Operating system** | Windows 64-bit for the supplied desktop build |
| **Python** | Python 3.10 or newer when running from source; not needed for the standalone build |
| **Display** | At least 1024 × 700; 1920 × 1080 recommended for viewing plots and settings together |
| **Rendering** | CPU-based Matplotlib rendering, including 3D figures; no dedicated GPU required |
| **Internet** | Needed for hosted documentation and online map backgrounds |

Processing time and memory use depend on dataset size, interpolation settings and
the number of uncertainty simulations.

## Installation

### Standalone Windows application

Use the supplied [AquaSTAT_EXE](AquaSTAT_EXE/) application folder and launch
`AquaSTAT.exe`.

Keep **`AquaSTAT.exe` and the `_internal/` folder together**. The standalone
application includes its Python runtime and dependencies.

### Run from source

Clone or download the [software repository](https://github.com/sachi5908/AquaSTAT).
Open PowerShell in the AquaSTAT project root and run:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe main.py
```

These commands use the virtual environment directly; activation is optional.
In VS Code, select `.venv\Scripts\python.exe` as the interpreter.

To open a saved project at startup:

```powershell
.\.venv\Scripts\python.exe main.py "C:\path\to\study.aquastat"
```

### Dependencies

The main runtime dependencies include **PySide6, NumPy, pandas, SciPy,
Matplotlib, scikit-learn, Shapely, pyproj, openpyxl, xlrd, python-docx,
ReportLab and defusedxml**. See [requirements.txt](requirements.txt) for the
complete runtime requirements.

## Usage

1. Create or open a project from **Home** or **Projects**.
2. Import a **CSV or Excel workbook** and review its columns and units in **Data**.
3. Choose an analysis in the **Plot library** and configure its inputs under **Settings**.
4. Click **Generate**. Use **Auto update** when you want setting changes to refresh the plot.
5. Review the figure and numerical results. Adjust labels, colors, fonts and dimensions under **Style**.
6. Use **Export** for figures or results and methods. Use **Save project** to preserve the dataset and workspace settings.

Modules share the imported dataset. Each plot retains its own analysis,
appearance and export settings. Saved projects embed the data so they can reopen
without reading the original CSV or workbook again.

Use one row per sample or observation and a header row for column names. Required
fields vary by analysis. Review units, missing-data policies and detection-limit
handling before interpreting a result; blank cells are not zeros.

## Outputs and reproducibility

| Output | Formats | Contents |
| --- | --- | --- |
| **Figures** | PNG, TIFF, JPG, PDF, SVG | The rendered plot, including its camera, labels, legend and color scale |
| **Results and methods** | CSV + JSON, Excel, Word, PDF | Available numerical tables, methods, warnings and provenance |
| **Projects** | `.aquastat` | Embedded dataset and saved workspace and plot settings |

Apply pending settings before exporting. Figure exports use the last rendered
result, and 3D images preserve the current camera view. PDF and SVG support vector
artwork; online map tiles remain raster images.

For research, retain numerical results and methods alongside figures. Report the
AquaSTAT version, source or standalone build, input units, variable selection,
preprocessing, coordinate system and uncertainty assumptions relevant to the analysis.

Irrigation-diagram boundaries include documented approximations, and spatial and
uncertainty results depend on the selected models. Consult the
[scientific references](https://sachi5908.github.io/AquaSTAT_Documentation/references.html)
and the relevant online method guide when interpreting or publishing results.

## Project structure

```text
AquaSTAT/
├── main.py                  # Desktop entry point
├── aquastatpy/
│   ├── __init__.py          # Application version
│   ├── core/                # Data, projects, plot jobs and exports
│   ├── ui/                  # Desktop interface and shared controls
│   ├── modules/             # Five analysis workspaces
│   ├── assessment/          # Assessment and uncertainty calculations
│   └── assets/              # Bundled logos, icons and online resource links
├── requirements.txt         # Source runtime dependencies
├── LICENSE                  # GNU GPL version 3
└── README.md
```

User documentation is published on the separate documentation site. The root
[.gitignore](.gitignore) excludes local documentation, manuscript and literature
folders, generated validation output and build caches from Git uploads. Application
source, bundled runtime assets and the standalone application folder remain included.

## Development and contributing

Bug reports and suggestions are welcome through the
[issue tracker](https://github.com/sachi5908/AquaSTAT/issues). Include the AquaSTAT
version, selected module and plot, reproduction steps and any error message.
A small anonymized input file helps reproduce data-dependent issues.

Install pytest into your source environment and run the checks from the project root:

```powershell
.\.venv\Scripts\python.exe -m pip install pytest
$env:QT_QPA_PLATFORM = 'offscreen'
$env:QT_QPA_FONTDIR = 'C:\Windows\Fonts'
$env:MPLBACKEND = 'Agg'
.\.venv\Scripts\python.exe -m pytest tests -q
```

Use a fresh terminal for a normal desktop launch, or clear the test overrides:

```powershell
Remove-Item Env:QT_QPA_PLATFORM, Env:QT_QPA_FONTDIR, Env:MPLBACKEND -ErrorAction SilentlyContinue
```

Test the affected workflow with representative data, preserve scientific-method
attribution, and update the hosted documentation when behavior changes.

## License and acknowledgments

AquaSTAT is distributed under the **GNU General Public License, version 3**.
See [LICENSE](LICENSE) for the complete license text.

Original geochemical plotting work by **Jing Yang and collaborators** is retained.
Scientific-module credits remain in the source and online references. The startup
and project interface draw inspiration from **FracSTAT**, and bundled third-party
assets retain their original notices. Maps using OpenStreetMap must preserve
contributor attribution.

## Citing AquaSTAT

A suggested software reference is:

> Mahanta, S. N., & Phukan, B. *AquaSTAT* (Version 1.0) [Computer software]. https://github.com/sachi5908/AquaSTAT

Also cite the original scientific methods relevant to the analyses used.

## Authors and contact

| Author | Contact |
| --- | --- |
| **Sachida Nanda Mahanta** | [sachida5908@gmail.com](mailto:sachida5908@gmail.com) |
| **Bristi Phukan** | [bristi.87.hn.24@gmail.com](mailto:bristi.87.hn.24@gmail.com) |
