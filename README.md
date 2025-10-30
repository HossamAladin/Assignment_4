# Assignment 4  SeqTrack Inference Evaluation (Guide + Index)

This README maps every assignment requirement to the exact files/folders, summarizes the results, and guides you to graphs, logs, configs, and code. Itâ€™s the single entry point for anyone browsing this repo.

Repository: https://github.com/HossamAladin/Assignment_4.git

## What we did (summary)

- Model: SeqTrack-B256
- Dataset: LaSOT (8 sequences: 4 airplane + 4 coin)
- Epochs evaluated: 1â€“10 (full-length sequences, no frame sampling)
- Metrics: IoU, Precision, AUC per epoch; FPS and ms/frame from per-sequence timings

Key results

- Best AUC: 24.91% (epoch 9)
- Best IoU: 24.91% (epoch 9)
- Best Precision: 27.24% (epoch 5)
- Average FPS: ~18.30

## Where to find things quickly

- **Graphs (evaluation)**
  - 	esting/evaluation_graph.png â€“ IoU/Precision/AUC vs epoch (overview)
  - 	esting/evaluation_auc_graph.png â€“ AUC vs epoch
  - 	esting/evaluation_fps_graph.png â€“ FPS vs epoch
  - 	esting/evaluation_class_iou.png â€“ Class-wise IoU
  - 	esting/evaluation_class_auc.png â€“ Class-wise AUC
  - 	esting/evaluation_class_precision.png â€“ Class-wise Precision
- **Logs and summaries**
  - 	esting/inference_logs/inference_log.txt â€“ Per-sequence timings + per-epoch summary (frames, total time, FPS, ms/frame) as recorded alongside the results.
  - 	esting/evaluation_results.json â€“ Per-epoch metrics with timing, written together with the analysis outputs.
- **Per-epoch raw results**
  - 	esting/results/seqtrack/seqtrack_b256_XXX/lasot/*.txt â€“ Tracker outputs
  - 	esting/results/seqtrack/seqtrack_b256_XXX/lasot/*_time.txt â€“ Per-sequence timing arrays
- **Documentation (final report)**
  - 	esting/Assignment(4).docx â€“ Project documentation with tables, figures, and reflections
- **Evaluation code & config**
  - SeqTrack/evaluate_checkpoints.py â€“ Evaluates checkpoints across epochs, writes JSON/logs and plots
  - SeqTrack/experiments/seqtrack/seqtrack_b256.yaml â€“ Active experiment configuration used here

## How each requirement is satisfied

- Full-length sequences (no frame sampling): evidenced by per-sequence totals in 	esting/inference_logs/inference_log.txt
- Inference tables/graphs: present in 	esting/Assignment(4).docx and the PNGs under 	esting/
- Per-epoch (1â€“10) evaluation: summarized in the graphs and JSON; best epochs noted above
- Reflections: included in 	esting/Assignment(4).docx
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
- Place checkpoints under 	raining_runs/... or pass --checkpoint_dir

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

- Logs: 	esting/inference_logs/inference_log.txt
- Summary JSON: 	esting/evaluation_results.json
- Results: 	esting/results/seqtrack/seqtrack_b256_XXX/lasot/*.txt and *_time.txt

## Repository structure (detailed)

`
Assignment_4/
â”œâ”€â”€ SeqTrack/                         # Main project code
â”‚   â”œâ”€â”€ experiments/seqtrack/         # YAML configs (active: seqtrack_b256.yaml)
â”‚   â”œâ”€â”€ evaluate_checkpoints.py       # Evaluation driver (epochs, metrics, timing)
â”‚   â”œâ”€â”€ tracking/                     # Test/train entry points
â”‚   â””â”€â”€ lib/                          # Core libraries (models, eval utils)
â”œâ”€â”€ testing/                          # All evaluation artifacts
â”‚   â”œâ”€â”€ Assignment(4).docx            # Final project documentation
â”‚   â”œâ”€â”€ evaluation_graph.png          # Overview metrics (IoU/Precision/AUC)
â”‚   â”œâ”€â”€ evaluation_auc_graph.png      # AUC vs epoch
â”‚   â”œâ”€â”€ evaluation_fps_graph.png      # FPS vs epoch
â”‚   â”œâ”€â”€ evaluation_class_iou.png      # Class-wise IoU
â”‚   â”œâ”€â”€ evaluation_class_auc.png      # Class-wise AUC
â”‚   â”œâ”€â”€ evaluation_class_precision.png# Class-wise Precision
â”‚   â”œâ”€â”€ evaluation_results.json       # Machine-readable summary per epoch
â”‚   â”œâ”€â”€ inference_logs/inference_log.txt
â”‚   â””â”€â”€ results/seqtrack/seqtrack_b256_XXX/lasot/
â”‚       â”œâ”€â”€ <sequence>.txt            # Tracking outputs
â”‚       â””â”€â”€ <sequence>_time.txt       # Per-sequence timings
â””â”€â”€ README.md                         # This guide
`

## Notes

- Epoch 9 is the strongest overall (AUC/IoU); epoch 5 peaks in Precision.
- FPS remains ~18â€“19 across epochs (â‰ˆ52â€“56 ms/frame), indicating stable runtime.
- Class-wise plots show airplane outperforming coin from epoch 5 onward.

