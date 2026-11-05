# AquaSTAT

AquaSTAT is a Python desktop application for water-chemistry analysis, geochemical
diagrams, multivariate statistics, spatial mapping, and interactive 3D
visualization. It combines a project workspace with figure styling, numerical
results, and methods exports to support research and publication workflows.

The interface uses **PySide6** and **Matplotlib**. Scientific calculations use
NumPy, pandas, SciPy, and scikit-learn; spatial workflows also use pyproj and
Shapely. Data and analysis run locally. Online map backgrounds require an internet
connection.

## Modules

| Module | Main capabilities |
| --- | --- |
| **Groundwater & contamination** | Triangle, rectangle, color-coded and contour-filled Piper diagrams; Durov, Stiff, Chernoff face, Schoeller, Gibbs, Chadha, Gaillardet and HFE-D diagrams; USSL and Wilcox irrigation assessments. |
| **Statistics** | Pearson and Spearman correlation; PCA scores, loadings, scree plots and correlation circles; optional Varimax rotation; Ward clustering; sample heatmaps, scatter matrices, boxplots, observed time series and bootstrap intervals. |
| **Maps, kriging & contours** | Sample-location maps, optional OpenStreetMap backgrounds, ordinary kriging, prediction variance, IDW interpolation and contours. |
| **3D visualization** | XYZ sample scatter, linearly interpolated XYZ surfaces, PCA sample scores and component loadings; camera rotation, plane views and coordinate guides. |
| **Assessment & uncertainty** | Measurement-quality and charge-balance checks, uncertainty and sensitivity scenarios, chemical screening, assay priorities, compositional PCA, cluster stability, spatial validation and repeated-well analysis. |

## Install and launch

Use **Python 3.10 or newer**. The desktop application is developed and checked on
Windows. Run it from the source folder using `main.py`.

Open PowerShell in the AquaSTAT folder, then create a virtual environment and
install the dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe main.py
```

These commands use the environment's interpreter directly, so activating the
environment is optional. In VS Code, select `.venv\Scripts\python.exe` as the
Python interpreter before running `main.py`.

If your current Python environment already has the dependencies installed:

```powershell
python main.py
```

To open a saved project at startup:

```powershell
python main.py "C:\path\to\study.aquastat"
```

## First project

1. From **Home**, create a project, choose its folder and starting module, or open
   an existing `.aquastat` project.
2. Import a **CSV or Excel workbook**. For Excel, select the intended worksheet.
   Review column names and the imported table in **Data**.
3. Choose a plot from the **Plot library**. Under **Settings**, select the
   measurement columns, units, preprocessing and method options it requires.
4. Click **Generate**. Auto update can refresh plots after setting changes;
   turn it off when you prefer to apply changes manually.
5. Inspect the plot and available numerical results. Use **Style** and the font
   toolbar to adjust labels, colors, legends, figure size and typography.
6. Use **Export** to save figures or export numerical tables and methods.
   **Save project** separately to preserve the dataset and plot settings.

Modules share the imported dataset. Each plot keeps its own analysis, appearance
and export settings. Saved projects embed the data, allowing them to reopen
without reading the original CSV or workbook again.

## Preparing data

Use one row per sample or observation, with a header row identifying the columns.
Required columns depend on the selected plot; not every workflow needs a complete
major-ion dataset.

| Data | Typical columns or requirements |
| --- | --- |
| Sample identification | A `Sample` column is useful for labels and is required by some sample-specific diagrams. |
| Major-ion chemistry | `Ca`, `Mg`, `Na`, `K`, `HCO3`, `CO3`, `Cl`, `SO4`; additional fields such as `pH` and `TDS` depend on the diagram. |
| Irrigation assessment | Measured `EC` and the required ion concentrations. Select concentration and conductivity units explicitly. |
| Statistics | Numeric measurement columns selected for the analysis. Review IDs, coordinates and redundant variables before including them. |
| Maps | Numeric X/Y coordinates and an explicitly selected source coordinate system; interpolation also needs a numeric measurement. |
| XYZ plots | Three distinct numeric columns. Surfaces need at least three distinct, non-collinear X/Y locations. |
| Time series | A measurement, date/time column and optional group or site column. |

Review the selected missing-data policy and reported exclusions before interpreting
a result. A blank cell does not mean zero. Qualifiers such as `<0.01`, detection
limits, and laboratory uncertainties need explicit treatment; the Assessment
module provides measurement-model controls for these workflows.

Bundled datasets are in [data/](data/). Check their available fields, units and
source information before choosing an analysis.

Assessment engine 1.1.0 adds supplied/training-fitted censored lognormal models,
explicit reporting-limit probability bounds, and optional follow-up assay value
under a declared precision and decision-loss model. See the
[assessment 1.1 methods and limitations](docs/ASSESSMENT_1_1.md) and the
[executed manuscript evidence](Manuscript/README.md).

## Figure styling and 3D views

The plot toolbar and **Style** inspector provide font, text-color, axis-label,
tick, legend, grid and figure-size controls. Under **Settings > Plot settings**,
the manual title has independent size, bold/italic and left/center/right
alignment controls. A blank title retains the automatic heading.

The **3D visualization** module adds a toolbar directly above the plot:

- **3D / isometric**, **XY / top**, **XZ / front**, and **YZ / side** presets use
  orthographic projection. Plane views hide the collapsed axis's ticks and label.
- **Auto rotate** animates the preview. The **View** menu provides speed,
  direction, perspective/orthographic projection, exact camera angles and reset.
- Drag the plot to choose a custom camera. Rotation stops when exporting,
  changing plots or leaving the module.
- XYZ **coordinate guides** are enabled by default and connect samples to the
  coordinate planes without expanding the axes to zero. PCA uses origin lines
  from `(0, 0, 0)`.
- Color scales follow the visible 3D plot height during rotation, resizing and
  export.

Image exports save a fixed camera view. Save multiple plane views when a figure
needs to show different projections. Camera controls change the view without
recalculating measurements.

## Exports and reproducibility

| Output | Formats | Contents |
| --- | --- | --- |
| Figures | PNG, TIFF, JPG, PDF, SVG | The current rendered figure, including its camera, labels, legend and color scale. |
| Results and methods | CSV + JSON, Excel, Word, PDF | Available numerical tables, methods, warnings and provenance for the generated analysis. |
| Projects | `.aquastat` | Embedded dataset and saved workspace/plot settings. |

Choose the output folder, file name, format and DPI in **Export**. Existing files
require confirmation before replacement. Figure export uses the last rendered
result; apply pending settings with **Generate** before saving.

For publication, choose dimensions and resolution to match the journal's
requirements. PDF/SVG support vector artwork; map tiles remain raster images.
Tight cropping can change the final page dimensions. Save numerical tables and
methods alongside figures, and record units, variable selection, preprocessing
and uncertainty assumptions.

The USSL/Wilcox graphical boundaries include documented approximations; review
their provenance before using graphical classifications in a manuscript. Spatial
interpolation depends on coordinate units and model settings. See the
[scientific methods and publication guide](docs/publication.html) and
[mapping guide](docs/maps.html) for definitions and limitations.

## Documentation

| Guide | Topics |
| --- | --- |
| [Documentation home](docs/index.html) | Complete HTML/CSS/JS guide with local figures, search and examples. |
| [First project](docs/quickstart.html) | Import a workbook, generate a diagram, save and export. |
| [Workspace guide](docs/workspace.html) | Project lifecycle, desktop controls, navigation and styling. |
| [Diagram library](docs/diagrams.html) | All 14 chemistry and irrigation views, inputs, formulas and citations. |
| [Statistics](docs/statistics.html) | Correlation, PCA, clustering, time series and bootstrap. |
| [Maps](docs/maps.html) | Coordinates, interpolation, boundaries, backgrounds and attribution. |
| [Assessment](docs/assessment.html) | Measurement quality, uncertainty, compositional and spatial validation. |
| [Datasets and worked study](docs/tutorial.html) | A 47-row Sukinda tutorial and four bundled datasets. |
| [Multi-dataset plot gallery](docs/example-gallery.html) | Moreno Merino, Liu and Yang plots, plus Sukinda maps using the supplied study-area KML. |
| [Publication and Python API](docs/publication.html) | Figure and methods exports, with linked Python and replay examples. |
| [Complete printable manual](docs/manual.html) | One continuous HTML guide; print or save as PDF from the browser. |

Open `docs/index.html` directly in a browser; no server or internet is needed.
The in-app **Support & Resources** page also opens the bundled HTML site and manual. Online
documentation and issue links become available when configured in
[`resource_links.json`](aquastatpy/assets/resource_links.json).
See [using and hosting the guide](docs/site-guide.html) for GitHub Pages and
future image-hosting instructions. All current documentation images are local.

AquaSTAT authors: **Sachida Nanda Mahanta** (sachida5908@gmail.com) and
**Bristi Phukan** (bristi.87.hn.24@gmail.com). Scientific-module author credits
and upstream acknowledgments are retained in the source and documentation.

## Development and checks

The main source locations are:

```text
main.py                 Desktop entry point
requirements.txt        Runtime dependencies
aquastatpy/
  core/                 Data, projects, plot jobs and exports
  ui/                   Shared desktop interface
  modules/              Module workspaces and controls
  assessment/           Assessment and uncertainty calculations
docs/                   User and scientific-method guides
data/                   Bundled datasets
tests/                  Automated checks
validation/             Rendering reviews and validation artifacts
```

Install pytest into the same environment, then run the checks from the project
root. The following PowerShell commands use Qt's offscreen mode:

```powershell
.\.venv\Scripts\python.exe -m pip install pytest
$env:QT_QPA_PLATFORM = 'offscreen'
$env:QT_QPA_FONTDIR = 'C:\Windows\Fonts'
$env:MPLBACKEND = 'Agg'
.\.venv\Scripts\python.exe -m pytest tests -q
```

Use a fresh terminal for a normal desktop launch, or remove these test overrides:

```powershell
Remove-Item Env:QT_QPA_PLATFORM, Env:QT_QPA_FONTDIR, Env:MPLBACKEND -ErrorAction SilentlyContinue
```

When reporting a problem, include the Python version, selected module/plot,
reproduction steps and error text. A small anonymized input example helps
reproduce data-dependent issues.

## License and acknowledgments

AquaSTAT is distributed under the **GNU General Public License, version 3**;
see [LICENSE](LICENSE). Original scientific-module author credits are retained
in the source. Bundled third-party assets retain their accompanying notices.
Maps using OpenStreetMap must retain the displayed contributor attribution.
