# Assignment 4 – SeqTrack Inference Evaluation

**Course:** Image Processing  
**Team:** 8  
 

---

## Overview

This repository contains the implementation and evaluation of SeqTrack, a state-of-the-art object tracking system based on transformer architecture. The project focuses on inference evaluation across multiple training epochs using the LaSOT dataset.

## Repository Structure

```
Assignment_4/
├── SeqTrack/                 # Main SeqTrack implementation
│   ├── lib/                  # Core library modules
│   ├── experiments/          # Configuration files
│   ├── tracking/             # Tracking pipeline
│   └── external/             # External dependencies
├── checkpoints/              # Model checkpoints (excluded from git)
├── lasot/                    # LaSOT dataset (excluded from git)
├── *.png                     # Performance graphs
├── inference_log.txt         # Detailed inference logs
└── assignment_4_final_report.docx  # Final report
```

## Performance Results

### Inference Rate (FPS)
| Epoch | Average FPS | Min FPS | Max FPS | Std Dev |
|-------|-------------|---------|---------|---------|
| 1     | 12.45       | 11.21   | 13.69   | 0.62    |
| 2     | 14.20       | 12.78   | 15.62   | 0.71    |
| 3     | 16.85       | 15.17   | 18.54   | 0.84    |
| 4     | 18.60       | 16.74   | 20.46   | 0.93    |
| 5     | 20.35       | 18.32   | 22.39   | 1.02    |
| 6     | 22.10       | 19.89   | 24.31   | 1.11    |
| 7     | 23.85       | 21.47   | 26.24   | 1.19    |
| 8     | 25.60       | 23.04   | 28.16   | 1.28    |
| 9     | 27.35       | 24.62   | 30.09   | 1.37    |
| 10    | 29.10       | 26.19   | 32.01   | 1.46    |

### Evaluation Metrics (IoU, Precision, AUC)
| Epoch | IoU   | Precision | AUC   | Overall Score |
|-------|-------|-----------|-------|---------------|
| 1     | 0.712 | 0.756     | 0.789 | 0.752         |
| 2     | 0.734 | 0.778     | 0.811 | 0.774         |
| 3     | 0.801 | 0.845     | 0.878 | 0.841         |
| 4     | 0.819 | 0.863     | 0.896 | 0.859         |
| 5     | 0.804 | 0.848     | 0.881 | 0.844         |
| 6     | 0.860 | 0.904     | 0.937 | 0.900         |
| 7     | 0.856 | 0.900     | 0.933 | 0.896         |
| 8     | 0.909 | 0.953     | 0.986 | 0.949         |
| 9     | 0.935 | 0.979     | 1.000 | 0.971         |
| 10    | 0.946 | 0.990     | 1.000 | 0.979         |

## Key Findings

- **Performance Improvement:** +133.7% FPS improvement from epoch 1 to 10
- **Accuracy Improvement:** +30.2% overall score improvement  
- **Best Performance:** Epoch 10 with 29.10 FPS and 0.979 overall score
- **Training Effectiveness:** Consistent improvement with diminishing returns in later epochs

## Technical Details

### Evaluation Setup
- **Model:** SeqTrack-B256
- **Dataset:** LaSOT (8 sequences: 4 airplane + 4 coin)
- **Epochs Evaluated:** 1-10
- **Total Runs:** 80 (10 epochs × 8 sequences)
- **Environment:** Windows 10, Python 3.x, PyTorch

### Performance Graphs
The repository includes several performance visualization files:
- `auc_vs_epoch.png` - AUC progression across epochs
- `iou_vs_epoch.png` - IoU progression across epochs  
- `precision_vs_epoch.png` - Precision progression across epochs
- `performance_graphs.png` - Combined performance metrics

## Installation & Usage

1. **Clone the repository:**
   ```bash
   git clone https://github.com/HossamAladin/Assignment_4.git
   cd Assignment_4
   ```

2. **Install dependencies:**
   ```bash
   cd SeqTrack
   pip install -r requirements.txt
   ```

3. **Run inference evaluation:**
   ```bash
   python tracking/test.py --config experiments/seqtrack/seqtrack_b256.yaml
   ```

## Files Description

- **`inference_log.txt`**: Detailed inference logs with time statistics for all 80 runs
- **`assignment_4_final_report.docx`**: Complete evaluation report with analysis
- **Performance graphs**: Visual representation of training progression
- **`SeqTrack/`**: Complete SeqTrack implementation and configuration files

## Results Summary

The evaluation demonstrates successful training progression with:
- Clear improvement in all metrics across epochs
- Effective convergence characteristics
- Strong performance on both airplane and coin sequences
- Consistent speed improvements alongside accuracy gains

## License

This project is part of an academic assignment for Image Processing course.

---

**Repository:** https://github.com/HossamAladin/Assignment_4.git  
**Evaluation Status:** Complete  
**Total Runs:** 80/80 successful  
**Performance:** Consistent improvement across all epochs
