# Assignment 4 - SeqTrack Inference Evaluation (Guide + Index)

This README maps requirements to files/folders, summarizes results, and links to graphs, logs, configs, and code.

Repository: https://github.com/HossamAladin/Assignment_4.git

## What we did (summary)
- Model: SeqTrack-B256
- Dataset: LaSOT (8 sequences: 4 airplane + 4 coin)
- Epochs evaluated: 1-10 (full-length sequences, no frame sampling)
- Metrics: IoU, Precision, AUC per epoch; FPS and ms/frame from per-sequence timings

### Overall Performance Highlights
- IoU grew about 6x: 4.21% (Epoch 1) -> 24.39% (Epoch 10)
- Precision improved about 6.8x: 3.48% (Epoch 1) -> 23.82% (Epoch 10)
- Rapid learning: big jump from Epoch 4 to 5 (2.53% -> 14.41% IoU)
- Recovery and peak: dip at Epoch 7 (10.99% IoU), peak IoU 24.91% at Epoch 9

### Class-Specific Success
- Airplane: IoU 3.99% -> 30.13% (Epoch 10); Precision 1.86% -> 41.35%
- Coin: IoU 4.42% -> 18.64% (Epoch 10); Precision 6.28% (challenging class)

## Where to find things quickly
- Graphs (evaluation)
  - testing/evaluation_graph.png - IoU/Precision/AUC vs epoch (overview)
  - testing/evaluation_auc_graph.png - AUC vs epoch
  - testing/evaluation_fps_graph.png - FPS vs epoch
  - testing/evaluation_class_iou.png - Class-wise IoU
  - testing/evaluation_class_auc.png - Class-wise AUC
  - testing/evaluation_class_precision.png - Class-wise Precision
- Logs and summaries
  - testing/inference_logs/inference_log.txt - Per-sequence timings and per-epoch summary
  - testing/evaluation_results.json - Per-epoch metrics with timing
- Per-epoch raw results
  - testing/results/seqtrack/seqtrack_b256_XXX/lasot/*.txt - Tracker outputs
  - testing/results/seqtrack/seqtrack_b256_XXX/lasot/*_time.txt - Per-sequence timing arrays
- Documentation (final report)
  - testing/Assignment(4).docx - Project documentation with tables, figures, reflections
- Evaluation code and config
  - SeqTrack/evaluate_checkpoints.py - Evaluates checkpoints, writes JSON/logs and plots
  - SeqTrack/experiments/seqtrack/seqtrack_b256.yaml - Active experiment configuration

## How each requirement is satisfied
- Full-length sequences (no frame sampling): see totals in testing/inference_logs/inference_log.txt
- Inference tables/graphs: in testing/Assignment(4).docx and PNGs under testing/
- Per-epoch (1-10) evaluation: summarized in graphs and JSON; best epochs noted above
- Reflections: included in testing/Assignment(4).docx
- GitHub submission: this repository

## Reproduce the evaluation

1. Setup
`ash
git clone https://github.com/HossamAladin/Assignment_4.git
cd Assignment_4/SeqTrack
pip install -r requirements.txt
`

2. Data/Checkpoints
- Configure dataset paths (see lib/test/evaluation/local.py)
- Place checkpoints under training_runs/... or pass --checkpoint_dir

3. Run
`ash
python evaluate_checkpoints.py \
  --tracker_name seqtrack \
  --tracker_param seqtrack_b256 \
  --dataset_name lasot \
  --start_epoch 1 \
  --end_epoch 10
`

Outputs
- Logs: testing/inference_logs/inference_log.txt
- Summary JSON: testing/evaluation_results.json
- Results: testing/results/seqtrack/seqtrack_b256_XXX/lasot/*.txt and *_time.txt

## Repository structure (detailed)
`
Assignment_4/
|-- SeqTrack/
|   |-- experiments/seqtrack/
|   |-- evaluate_checkpoints.py
|   |-- tracking/
|   -- lib/
|-- testing/
|   |-- Assignment(4).docx
|   |-- evaluation_graph.png
|   |-- evaluation_auc_graph.png
|   |-- evaluation_fps_graph.png
|   |-- evaluation_class_iou.png
|   |-- evaluation_class_auc.png
|   |-- evaluation_class_precision.png
|   |-- evaluation_results.json
|   |-- inference_logs/inference_log.txt
|   -- results/seqtrack/seqtrack_b256_XXX/lasot/
|       |-- <sequence>.txt
|       -- <sequence>_time.txt
-- README.md
`

## Notes
- Epoch 9 is strongest overall (AUC/IoU); Epoch 5 peaks in Precision.
- FPS is about 18-19 across epochs (about 52-56 ms/frame), stable runtime.
- Airplane class outperforms coin from Epoch 5 onward.

## 8. Evaluation Setup
- Model: SeqTrack-B256
- Dataset: LaSOT (8 sequences: 4 airplane + 4 coin)
- Epochs: 1-10 (80 runs total)
- Environment: Windows 11, Python 3.x, PyTorch

## 9. Key Findings
- Overall learning: IoU ~6x (4.21%->24.39%), Precision ~6.8x (3.48%->23.82%).
- Airplane specialization: IoU 30.13%, Precision 41.35% (Epoch 10).
- Coin remains challenging: IoU 18.64%, Precision 6.28% (false positives).
