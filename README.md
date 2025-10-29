### Assignment 4 – SeqTrack Inference Evaluation (Guide + Index)

This README maps every assignment requirement to the exact files/folders, summarizes the results, and guides you to graphs, logs, configs, and code. It’s the single entry point for anyone browsing this repo.

Repository: `https://github.com/HossamAladin/Assignment_4.git`

### What we did (summary)
- Model: SeqTrack-B256
- Dataset: LaSOT (8 sequences: 4 airplane + 4 coin)
- Epochs evaluated: 1–10 (full-length sequences, no frame sampling)
- Metrics: IoU, Precision, AUC per epoch; FPS and ms/frame from per-sequence timings

Key results
- Best AUC: 24.91% (epoch 9)
- Best IoU: 24.91% (epoch 9)
- Best Precision: 27.24% (epoch 5)
- Average FPS: ~18.30

### Where to find things quickly
- Graphs (evaluation)
  - `testing/evaluation_graph.png` – IoU/Precision/AUC vs epoch (overview)
  - `testing/evaluation_auc_graph.png` – AUC vs epoch
  - `testing/evaluation_fps_graph.png` – FPS vs epoch
  - `testing/evaluation_class_iou.png` – Class-wise IoU
  - `testing/evaluation_class_auc.png` – Class-wise AUC
  - `testing/evaluation_class_precision.png` – Class-wise Precision
- Logs and summaries
  - `testing/inference_logs/inference_log.txt` – Per-sequence timings + per-epoch summary (frames, total time, FPS, ms/frame)
  - `testing/evaluation_results.json` – Per-epoch metrics + timing (machine-readable)
- Per-epoch raw results
  - `testing/results/seqtrack/seqtrack_b256_XXX/lasot/*.txt` – Tracker outputs
  - `testing/results/seqtrack/seqtrack_b256_XXX/lasot/*_time.txt` – Per-sequence timing arrays
- Final report
  - `assignment_4_final_report.docx` – Final write-up with tables/figures
- Evaluation code & config
  - `SeqTrack/evaluate_checkpoints.py` – Evaluates checkpoints across epochs, writes JSON/logs and plots
  - `SeqTrack/experiments/seqtrack/seqtrack_b256.yaml` – Active experiment configuration used here

### How each requirement is satisfied
- Full-length sequences (no frame sampling): evidenced by per-sequence totals in `testing/inference_logs/inference_log.txt`
- Inference tables/graphs: present in the DOCX and PNGs under `testing/`
- Per-epoch (1–10) evaluation: summarized in the graphs and JSON; best epochs noted above
- Reflections: included in the report (and also drafted in the project’s Markdown version earlier)
- GitHub submission: this repository

### Reproduce the evaluation
1) Setup
```bash
git clone https://github.com/HossamAladin/Assignment_4.git
cd Assignment_4/SeqTrack
pip install -r requirements.txt
```
2) Data/Checkpoints
- Configure dataset paths (see `lib/test/evaluation/local.py`)
- Place checkpoints under `training_runs/...` or pass `--checkpoint_dir`
3) Run
```bash
python evaluate_checkpoints.py \
  --tracker_name seqtrack \
  --tracker_param seqtrack_b256 \
  --dataset_name lasot \
  --start_epoch 1 \
  --end_epoch 10
```
Outputs
- Logs: `testing/inference_logs/inference_log.txt`
- Summary JSON: `testing/evaluation_results.json`
- Results: `testing/results/seqtrack/seqtrack_b256_XXX/lasot/*.txt` and `*_time.txt`

### Repository structure (detailed)
```
Assignment_4/
├── SeqTrack/                         # Main project code
│   ├── experiments/seqtrack/         # YAML configs (active: seqtrack_b256.yaml)
│   ├── evaluate_checkpoints.py       # Evaluation driver (epochs, metrics, timing)
│   ├── tracking/                     # Test/train entry points
│   └── lib/                          # Core libraries (models, eval utils)
├── testing/                          # All evaluation artifacts
│   ├── evaluation_graph.png          # Overview metrics (IoU/Precision/AUC)
│   ├── evaluation_auc_graph.png      # AUC vs epoch
│   ├── evaluation_fps_graph.png      # FPS vs epoch
│   ├── evaluation_class_iou.png      # Class-wise IoU
│   ├── evaluation_class_auc.png      # Class-wise AUC
│   ├── evaluation_class_precision.png# Class-wise Precision
│   ├── evaluation_results.json       # Machine-readable summary per epoch
│   ├── inference_logs/inference_log.txt
│   └── results/seqtrack/seqtrack_b256_XXX/lasot/
│       ├── <sequence>.txt            # Tracking outputs
│       └── <sequence>_time.txt       # Per-sequence timings
├── assignment_4_final_report.docx    # Final report
└── README.md                         # This guide
```

### Notes
- Epoch 9 is the strongest overall (AUC/IoU); epoch 5 peaks in Precision.
- FPS remains ~18–19 across epochs (≈52–56 ms/frame), indicating stable runtime.
- Class-wise plots show airplane outperforming coin from epoch 5 onward.
