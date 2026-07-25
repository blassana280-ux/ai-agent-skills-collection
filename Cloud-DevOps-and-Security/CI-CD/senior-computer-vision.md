---
name: senior-computer-vision
description: "Computer vision engineering skill for object detection, image segmentation, and visual AI systems. Covers CNN and Vision Transformer architectures, YOLO/Faster R-CNN/DETR detection, Mask R-CNN/SAM segmentation, and production deployment with ONNX/TensorRT. Includes PyTorch, torchvision, Ultralytics, Detectron2, and MMDetection frameworks. Use when building detection pipelines, training custom models, optimizing inference, or deploying vision systems."
---

# Senior Computer Vision Engineer

Production computer vision engineering skill for object detection, image segmentation, and visual AI system deployment.

## Table of Contents

- [Quick Start](#quick-start)
- [Core Expertise](#core-expertise)
- [Tech Stack](#tech-stack)
- [Workflow 1: Object Detection Pipeline](#workflow-1-object-detection-pipeline)
- [Workflow 2: Model Optimization and Deployment](#workflow-2-model-optimization-and-deployment)
- [Workflow 3: Custom Dataset Preparation](#workflow-3-custom-dataset-preparation)
- [Architecture Selection Guide](#architecture-selection-guide)
- [Reference Documentation](#reference-documentation)

## Quick Start

```bash
# Generate training configuration for YOLO or Faster R-CNN
python scripts/vision_model_trainer.py models/ --task detection --arch yolov8

# Analyze model for optimization opportunities (quantization, pruning)
python scripts/inference_optimizer.py model.pt --target onnx --benchmark

# Build dataset pipeline with augmentations
python scripts/dataset_pipeline_builder.py images/ --format coco --augment
```

## Core Expertise

This skill provides guidance on:

- **Object Detection**: YOLO family (v5-v11), Faster R-CNN, DETR, RT-DETR
- **Instance Segmentation**: Mask R-CNN, YOLACT, SOLOv2
- **Semantic Segmentation**: DeepLabV3+, SegFormer, SAM (Segment Anything)
- **Image Classification**: ResNet, EfficientNet, Vision Transformers (ViT, DeiT)
- **Video Analysis**: Object tracking (ByteTrack, SORT), action recognition
- **3D Vision**: Depth estimation, point cloud processing, NeRF
- **Production Deployment**: ONNX, TensorRT, OpenVINO, CoreML

## Tech Stack

| Category | Technologies |
|----------|--------------|
| Frameworks | PyTorch, torchvision, timm |
| Detection | Ultralytics (YOLO), Detectron2, MMDetection |
| Segmentation | segment-anything, mmsegmentation |
| Optimization | ONNX, TensorRT, OpenVINO, torch.compile |
| Image Processing | OpenCV, Pillow, albumentations |
| Annotation | CVAT, Label Studio, Roboflow |
| Experiment Tracking | MLflow, Weights & Biases |
| Serving | Triton Inference Server, TorchServe |

## Workflow 1: Object Detection Pipeline

Use this workflow when building an object detection system from scratch.

### Step 1: Define Detection Requirements

Analyze the detection task requirements:

```
Detection Requirements Analysis:
- Target objects: [list specific classes to detect]
- Real-time requirement: [yes/no, target FPS]
- Accuracy priority: [speed vs accuracy trade-off]
- Deployment target: [cloud GPU, edge device, mobile]
- Dataset size: [number of images, annotations per class]
```

### Step 2: Select Detection Architecture

Choose architecture based on requirements:

| Requirement | Recommended Architecture | Why |
|-------------|-------------------------|-----|
| Real-time (30 FPS) | YOLOv8/v11, RT-DETR | Single-stage, optimized for speed |
| High accuracy | Faster R-CNN, DINO | Two-stage, better localization |
| Small objects | YOLO + SAHI, Faster R-CNN + FPN | Multi-scale detection |
| Edge deployment | YOLOv8n, MobileNetV3-SSD | Lightweight architectures |
| Transformer-based | DETR, DINO, RT-DETR | End-to-end, no NMS required |

### Step 3: Prepare Dataset

Convert annotations to required format:

```bash
# COCO format (recommended)
python scripts/dataset_pipeline_builder.py data/images/ \
    --annotations data/labels/ \
    --format coco \
    --split 0.8 0.1 0.1 \
    --output data/coco/

# Verify dataset
python -c "from pycocotools.coco import COCO; coco = COCO('data/coco/train.json'); print(f'Images: {len(coco.imgs)}, Categories: {len(coco.cats)}')"
```

### Step 4: Configure Training

Generate training configuration:

```bash
# For Ultralytics YOLO
python scripts/vision_model_trainer.py data/coco/ \
    --task detection \
    --arch yolov8m \
    --epochs 100 \
    --batch 16 \
    --imgsz 640 \
    --output configs/

# For Detectron2
python scripts/vision_model_trainer.py data/coco/ \
    --task detection \
    --arch faster_rcnn_R_50_FPN \
    --framework detectron2 \
    --output configs/
```

### Step 5: Train and Validate

```bash
# Ultralytics training
yolo detect train data=data.yaml model=yolov8m.pt epochs=100 imgsz=640

# Detectron2 training
python train_net.py --config-file configs/faster_rcnn.yaml --num-gpus 1

# Validate on test set
yolo detect val model=runs/detect/train/weights/best.pt data=data.yaml
```

### Step 6: Evaluate Results

Key metrics to analyze:

| Metric | Target | Description |
|--------|--------|-------------|
| mAP@50 | 0.7 | Mean Average Precision at IoU 0.5 |
| mAP@50:95 | 0.5 | COCO primary metric |
| Precision | 0.8 | Low false positives |
| Recall | 0.8 | Low missed detections |
| Inference time | 10,000 | 90% | 5% | 5% |

### Step 6: Generate Dataset Configuration

```bash
# For Ultralytics YOLO
python scripts/dataset_pipeline_builder.py data/final/ \
    --generate-config yolo \
    --output data.yaml

# For Detectron2
python scripts/dataset_pipeline_builder.py data/final/ \
    --generate-config detectron2 \
    --output detectron2_config.py
```

## Architecture Selection Guide

### Object Detection Architectures

| Architecture | Speed | Accuracy | Best For |
|--------------|-------|----------|----------|
| YOLOv8n | 1.2ms | 37.3 mAP | Edge, mobile, real-time |
| YOLOv8s | 2.1ms | 44.9 mAP | Balanced speed/accuracy |
| YOLOv8m | 4.2ms | 50.2 mAP | General purpose |
| YOLOv8l | 6.8ms | 52.9 mAP | High accuracy |
| YOLOv8x | 10.1ms | 53.9 mAP | Maximum accuracy |
| RT-DETR-L | 5.3ms | 53.0 mAP | Transformer, no NMS |
| Faster R-CNN R50 | 46ms | 40.2 mAP | Two-stage, high quality |
| DINO-4scale | 85ms | 49.0 mAP | SOTA transformer |

### Segmentation Architectures

| Architecture | Type | Speed | Best For |
|--------------|------|-------|----------|
| YOLOv8-seg | Instance | 4.5ms | Real-time instance seg |
| Mask R-CNN | Instance | 67ms | High-quality masks |
| SAM | Promptable | 50ms | Zero-shot segmentation |
| DeepLabV3+ | Semantic | 25ms | Scene parsing |
| SegFormer | Semantic | 15ms | Efficient semantic seg |

### CNN vs Vision Transformer Trade-offs

| Aspect | CNN (YOLO, R-CNN) | ViT (DETR, DINO) |
|--------|-------------------|------------------|
| Training data needed | 1K-10K images | 10K-100K+ images |
| Training time | Fast | Slow (needs more epochs) |
| Inference speed | Faster | Slower |
| Small objects | Good with FPN | Needs multi-scale |
| Global context | Limited | Excellent |
| Positional encoding | Implicit | Explicit |

## Reference Documentation
→ See references/reference-docs-and-commands.md for details

## Performance Targets

| Metric | Real-time | High Accuracy | Edge |
|--------|-----------|---------------|------|
| FPS | 30 | 10 | 15 |
| mAP@50 | 0.6 | 0.8 | 0.5 |
| Latency P99 | 50ms | 150ms | 100ms |
| GPU Memory | 4GB | 8GB | 2GB |
| Model Size | 50MB | 200MB | 20MB |

## Resources

- **Architecture Guide**: `references/computer_vision_architectures.md`
- **Optimization Guide**: `references/object_detection_optimization.md`
- **Deployment Guide**: `references/production_vision_systems.md`
- **Scripts**: `scripts/` directory for automation tools
