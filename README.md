# Self-Supervised Pretraining for Autonomous Driving

[![Report PDF](https://img.shields.io/badge/Report-PDF-red?style=flat-square&logo=adobeacrobatreader)](assets/self-supervised-driving-survey.pdf)

This repository is a companion resource for the survey report **Self-Supervised Pretraining on Autonomous Driving Data: A Survey**. The report studies how recent methods use unlabeled or weakly supervised driving data to learn representations for downstream perception, forecasting, occupancy reasoning, and planning-related tasks.

The survey is organized around an objective-first taxonomy. Instead of grouping methods only by sensor modality, it asks what the pretext objective trains the representation to preserve: geometry, BEV structure, occupancy, temporal dynamics, multimodal consistency, trajectory-map context, or latent scene state.

## Taxonomy

| Objective family | Core idea | Example methods |
| --- | --- | --- |
| Masked reconstruction-based pretraining | Hide part of the driving scene and reconstruct spatial or geometric targets. | Voxel-MAE, BEV-MAE |
| Reconstruction-based tokenization | Compress full observations into latent tokens for later world-model prediction. | BEVWorld, RenderWorld |
| Contrastive learning-based pretraining | Learn invariances from temporal, point, segment, or BEV correspondences. | TARL, BEVContrast |
| Rendering-based pretraining | Supervise 3D, voxel, or BEV representations by rendering observed sensor data. | UniPAD, RenderWorld |
| Future prediction-based pretraining | Predict future geometry, occupancy, point clouds, BEV latents, or visual states. | ViDAR, DriveWorld |
| Trajectory-map pretraining | Pretrain on trajectories, road networks, map elements, routes, or local planning signals. | Forecast-MAE, Plan-MAE |
| JEPA-style latent prediction | Predict latent embeddings instead of reconstructing raw observations. | AD-L-JEPA, AD-LiST-JEPA |

> **Note:** World-model papers are treated as boundary cases and are discussed by the specific component most relevant to each pretraining objective.

## Representative Papers

The following list is representative rather than exhaustive. Papers are grouped by the main role they play in the taxonomy, although some methods may naturally belong to more than one category.

### Masked Reconstruction-Based Pretraining

- **Voxel-MAE**: Masked autoencoder pretraining on LiDAR point clouds for voxel-space representation learning. [[paper]](https://doi.org/10.1109/WACVW58289.2023.00039) [[code]](https://github.com/georghess/voxel-mae)
- **Occupancy-MAE**: Masked binary voxel occupancy prediction for large-scale outdoor LiDAR point clouds. [[paper]](https://doi.org/10.1109/TIV.2023.3322409) [[code]](https://github.com/chaytonmin/Occupancy-MAE)
- **BEV-MAE**: BEV-guided masking and point-density prediction for LiDAR point cloud pretraining in autonomous driving. [[paper]](https://doi.org/10.1609/aaai.v38i4.28141) [[code]](https://github.com/VDIGPKU/BEV-MAE)
- **GeoMAE**: Masked geometric target prediction with local geometric quantities such as centroids, normals, curvature, and occupancy. [[paper]](https://arxiv.org/abs/2305.08808) [[code]](https://github.com/Tsinghua-MARS-Lab/GeoMAE)

### Reconstruction-Based Tokenization

- **GAIA-1**: A generative driving world model that first learns discrete image tokens through autoencoding and distillation-style training. [[paper]](https://arxiv.org/abs/2309.17080)
- **OccWorld**: A 3D occupancy world model that learns discrete scene tokens with a VQ-VAE-style occupancy tokenizer. [[paper]](https://arxiv.org/abs/2311.16038) [[code]](https://github.com/wzzheng/OccWorld)
- **BEVWorld**: A multimodal world simulator that tokenizes heterogeneous sensor inputs into scene-level BEV latents. [[paper]](https://arxiv.org/abs/2407.05679) [[code]](https://github.com/zympsyche/BevWorld)
- **Copilot4D**: A LiDAR world-model pipeline that tokenizes sensor observations into discrete latents with a VQ-VAE. [[paper]](https://arxiv.org/abs/2311.01017)
- **RenderWorld**: A world-model pipeline that compresses generated 3D semantic occupancy labels with an AM-VAE for downstream autoregressive forecasting and planning. [[paper]](https://doi.org/10.1109/ICRA55743.2025.11127609)

### Contrastive Learning-Based Pretraining

- **TARL**: Temporal consistent 3D LiDAR representation learning for semantic perception in autonomous driving. [[paper]](https://doi.org/10.1109/CVPR52729.2023.00505) [[code]](https://github.com/PRBonn/TARL)
- **BEVContrast**: Self-supervised contrastive learning in BEV space for automotive LiDAR point clouds. [[paper]](https://doi.org/10.1109/3DV62453.2024.00017) [[code]](https://github.com/valeoai/BEVContrast)
- **PointContrast**: General 3D point cloud contrastive pretraining used as background for driving-specific contrastive methods. [[paper]](https://doi.org/10.1007/978-3-030-58580-8_34) [[code]](https://github.com/facebookresearch/PointContrast)

### Rendering-Based Pretraining

- **UniPAD**: A universal autonomous-driving pretraining paradigm based on volumetric differentiable rendering across camera, LiDAR, and multimodal settings. [[paper]](https://doi.org/10.1109/CVPR52733.2024.01443) [[code]](https://github.com/Nightmare-n/UniPAD)
- **PreWorld**: A semi-supervised vision-centric 3D occupancy world model that uses 2D-label-driven volume rendering during pretraining, followed by supervised fine-tuning for occupancy prediction, forecasting, and planning. [[paper]](https://arxiv.org/abs/2502.07309) [[code]](https://github.com/getterupper/PreWorld)
- **RenderWorld**: Uses a Gaussian-based Img2Occ module with rendering supervision to generate self-supervised 3D semantic occupancy labels for subsequent world-model forecasting and planning. [[paper]](https://doi.org/10.1109/ICRA55743.2025.11127609)

### Future Prediction-Based Pretraining

- **ViDAR**: Visual point cloud forecasting from historical visual inputs with future LiDAR observations as supervision. [[paper]](https://doi.org/10.1109/CVPR52733.2024.01390) [[code]](https://github.com/OpenDriveLab/ViDAR)
- **UnO**: Learns a continuous 4D occupancy field from unlabeled LiDAR data and forecasts future occupancy for perception and forecasting. [[paper]](https://doi.org/10.1109/CVPR52733.2024.01373)
- **DriveWorld**: 4D pre-trained scene understanding through world-model-style occupancy and dynamics prediction. [[paper]](https://doi.org/10.1109/CVPR52733.2024.01470)
- **OccWorld**: Future scene and ego-trajectory prediction in a discrete occupancy-token space. [[paper]](https://arxiv.org/abs/2311.16038) [[code]](https://github.com/wzzheng/OccWorld)
- **BEVWorld**: Action-conditioned future scene simulation in BEV latent space. [[paper]](https://arxiv.org/abs/2407.05679) [[code]](https://github.com/zympsyche/BevWorld)
- **Copilot4D**: Future BEV token prediction with discrete diffusion. [[paper]](https://arxiv.org/abs/2311.01017)
- **RenderWorld**: Future semantic occupancy forecasting using self-supervised 3D occupancy labels and learned occupancy latents. [[paper]](https://doi.org/10.1109/ICRA55743.2025.11127609)
- **Drive-OccWorld**: Vision-centric 4D occupancy forecasting and planning via action-conditioned world modeling. [[paper]](https://doi.org/10.1609/aaai.v39i9.33010) [[code]](https://github.com/yuyang-cloud/Drive-OccWorld)
- **GAIA-1**: Autoregressive image-token prediction for generative driving world modeling. [[paper]](https://arxiv.org/abs/2309.17080)
- **DriveDreamer**: Real-world-driven driving video generation and world modeling. [[paper]](https://arxiv.org/abs/2309.09777) [[code]](https://github.com/JeffWang987/DriveDreamer)
- **Drive-WM**: Multiview visual forecasting and planning with a driving world model. [[paper]](https://arxiv.org/abs/2311.17918) [[code]](https://github.com/BraveGroup/Drive-WM)

### Trajectory-Map Pretraining

- **Forecast-MAE**: Masked autoencoding over agent trajectories and lane segments for motion forecasting. [[paper]](https://doi.org/10.1109/ICCV51070.2023.00797) [[code]](https://github.com/jchengai/forecast-mae)
- **Plan-MAE**: Self-supervised pretraining for integrated prediction and planning with trajectory, map, route, and local sub-planning signals. [[paper]](https://arxiv.org/abs/2507.09537)

### JEPA-Style Latent Prediction

- **AD-L-JEPA**: Joint-embedding predictive architecture for automotive LiDAR object detection with BEV embedding prediction. [[paper]](https://arxiv.org/abs/2501.04969) [[code]](https://github.com/HaoranZhuExplorer/AD-L-JEPA-Release)
- **AD-LiST-JEPA**: Spatiotemporal LiDAR JEPA-style world model for occupancy completion and forecasting. [[paper]](https://arxiv.org/abs/2602.12540)
