# MACSima TMA workbench

This repository begins with the **history of commands and QC work already performed** for the MACSima TMA project. The repository documents the original local and VSC5 entry points, evidence receipts, and the local PDF catalog. 

## Read the project history

- [Command and validation history](history/COMMAND_HISTORY.md): what ran, where it ran, the source script, and what the result establishes.
- [QC PDF index](history/QC_PDF_INDEX.md): filenames of the existing local `PDF_ONLY` deliverables, grouped by workflow step. This is an inventory, not a public copy of the PDFs.

The source workspace contains original scripts, logs, receipts, microscopy images, masks, cell tables, and reports. This public repository currently links them by relative archive names only. No real home directory, cluster path, account, hostname, credential, microscopy image, mask, cell table, or PDF has been uploaded.

## Route map

| Route | Historical evidence | Current repository scope |
| --- | --- | --- |
| MACSiQ View preprocessing and local analysis | Processed export metadata, ROI10 cytoplasm trials, and ROI5/ROI10 DAWN/DUSK work | Local analysis results documented; exact vendor batch preprocessing launch command is still to be recovered from the original runtime history |
| VSC5 analysis CLI | ROI2 smoke, full quantification, and analysis-resume jobs with validation receipts | Original `submit.sh` modes and outcomes documented |
| Cellpose segmentation | Existing Cellpose4 masks and local segmentation script | Original source identified; its exact launch and a Z-stack run are not asserted from the inspected archive |
| Local 27-ROI QC | Stage scripts, review notes, completed all-cycle receipt, and `PDF_ONLY` deliverables | Historical steps and status recorded without altering source data |

The statuses in the history distinguish completed computation, technical checks, visual review, and scientific acceptance. A generated PDF or a completed job does not by itself approve a biological interpretation.
