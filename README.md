# COM 4504 — Digital Image Processing Project
## Real-Time Object Detection in Aerial Images (UAV)
### Emine Binay | Ankara University

---

## Project Overview

This repository contains my technical contributions to the COM 4504 Digital Image Processing course project. The project develops a real-time object detection and multi-object tracking pipeline for UAV (drone) aerial imagery using YOLOv8, SAHI, and ByteTrack on the VisDrone2019 dataset.

- **Platform:** Kaggle (Tesla T4 GPU)


---

## My Responsibilities

### Phase 1 — Data Preparation (Days 1–4)
- VisDrone2019 dataset analysis and annotation format inspection
- VisDrone → YOLO format conversion (coordinate normalization formulas)
- Random Erasing augmentation implementation
- Class distribution visualization (per-class histogram, 343,205 instances)

### Phase 2 — Model Training (Days 5–10)
- HOG+SVM classical ML baseline setup and training
- Baseline YOLOv8n training without SAHI (30 epochs, batch=16)
- SAHI integration: patch size and overlap ratio experiments
- NMS fusion implementation for duplicate bounding box elimination
- Pipeline FPS measurement and latency decomposition

### Phase 3 — Evaluation and Analysis (Days 11–15)
- MOTA and IDF1 metric computation, ID switch count analysis
- SORT vs DeepSORT vs ByteTrack tracker comparison
- HOG+SVM vs Baseline DL vs Proposed System comparison
- Performance Evaluation (Section 4) drafting with all tables

---

## Key Results

### Detection Performance

| Method | mAP@50 | mAP@50:95 | FPS |
|--------|--------|-----------|-----|
| HOG+SVM (Classical ML) | ~4–5% | ~2–3% | Moderate |
| YOLOv8n Baseline — no SAHI (ours) | **41.6%** | **28.3%** | **38.8** |
| YOLOv8n + SAHI (ours) | 41.6%+ | — | 3.7 |
| TPH-YOLOv5 (literature) | ~26–28% | ~17–19% | ~12 |
| YOLC (literature) | ~29–31% | ~19–21% | ~18 |

### Multi-Object Tracking Performance

| Tracker | MOTA | IDF1 | ID Switches | FPS |
|---------|------|------|-------------|-----|
| SORT | 42.3% | 47.8% | 312 | 28.5 |
| DeepSORT | 51.2% | 57.4% | 198 | 18.2 |
| **ByteTrack (ours)** | **62.1%** | **67.8%** | **89** | **35.6** |

### Pipeline Latency Decomposition

| Component | Latency | FPS |
|-----------|---------|-----|
| Preprocessing | 1.51 ms | 662 |
| YOLOv8n Inference | 24.16 ms | 41.4 |
| NMS Post-processing | 0.09 ms | >10,000 |
| **Full Pipeline (no SAHI)** | **25.77 ms** | **38.8** |
| Full Pipeline (with SAHI) | 243.7 ms | 4.1 |

> Target: 25 FPS — **EXCEEDED ✓**

### SAHI Comparison (5 validation images)

| | Without SAHI | With SAHI | Difference |
|--|-------------|-----------|------------|
| Avg. detections per image | 45.6 | 107.4 | **+135%** |
| Avg. inference time | 65.3 ms | 269.4 ms | 4.1× slower |

---

## Repository Contents

| File | Description |
|------|-------------|
| `emine-dip-project.ipynb` | Main Kaggle notebook — all code and outputs |
| `class_distribution.png` | VisDrone2019 class imbalance visualization |
| `random_erasing_examples.png` | Random Erasing augmentation examples |
| `sahi_comparison.png` | SAHI vs no-SAHI detection comparison chart |
| `latency_analysis.png` | Pipeline component latency bar chart |
| `tracker_comparison.png` | SORT vs DeepSORT vs ByteTrack comparison |
| `hog_svm_results.json` | HOG+SVM classification results |
| `sahi_comparison_results.json` | SAHI quantitative comparison data |
| `latency_results.json` | Pipeline latency measurements |
| `tracker_results.json` | Tracker comparison metrics |

---

## Dataset

**VisDrone2019-DET** — AISKYEYE Team, Tianjin University, China

| Split | Images | Instances |
|-------|--------|-----------|
| Train | 6,471 | 343,205 |
| Validation | 548 | ~29,000 |

**10 object categories:** pedestrian, people, bicycle, car, van, truck, tricycle, awning-tricycle, bus, motor

**Class distribution (train):**
- car: 144,867 (42.2%) — most frequent
- pedestrian: 79,337 (23.1%)
- awning-tricycle: 3,246 (0.9%) — least frequent

**Object size analysis:** 59.8% of instances are small objects (<32×32 px), motivating SAHI integration.

---

## Environment

| | |
|--|--|
| Platform | Kaggle Notebooks |
| GPU | Tesla T4 x2 (14,913 MiB each) |
| Python | 3.12 |
| ultralytics | 8.x |
| sahi | 0.11.x |
| supervision | latest |
| albumentations | 1.3.x |

---

## How to Run

1. Open `emine-dip-project.ipynb` on Kaggle
2. Add VisDrone dataset as input
3. Select GPU T4 x2 as accelerator
4. Run cells sequentially

---
