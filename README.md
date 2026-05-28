# Digital-Image-Processing-Project
#**COM 4504 Digital Image Processing - Emine Binay**

## Real-Time Object Detection in Aerial Images (UAV)
### Emine Binay | Ankara University

---

## Project Overview

This repository contains my technical work for the COM 4504 Digital Image Processing course project. The project develops a real-time object detection and multi-object tracking pipeline for UAV (drone) aerial imagery using YOLOv8, SAHI, and ByteTrack on the VisDrone2019 dataset.
  
**Platform:** Kaggle (Tesla T4 GPU)  

---

## My Responsibilities

### Phase 1 — Data Preparation
- VisDrone2019 dataset analysis and annotation format inspection
- VisDrone → YOLO format conversion script (coordinate normalization)
- Random erasing augmentation implementation
- Class distribution visualization (per-class histogram)

### Phase 2 — Model Training
- HOG+SVM classical ML baseline (comparison purposes)
- Baseline YOLOv8n training (30 epochs, SAHI-free)
- SAHI integration and patch size/overlap experiments
- NMS fusion implementation for duplicate bounding box elimination
- Pipeline FPS measurement and latency decomposition

### Phase 3 — Evaluation
- MOTA and IDF1 metric computation, ID switch analysis
- SORT vs DeepSORT vs ByteTrack tracker comparison
- HOG+SVM vs Baseline DL vs Proposed System comparison
- Performance Evaluation section (Section 4) drafting

---

## Key Results

| Method | mAP@50 | FPS |
|--------|--------|-----|
| HOG+SVM (Classical ML) | ~4–5% | Moderate |
| YOLOv8n Baseline (no SAHI) | **41.6%** | **38.8** |
| YOLOv8n + SAHI | 41.6%+ | 3.7 |

| Tracker | MOTA | IDF1 | ID Switches |
|---------|------|------|-------------|
| SORT | 42.3% | 47.8% | 312 |
| DeepSORT | 51.2% | 57.4% | 198 |
| **ByteTrack** | **62.1%** | **67.8%** | **89** |

### Pipeline Latency
