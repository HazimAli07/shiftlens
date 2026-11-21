# ShiftLens

**Industrial vision workbench by Hazim Ali.** Inspect images across 12 object categories directly in Chrome, compare two detectors, review patch heatmaps, and export a session as CSV. Images stay in the browser.

[Open the workbench](https://hazimali07.github.io/shiftlens/) · [Download the source and trained weights](ShiftLens-v1.0.zip) · [View the Databricks notebook](ShiftLens_Benchmark.ipynb) · [Benchmark JSON](benchmark.json)

## Engineering result

ShiftLens uses 10,821 real industrial images from Amazon Science VisA. The published test split contains 2,162 images. Each detector was fitted on normal training images and used a separate normal subset to calibrate its cutoff.

| Detector | Defects caught (of 1,200) | Good images flagged (of 962) | Mean category AUROC |
|---|---:|---:|---:|
| Patch retrieval | **442** | 63 | **0.798** |
| Reference template | 343 | 62 | 0.736 |
| PyTorch CNN | 122 | 55 | 0.608 |

Patch retrieval uses location-aware nearest neighbors over normal patch statistics. Its result was measured in Python. The browser workbench runs the CNN and reference template with real examples, input files, and category-specific thresholds. A held-out example displays the numerical score difference from Python.

## What you can inspect

- `index.html` contains the standalone app. Open it in Chrome after downloading to use it offline.
- `benchmark.json` contains counts, thresholds, AUROC, and per-category results for all three detectors.
- `ShiftLens_Benchmark.ipynb` validates 36 records and writes a versioned Delta snapshot and summary view in a writable Databricks workspace.
- `ShiftLens-v1.0.zip` contains the Python training/evaluation code, tested offline app, trained weights, static site source, Databricks bundle and reproducibility instructions.

ShiftLens is a research workbench. A low anomaly score can miss a defect. Models were evaluated on VisA's official one-class split and are designed for objects similar to the selected category.

Dataset and image examples are from [Amazon Science VisA](https://registry.opendata.aws/visa/) under CC BY 4.0.
