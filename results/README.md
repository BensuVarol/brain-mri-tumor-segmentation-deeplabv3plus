# Recorded results and provenance

These files come from the saved outputs of the supplied, executed **`Brain_MRI_Tumor_Segmentation_DeepLabV3Plus_Final (1).ipynb`**. The [repository notebook](../notebooks/Brain_MRI_Tumor_Segmentation_DeepLabV3Plus_V2.ipynb) is preserved byte for byte. Its established filename is retained so existing GitHub and Colab links continue to work.

- Source notebook SHA-256: `5eeb967cf2e6092de9b4c2823f8efb708308f5339193f08bd00dfaf9cb879fab`.
- Executed code cells: **24**; recorded error outputs: **0**.
- Recorded training: **14 completed epochs** (5 warm-up + 9 fine-tuning); selected fine-tuning checkpoint at **epoch 7**; validation-selected threshold **0.70**.
- Test set: **378 slices from 11 patients**, including **127 tumor-positive** and **251 tumor-free** reference masks.
- Test Global Dice / IoU: **0.8359 / 0.7181**, rounded to four decimal places.
- Training and inference were **not rerun** for this repository update.

## Embedded figures

PNG images were decoded directly from saved `image/png` outputs. Their bytes were not redrawn, resized, or enhanced. They are the notebook's embedded renderings; separate higher-DPI files named in `savefig` calls were not supplied. Cell indices below are zero-based.

| File | Source cell | Scope |
|---|---:|---|
| [input_example.png](input_example.png) | 7 | One tumor-positive MRI/reference-mask example and overlay |
| [training_curves.png](training_curves.png) | 24 | Recorded 14-epoch training and validation curves |
| [prediction_results.png](prediction_results.png) | 34 | Four fixed-seed tumor-positive test examples, threshold 0.70 |

The prediction preview contains positive slices only. It does not demonstrate behavior on tumor-free cases; the test metric table records **61 false-positive empty slices out of 251**. Figure dimensions, byte sizes, hashes, and exact output locations are listed in [recorded_run_summary.json](recorded_run_summary.json).

## Tables and logs

| File | Source and precision |
|---|---|
| [dataset_split_summary.csv](dataset_split_summary.csv) | Exact integer split counts from the saved cell 9 table |
| [recorded_validation_metrics.csv](recorded_validation_metrics.csv) | Cell 29 validation table, retaining the rounded `displayed_value` strings, including scientific notation |
| [recorded_test_metrics.csv](recorded_test_metrics.csv) | Cell 31 test table, retaining the rounded `displayed_value` strings |
| [validation_threshold_table.txt](validation_threshold_table.txt) | Complete saved cell 28 table display: nine thresholds, with some columns abbreviated by pandas |
| [training_log.txt](training_log.txt) | Saved stdout from cells 21 and 22, with terminal ANSI styling removed |
| [recorded_verification_checks.txt](recorded_verification_checks.txt) | Successful messages from patient split, training-metric, model reload, and evaluation checks in cells 10, 16, 23, and 27 |
| [recorded_run_summary.json](recorded_run_summary.json) | Documented transcription of the recorded configuration, displayed metrics, definitions, checks, and figure provenance |

The original full-precision runtime CSV/JSON files were **not supplied**. These are explicitly named recorded-output transcriptions, not replacements claiming the original precision. Values in scientific notation may round integer pixel counts: **do not treat these displayed counts as exact counts for recomputation**. No hidden threshold columns or per-image results were invented.

## Interpretation and scope

The checkpoint is selected by validation loss; the threshold is selected on validation Global Dice before the recorded test evaluation. Metrics are pixel-pooled or slice-average values at 256 × 256. The 378 test slices come from 11 patients; these are not 378 independent patients, patient-wise scores, or 3D volume metrics.

The latest run has higher test Global Dice/IoU and fewer false-positive empty slices than the prior recorded V2 run, but lower positive-slice Mean Dice and recall. Both are separate training runs with different recorded TensorFlow versions, so the differences cannot be attributed solely to code changes. See [the main README comparison](../README.md#comparison-with-the-prior-recorded-v2-run).

The saved `.keras` model, all individual prediction masks, and original runtime metrics files are not embedded in the supplied notebook and are not included here. Raw datasets, credentials, large checkpoints, and run archives are excluded.
