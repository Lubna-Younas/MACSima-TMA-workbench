# Previously performed command and QC history

This is a **record of work already performed**, assembled from the original workspace scripts, local review notes, and receipts on 2 November 2026. It is not a new pipeline or an instruction to rerun every stage. Script names below refer to the preserved local project archive. Shell examples replace private locations with `/path/to/...` placeholders as requested; some archived scripts also contain path-specific configuration and cannot be run unchanged from a public clone.

## VSC5 CLI pilot

The preserved `vsc5_macsima/submit.sh` wrapper exposes `check`, `smoke`, `pilot-devel`, `explore-devel`, `pilot`, `explore`, and `batch` modes. The recorded ROI2 history includes a completed three-marker smoke job, a full ROI2 quantification job that timed out before analysis finished, and a completed analysis-only resume. `vsc5_macsima/reports/PILOT_STATUS.md`, `full_roi2_validation.json`, and `local_vsc5_smoke_comparison.json` are the local evidence. The seven other ROIs were configured but **not run through that VSC5 batch wrapper** at that checkpoint.

Historical wrapper pattern, with the location redacted:

```bash
cd /path/to/private-workspace/vsc5_macsima
bash submit.sh check
bash submit.sh smoke
bash submit.sh pilot-devel
bash submit.sh explore-devel
```

The wrapper uses site-specific `cluster.env`, `config.vsc5.json`, and Slurm settings. These lines identify the wrapper modes consistent with the recorded jobs; the exact original shell lines were not preserved in the inspected local copy. The job receipts are the outcome evidence. They do not establish MACSiQ View vendor preprocessing or a current full VSC5 batch run.

## MACSiQ View preprocessing and Cellpose source

The processed TIFF metadata in the earlier ROI2 workflow records MACSiQ View 1.3.3 distortion correction, flat-field correction, and denoising. Background subtraction was confirmed separately by the user. The inspected workspace does **not** contain a recovered, executable command for unattended vendor batch preprocessing on VSC5 or in the MACSiQ View Python console. The validated VSC5 MACSiQ repair was a **Python/Jupyter startup repair**, not a preprocessing run. Its runtime-only invocation was:

```bash
bash /path/to/private-software/run_macsiq_python_fixed.sh --check-python
```

The original local Cellpose script is `run_cellpose4_cpsam_tma_rois.py`. It specifies Cellpose 4.0.7 `cpsam`, 2D DAPI images, 1024-pixel tiles, 128-pixel overlap, and four selected ROIs. Existing Cellpose4 masks are used by later QC. The inspected project archive does not contain a run receipt tying that script to a complete batch, and it contains no tested Z-stack mode in that script. These distinctions prevent an unverified launch or Z-stack result from being labeled historical validation.

Local MACSiQ View **analysis** is separately evidenced. `vsc5_macsima/roi10_cytoplasm_20260909/README.md` and trial receipts record ten full-ROI cytoplasm segmentation comparisons in MACS iQ View 1.3.3 with fixed Cellpose4 nuclei; the candidate mask was not approved as a replacement. `dawn_dusk/roi5_roi10_gating/README.md` records local DAWN runs in MACS iQ View and DUSK review for ROI5/ROI10; the automatic biological gates did not pass validation. These are genuine local console/application runs, but they are different operations from unattended vendor batch preprocessing.

## Local 27-ROI QC sequence

The archive root is `batch_qc_27roi_20260910/`. The commands below identify its existing entry points. Use the preserved review and receipt files for outcomes; do not treat these lines as an automatic rerun recipe.

```bash
cd /path/to/private-workspace
PYTHON=/path/to/existing/macsima/python
"$PYTHON" batch_qc_27roi_20260910/stage1/intake.py
"$PYTHON" batch_qc_27roi_20260910/stage1/summarize.py
"$PYTHON" batch_qc_27roi_20260910/stage2/run_stage2.py
"$PYTHON" batch_qc_27roi_20260910/stage3/run_stage3.py
"$PYTHON" batch_qc_27roi_20260910/stage4/run_stage4.py
"$PYTHON" batch_qc_27roi_20260910/stage5/run_stage5.py
"$PYTHON" batch_qc_27roi_20260910/stage6/run_stage6.py
"$PYTHON" batch_qc_27roi_20260910/stage7/run_stage7.py
"$PYTHON" batch_qc_27roi_20260910/stage8/run_stage8.py
```

| Checkpoint | Original source and evidence | PDF numbers | Recorded meaning |
| --- | --- | --- | --- |
| Intake and coordinate/mask review | `stage1/`, `stage1b/`, `stage1c/` reviews and receipts | 01–06 | 27-ROI inventory and targeted follow-up completed; Stage 1 scientific review remained open |
| DAPI cycle image screen | `stage2/run_stage2.py`, `stage2/completion_receipt.json` | 07–08 | 27 ROIs, C000–C033 review checkpoint; no corrections or exclusions |
| Translation screen | `stage3/run_stage3.py`, `stage3/completion_receipt.json` | 09–10 | 27 ROIs × 33 signal cycles; earlier purported held-out checks reused fit fields, so independent validation was not established there |
| Marker image screen | `stage4/run_stage4.py`, `stage4/completion_receipt.json` | 11–12 | Signal/background sampling and marker image review |
| Cross-ROI marker screen | `stage5/run_stage5.py`, `stage5/completion_receipt.json` | 13–14 | Image-level consistency, not cell identities |
| Integrated ROI/tissue review | `stage6/run_stage6.py`, `stage6/completion_receipt.json` | 15–16 | Provisional tissue labels and technical context |
| Review packaging | `stage7/run_stage7.py`, `stage7/completion_receipt.json` | 17–18 | Review-ready package, not scientific acceptance |
| Initial mask screen | `stage8/run_stage8.py`, `stage8/completion_receipt.json` | 19–20 | Mask-only summary; `stage8/run_dapi_mask_overlap.py` was abandoned and is not validated evidence |

The subsequent nuclear-reference checkpoint is in `nuclear_validation_reference/` and PDFs 21–22. The complete all-cycle DAPI measurement is in `batch_cycle_validation/`: `run_batch.py`, `fast_moments.py`, `measure_centroids.py`, `build_batch_review.py`, `finish_batch.py`, and `verify_delivery.py`. `RUN_STATUS.json` and `delivery_receipt.json` record **completed computation** for 27 ROIs × 33 cycles, 891 ROI-cycle records, 1,782 DAPI acquisitions, 509,264 original nuclear labels, and five PDFs (24–28; 277 pages). Source masks were hash checked, original images/masks were unchanged, and no exclusions were applied. Registration uncertainty and per-nucleus/cycle status remain part of the output; this is not exhaustive manual segmentation adjudication.

The preserved all-cycle entry points were invoked from the local project environment. The default `run_batch.py` arguments select all 27 ROIs and C001–C033; the completion and verification scripts consume its saved checkpoints:

```bash
cd /path/to/private-workspace
PYTHON=/path/to/existing/macsima/python
"$PYTHON" batch_qc_27roi_20260910/batch_cycle_validation/run_batch.py
"$PYTHON" batch_qc_27roi_20260910/batch_cycle_validation/finish_batch.py
"$PYTHON" batch_qc_27roi_20260910/batch_cycle_validation/verify_delivery.py
```

The Stage 1B/1C source also includes `stage1b/coordinates.py`, `masks_and_overlays.py`, `build_figures.py`, and `finalize_checkpoint.py`, followed by the focused `stage1c/` provenance, diagnostics, figure, and addendum scripts. Their review files are the source of truth for the exact checkpoint scope.

## Later local review and measurement checkpoints

| Original source | PDF numbers | What was performed and its limit |
| --- | --- | --- |
| `cycle_localization/` | 23 | ROI2 cycle-labeled spatial QC |
| `biomarker_review/build_checkpoint.py` | 29–30 | 27-ROI image-level biomarker review; not final cell-level marker approval |
| `registration_pilot/` | 31 | Five-case correction pilot; no candidate transform accepted into production |
| `roi_channel_register/` | 32 | Full ROI/channel technical review register with unresolved human decisions |
| `cell_marker_pilot/` | 33 | Bounded cell-marker quantification pilot |
| `gating_pilot/run_gating_pilot.py` | 34 | Candidate thresholds and source-image backchecks, biological gates |
| `clusters_pilot/` | 35–48 | Preflight, 27-ROI measurements, numbered exploratory clusters, neighbourhoods, gate sensitivity, image backchecks, AF/compartment checks, panel and seed reviews; see each receipt and review index |
| `targeted_dapi/`, `roi26_local/` | 49–50 | Targeted DAPI and ROI26 shift diagnostics; no accepted correction inferred |
| `presentation_cheat_sheet/`, segmentation review/audit folders | 51–55 | Figure navigation and revised segmentation candidate reviews; prior split/merge examples were corrected, not accepted as error rates |
| ROI-specific reconstruction folders | Unnumbered ROI reports | Native-field reconstructions with separate technical, visual, and scientific status; do not infer all ROIs have finished from files already present |

The full measurement and exploration work used original masks and retained all cells in the measurement store. Candidate analysis subsets, gates, numbered clusters, and cell labels are not final biological identities. Native Field IDs and per-cell coordinates require explicit mapping; sparse image checks do not prove every nucleus is registered.

## Evidence and publication boundary

The local `PDF_ONLY` folder contains 77 PDF files at this snapshot. [The PDF index](QC_PDF_INDEX.md) lists every filename. PDFs, source images, masks, original receipts with private paths, patient/sample metadata, and the path-bound source scripts are not copied into this public PR. This history is meant to guide a later, item-by-item source-code publication review. The existing local archive remains the authoritative source for exact input hashes, output hashes, versions, and per-ROI status.
