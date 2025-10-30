# Assignment 4 - SeqTrack Inference Evaluation (Guide + Index)

## What we did (summary)
- Model: SeqTrack-B256
- Dataset: LaSOT (8 sequences: 4 airplane + 4 coin)
- Epochs evaluated: 1-10 (full-length sequences, no frame sampling)
- Metrics: IoU, Precision, AUC per epoch; FPS and ms/frame from per-sequence timings

## Overall Performance Highlights
- IoU grew about 6x: 4.21% (Epoch 1) -> 24.39% (Epoch 10)
- Precision improved about 6.8x: 3.48% (Epoch 1) -> 23.82% (Epoch 10)
- Rapid learning: big jump from Epoch 4 to 5 (2.53% -> 14.41% IoU)
- Recovery and peak: dip at Epoch 7 (10.99% IoU) -> peak IoU 24.91% at Epoch 9

## Class-Specific Success
- Airplane: IoU 3.99% -> 30.13% (Epoch 10); Precision 1.86% -> 41.35%
- Coin: IoU 4.42% -> 18.64% (Epoch 10); Precision remains low at 6.28%

## Where to find things quickly (exact paths)
- Graphs (evaluation)
  - testing/evaluation_graph.png              - IoU/Precision/AUC vs epoch (overview)
  - testing/evaluation_auc_graph.png          - AUC vs epoch
  - testing/evaluation_fps_graph.png          - FPS vs epoch
  - testing/evaluation_class_iou.png          - Class-wise IoU
  - testing/evaluation_class_auc.png          - Class-wise AUC
  - testing/evaluation_class_precision.png    - Class-wise Precision
- Logs and summaries
  - testing/inference_logs/inference_log.txt  - Per-sequence timings and per-epoch summary
  - testing/evaluation_results.json           - Per-epoch metrics with timing
- Per-epoch raw results (tracker outputs and timings)
  - testing/results/seqtrack/seqtrack_b256_XXX/lasot/*.txt        - Predicted boxes per sequence
  - testing/results/seqtrack/seqtrack_b256_XXX/lasot/*_time.txt   - Per-sequence timing arrays
- Documentation (final report)
  - testing/Assignment(4).docx                - Project documentation with tables, figures, reflections
- Evaluation code and config
  - SeqTrack/evaluate_checkpoints.py          - Evaluates checkpoints, writes JSON/logs/plots
  - SeqTrack/experiments/seqtrack/seqtrack_b256.yaml  - Active experiment configuration
- Dataset local path configuration
  - SeqTrack/lib/test/evaluation/local.py     - Edit dataset roots here

## How each requirement is satisfied
- Full-length sequences (no frame sampling): see totals in testing/inference_logs/inference_log.txt
- Inference tables/graphs: in testing/Assignment(4).docx and PNGs under testing/
- Per-epoch (1-10) evaluation: summarized in graphs and JSON; best epochs noted in highlights
- Reflections: included in testing/Assignment(4).docx
- GitHub submission: this repository

## Reproduce the evaluation

1. Setup
```bash
git clone https://github.com/HossamAladin/Assignment_4.git
cd Assignment_4/SeqTrack
pip install -r requirements.txt
```

2. Data/Checkpoints
-Checkpoints at   https://huggingface.co/hossamaladdin/Assignment3/tree/main/checkpoints
- Configure dataset paths (see lib/test/evaluation/local.py)
- Place checkpoints under training_runs/... or pass --checkpoint_dir

3. Run
```bash
python evaluate_checkpoints.py \
  --tracker_name seqtrack \
  --tracker_param seqtrack_b256 \
  --dataset_name lasot \
  --start_epoch 1 \
  --end_epoch 10
```

Outputs
- Logs: testing/inference_logs/inference_log.txt
- Summary JSON: testing/evaluation_results.json
- Results: testing/results/seqtrack/seqtrack_b256_XXX/lasot/*.txt and *_time.txt

## Repository structure (detailed)
```
Assignment_4/
|-- SeqTrack/
|   |-- experiments/seqtrack/
|   |-- evaluate_checkpoints.py
|   |-- tracking/
|   `-- lib/
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
|   `-- results/seqtrack/seqtrack_b256_XXX/lasot/
|       |-- <sequence>.txt
|       `-- <sequence>_time.txt
`-- README.md
```

## 8. Evaluation Setup
- Model: SeqTrack-B256
- Dataset: LaSOT (8 sequences: 4 airplane + 4 coin)
- Epochs: 1-10 (80 runs total)
- Environment: Windows 11, Python 3.x, PyTorch

## 9. Key Findings
- Strong overall learning: IoU up ~6x (4.21% -> 24.39%) and Precision up ~6.8x (3.48% -> 23.82%) by Epoch 10.
- Airplane class excels: Epoch 10 reaches 30.13% IoU and 41.35% Precision (best across epochs).
- Coin class is difficult: improves to 18.64% IoU, but Precision stays low at 6.28% (many false positives).
- Inference is fast and stable: ~18.30 FPS on average (about 54.69 ms/frame); final model runs at ~18.01 FPS.
- Best practical model: Epoch 10 provides the strongest accuracy-speed tradeoff despite coin weakness.

## Notes

-Course: Image Processing

Team: [8]

-GitHub Repository:
https://github.com/HossamAladin/Assignment_4.git




