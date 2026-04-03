<div align="center">

# TouchAnything

### The First Dataset and Framework for Bimanual Tactile Estimation from Egocentric Video

[![Project Page](https://img.shields.io/badge/Project-Page-blue)](https://jianyi2004.github.io/TouchAnything-Website/)
[![Paper](https://img.shields.io/badge/Paper-Coming%20Soon-orange)](#)
[![Dataset](https://img.shields.io/badge/Dataset-Coming%20Soon-green)](#)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)

**[Jianyi Zhou](https://github.com/Jianyi2004)<sup>1</sup>, Ziteng Gao<sup>1</sup>, Feiyang Hong<sup>1</sup>, Zirui Liu<sup>1</sup>, Guannan Zhang<sup>1</sup>, Weisheng Dai<sup>1</sup>,**  
**Ruichen Zhen<sup>2</sup>, Haotian Wu<sup>2</sup>, Yinian Mao<sup>2</sup>, Xushi Wang<sup>1</sup>, Yuxiang Jiang<sup>1</sup>, [Shuo Yang](mailto:shuoyang@hit.edu.cn)<sup>1✉</sup>**

<sup>1</sup>Harbin Institute of Technology, Shenzhen &nbsp;&nbsp; <sup>2</sup>Meituan Academy of Robotics

<sup>✉</sup>Corresponding author

---

</div>

## 📢 News

- **[2026-04]** Project website and initial README released
- **[Coming Soon]** Paper submission
- **[Coming Soon]** Dataset release
- **[Coming Soon]** Code release

## 🎯 Overview

We introduce **EgoTouch**, the first large-scale multi-view tactile dataset for egocentric hand-object interaction, comprising **302 diverse manipulation tasks** across **4,530 episodes** in both indoor and outdoor environments. The dataset provides synchronized multi-view video (egocentric + dual wrist cameras), bimanual 3D hand pose (42 joints), and dense continuous pressure maps from wearable tactile sensors.

Building upon this dataset, we propose **TouchAnything**, a unified multi-view tactile prediction architecture that integrates shared vision encoding, cross-view attention, and view dropout strategy. Our experiments demonstrate that incorporating complementary wrist views is crucial for resolving occluded contact regions and enabling reliable tactile inference under severe occlusions.

## ✨ Key Features

- **🎥 Multi-View Capture**: First dataset combining multi-view synchronized video (egocentric + dual wrist cameras) with real tactile pressure data
- **🖐️ Dense Tactile Sensing**: Real continuous pressure distributions from wearable sensors, capturing fine-grained contact dynamics
- **🤲 Bimanual Interaction**: Bimanual manipulation with 42-joint 3D hand pose annotations, enabling analysis of coordinated hand-object interaction
- **🔄 Synchronized Modalities**: Precise frame-level synchronization across video, pose, and pressure, enabling accurate temporal modeling of contact events

## 📊 Dataset Statistics

| Metric | Value |
|--------|-------|
| **Manipulation Tasks** | 302 |
| **Episodes** | 4,530 |
| **Camera Views** | 3 (Ego + Dual Wrist) |
| **Hand Joints** | 42 (Bimanual) |
| **Total Frames** | ~2M |
| **Objects** | 1,000+ |
| **Environments** | Indoor & Outdoor |

## 🔬 Dataset Comparison

EgoTouch is the first dataset to jointly provide multi-view video, bimanual hand pose, and real dense pressure data across diverse scenes.

| Dataset | In-the-wild | Hand Pose | Contact | Wrist Views | Hands | Objects | Frames |
|---------|-------------|-----------|---------|-------------|-------|---------|--------|
| GRAB | ❌ | MoCap | Analytical | ❌ | Biman. | 51 | 1.6M |
| ContactDB | ❌ | ❌ | Thermal | ❌ | Biman. | 50 | 375k |
| ARCTIC | ❌ | MoCap | Analytical | ❌ | Biman. | 11 | 2.1M |
| OakInk | ❌ | MoCap | Analytical | ❌ | Single | 100 | 230k |
| DexYCB | ❌ | Est. | ❌ | ❌ | Single | 20 | 582k |
| ActionSense | ❌ | Glove | Pressure | ❌ | Biman. | 21 | 521k |
| HOI4D | ❌ | Est. | ❌ | ❌ | Single | 800 | 2.4M |
| EgoPressure | ❌ | Est. | Pressure | ❌ | Single | 31 | 4.3M |
| EgoDex | ❌ | Est. | Analytical | ❌ | Biman. | 500 | 90M |
| OpenTouch | ✅ | Glove | Pressure | ❌ | Single | 800 | ~500k |
| **EgoTouch (Ours)** | ✅ | **Glove** | **Pressure** | ✅ | **Biman.** | **1000** | **2M** |

## 🏗️ Main Contributions

1. **First large-scale multi-view tactile dataset** for egocentric hand-object interaction, comprising 302 tasks, 4,530 episodes, bimanual pose, and dense continuous pressure maps across diverse indoor and outdoor scenes

2. **First multi-view tactile prediction benchmark**, including evaluation protocols that quantify the role of complementary wrist views and show clear gains under severe occlusion

3. **New multi-view tactile prediction architecture** with shared vision encoding, cross-view attention, and view dropout, enabling flexible inference with any combination of available views

## 🎬 Model Demo

<div align="center">

### Grasping Thermos

https://github.com/user-attachments/assets/拿保温杯_20260325_171636_233_tactile.mp4

### Handling Hair Dryer

https://github.com/user-attachments/assets/拿吹风机_20260320_094951_941_tactile.mp4

### Grasping Beverage

https://github.com/user-attachments/assets/拿饮料_20260325_163212_035_tactile.mp4

### Picking Up Mouse

https://github.com/user-attachments/assets/拿鼠标2_20260316_215323_166_tactile.mp4

### Bouncing Ping-Pong Ball

https://github.com/user-attachments/assets/颠乒乓球_20260320_172305_280_tactile.mp4

### USB Insertion

https://github.com/user-attachments/assets/插拔USB接口_20260319_115454_872_tactile.mp4

</div>

## 🛠️ Data Collection Setup

<div align="center">
<img src="assets/data_collection.png" width="90%">
</div>

Our data collection system integrates:

- **Head-mounted Wide-Angle Camera**: Captures global manipulation context from a wide-field first-person perspective
- **Dual Wrist Cameras**: Observe hand-object contact regions to overcome occlusion
- **Pressure-Sensing Gloves**: Record dense 16×16 pressure maps on each palm
- **Motion Capture**: Tracks 42-joint bimanual 3D hand pose at 30Hz
- **Temporal Synchronization**: All modalities aligned with millisecond precision

## 🧠 Method Architecture

<div align="center">
<img src="assets/model_architecture.png" width="90%">
</div>

We propose a multi-view tactile prediction model based on:

- **Shared DINOv2 Vision Encoder**: Extracts features from all camera views
- **Learnable View Embeddings**: Distinguishes between egocentric and wrist viewpoints
- **Cross-View Transformer Attention**: Fuses complementary information across views
- **View Dropout Training**: Enables robust inference with missing views

This design allows the model to work with any subset of available views at inference time, from ego-only to full multi-view, making it practical for real-world deployment.

## 📁 Data Format

Each episode is stored as an HDF5 file with the following structure:

```
├── images/
│   ├── chest_color    # (T, 480, 640, 3) egocentric RGB
│   ├── left_color     # (T, 480, 640, 3) left wrist RGB
│   ├── right_color    # (T, 480, 640, 3) right wrist RGB
│   └── *_depth        # (T, 480, 640) depth maps
├── hands/
│   ├── left_joint_xyz         # (T, 21, 3) left hand pose
│   ├── right_joint_xyz        # (T, 21, 3) right hand pose
│   └── *_joint_orientation    # (T, 21, 4) joint quaternions
├── pressure/
│   ├── left_pressure_grid     # (T, 21, 21) normalized [0,1]
│   ├── right_pressure_grid    # (T, 21, 21) normalized [0,1]
│   └── task_vmax (attr)       # task-level normalization factor
├── poses/
│   ├── chest_pose     # (T, 7) camera pose [xyz, quat]
│   ├── left_pose      # (T, 7) left wrist camera pose
│   └── right_pose     # (T, 7) right wrist camera pose
└── metadata/
    ├── task_name, trajectory_id, fps, num_frames
    └── camera_resolution
```

**T**: number of frames per episode (~120 frames @ 30Hz)

## 📦 Installation

> **Coming Soon**: Installation instructions will be provided upon code release.

## 🎯 Quick Start

> **Coming Soon**: Usage examples and tutorials will be provided upon code release.

## 📧 Contact

For questions or collaboration opportunities, please contact:

- **Shuo Yang** (Corresponding Author): [shuoyang@hit.edu.cn](mailto:shuoyang@hit.edu.cn)
- **Jianyi Zhou**: [GitHub](https://github.com/Jianyi2004)

## 🙏 Acknowledgments

This work represents a collaborative effort across multiple domains, from hardware setup to model development and data collection. We thank all team members for their contributions:

- **Jianyi Zhou**: Paper writing, model architecture design, website development, data collection
- **Ziteng Gao**: Data collection pipeline, experimental equipment management, data collection
- **Feiyang Hong**: Codebase organization, paper figure optimization, data collection
- **Zirui Liu**: Paper figure design and illustration, data collection
- **Guannan Zhang**: Project website video editing, data collection
- **Weisheng Dai**: Experimental equipment management, data collection
- **Ruichen Zhen**: Equipment procurement and hardware configuration
- **Haotian Wu**: Data collection hardware setup support
- **Yinian Mao**: High-level guidance and project support
- **Xushi Wang**: HaMeR inference framework development, data collection
- **Yuxiang Jiang**: Data collection participation
- **Shuo Yang**: Research ideation, project supervision, model design consultation, technical guidance

## 📄 License

> **Coming Soon**: License information will be provided upon dataset and code release.

---

<div align="center">

**© 2026 M-PAI Lab, Harbin Institute of Technology, Shenzhen. All rights reserved.**

[Project Page](https://jianyi2004.github.io/TouchAnything-Website/) | [Paper (Coming Soon)](#) | [Dataset (Coming Soon)](#)

</div>
