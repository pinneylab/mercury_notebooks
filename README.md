# Mercury tutorial notebooks

**Tutorial notebooks and example data for processing and analyzing high-throughput microfluidic enzyme kinetics (HT-MEK) experiments with [Mercury](https://github.com/pinneylab/mercury).**

[![Latest release](https://img.shields.io/github/v/release/pinneylab/mercury_notebooks?include_prereleases)](https://github.com/pinneylab/mercury_notebooks/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-purple.svg)](LICENSE)

This repository provides the notebook-based workflows that accompany Mercury and the Methods in Enzymology chapter **“Processing and analyzing high-throughput microfluidic enzymology data: a practical guide to rate fitting and quality control.”** *(in review)* The notebooks walk from raw HT-MEK microscopy images or previously quantified fluorescence tables to calibrated reaction rates, quality-controlled kinetic fits, and exportable biochemical parameters.

If you want the underlying Python package or API documentation, visit the [Mercury repository](https://github.com/pinneylab/mercury).

## 
Want to work through the examples in the paper? [Look here.](Methods_In_Enzymology/)

## Start here

Choose the workflow that matches your starting data:

| Starting point | Notebook | Purpose |
| --- | --- | --- |
| Quantified fluorescence tables | [`htbam_notebooks/analysis_mm.ipynb`](htbam_notebooks/analysis_mm.ipynb) | Calibrate fluorescence, fit initial rates, apply quality-control filters, fit Michaelis–Menten parameters, combine replicates, and export results |
| Raw tiled microscopy images | [`htbam_notebooks/process.ipynb`](htbam_notebooks/process.ipynb) | Stitch images, subtract backgrounds, locate chambers, and export fluorescence tables for downstream analysis |

For the shortest introduction to Mercury, begin with `analysis_mm.ipynb` and the supplied example dataset. Image processing requires experiment-specific raw images, acquisition metadata, device geometry, and pinlist information and is therefore a more advanced starting point.

## Repository contents

```text
mercury_notebooks/
├── htbam_notebooks/
│   ├── analysis_mm.ipynb        # Main Michaelis–Menten analysis tutorial
│   └── process.ipynb            # Image stitching and quantification workflow
├── example_data/
│   └── 9_17_25/                 # Example quantified assay tables
├── archive/                     # Historical notebooks retained for reference
├── in_progress/                 # Workflows under active development
├── LICENSE
└── README.md
```

Notebooks under `archive/` document earlier workflows and may depend on older Mercury APIs. Files under `in_progress/` are not part of the validated publication workflow.

## Installation

### 1. Download a versioned notebook release

For reproducible use, download the notebook archive associated with a [GitHub release](https://github.com/pinneylab/mercury_notebooks/releases). Each publication release should identify the compatible Mercury version.

Alternatively, clone the current development version:

```bash
git clone https://github.com/pinneylab/mercury_notebooks.git
cd mercury_notebooks
```

### 2.  Create an environment and Install the matching Mercury release

Follow [installation instructions](https://github.com/pinneylab/mercury#getting-started) in the *Mercury* repository.

### 3. Launch the notebooks

From the repository root, run:

```bash
jupyter notebook
```

Open `htbam_notebooks/analysis_mm.ipynb` and confirm that the selected kernel belongs to the `mercury-tutorial` environment.

## Michaelis–Menten tutorial

The primary analysis notebook follows the same conceptual sequence described in the Methods in Enzymology chapter:

1. Load button-quantification, product-standard, and kinetic time-series data.
2. Convert fluorescence measurements to enzyme and product concentrations.
3. Fit initial rates for each chamber and substrate concentration.
4. Estimate and subtract the nonenzymatic background rate where appropriate.
5. Apply chamber- and fit-level quality-control filters.
6. Fit Michaelis–Menten parameters.
7. Normalize fitted rates by enzyme concentration to obtain catalytic parameters.
8. Compare replicate chambers and inspect diagnostic plots.
9. Export chamber-level data, sample-level summaries, and visual diagnostics.

Before running the notebook, edit its parameter cell to specify the example-data or user-data directory, filenames, concentration columns, assay units, and fluorescence-calibration constants.

### Required analysis inputs

| Input | Description |
| --- | --- |
| `button_quant.csv` | Per-chamber protein-expression or loading measurements |
| `standard_data.csv` or `standard_data.csv.bz2` | Per-chamber product-standard measurements across known concentrations |
| `kinetics_data.csv` or `kinetics_data.csv.bz2` | Per-chamber reaction-progress measurements across time and substrate concentrations |

Exact filenames and metadata-column names are configured in the notebook and may differ between experiments.

### Principal analysis outputs

The example workflow exports:

- chamber-level kinetic parameters (`MM_chamber_data.csv`);
- sample-level parameter summaries (`MM_sample_data.csv`);
- Michaelis–Menten fit plots (`mm_sample_subplots.pdf`); and
- per-sample end-to-end diagnostic summaries (`all_samples_visual_summary/`).

## Processing new microscopy data

The processing notebook converts raw tiled microscopy images into the fluorescence tables used by the analysis notebook. It covers:

- tiled-image stitching and rotation/overlap adjustment;
- optional flat-field correction;
- fluorescence-background subtraction;
- device and pinlist configuration;
- interactive chamber-corner selection; and
- button, standard-curve, and kinetic-image quantification.

This workflow assumes the Mercury HT-MEK acquisition directory structure and metadata files, including `imaging.csv` and per-series `series_index.json` files. Users applying the workflow to a different microscope, file-naming convention, or device geometry should expect to adjust the configuration and inspect all intermediate images.

Raw microscopy example data will be included in this repo in a future release.

## Using your own data

We recommend copying the relevant notebook before editing it:

```bash
cp htbam_notebooks/analysis_mm.ipynb my_analysis.ipynb
```

Keep raw data unchanged, write outputs to a separate directory, and record the following alongside every analysis:

- Mercury software version or commit;
- notebook release or commit;
- Python version and environment specification;
- all user-edited parameter cells and filter thresholds; and
- any manual exclusions or fit-window adjustments.

## Citation

If these notebooks contribute to published work, please cite the Methods in Enzymology chapter and the archived notebook release:

> *[In Review]* Freitas, N., Zhang, J., Muir, D., et al. **Processing and analyzing high-throughput microfluidic enzymology data: a practical guide to rate fitting and quality control.** *Methods in Enzymology*.

## Authors and acknowledgments

These notebooks were developed by Nicholas Freitas, Duncan Muir, Jonathan Zhang, and contributors in the [Pinney Lab](https://pinneylab.com/).

Additional contributions and foundational development: Daniel Mohktari, Scott Longwell, and members of the [Fordyce Lab](https://www.fordycelab.com/).

## License

This repository is distributed under the [MIT License](LICENSE).
