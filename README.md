# Project 3 · Mapping Floodwaters with Deep Learning

This project demonstrates a rapid-response workflow for delineating flood extent from multi-temporal Sentinel-2 imagery using a U-Net segmentation model. All data are synthetically generated so the notebook can run end-to-end without external downloads.

## Contents
- `mapping_floodwaters.ipynb` – fully executable research narrative covering data simulation, model training, evaluation, and interpretation.

## Synthetic dataset
Each sample in the notebook pairs a pre-flood RGB chip with a post-flood chip and a binary mask that represents inundated pixels.
- Base scenes blend smooth river geometry with localized wetlands.
- Flooded areas are expanded via procedural noise plus intensity shifts mimicking water spectral signatures (lower red/green reflectance, higher blue).
- Random flips, rotations, and brightness/contrast jitter augment the training split for robustness.

## Model architecture
- **Backbone**: Custom U-Net with four encoder/decoder stages (32→256 channels) and skip connections to preserve shoreline detail.
- **Input channels**: Pre- and post-flood RGB stacks concatenated (6 channels total).
- **Loss**: 50/50 Binary Cross-Entropy + Dice to balance pixel-wise accuracy with overlap on thin river structures.

## Training loop
The notebook trains for 5 epochs on 200 synthetic tiles using Adam (lr=1e-3, batch size=8). Loss curves are logged and plotted to watch convergence. Validation samples are visualized to compare predictions and ground truth.

## Usage
1. Open `mapping_floodwaters.ipynb` in VS Code or Jupyter.
2. Run cells sequentially. Training takes ~3–4 minutes on CPU.
3. Review loss curves and qualitative panels to interpret performance.

## Next steps
- Incorporate additional spectral bands (e.g., NIR, SWIR) or Sentinel-1 SAR for cloud-robust mapping.
- Fine-tune on a small labeled real-world dataset to bridge the synthetic-to-real domain gap.
- Add uncertainty quantification (MC Dropout) and active learning hooks for field deployment.
