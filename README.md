# DeepLense — GSoC 2026 | ML4Sci Submission 

**Candidate:** Sarthak Jagota

**GitHub:** https://github.com/SarthakJagota

**Email:** sarthakjagota34@gmail.com

---

## Tasks Completed

| Task | Description | Key Result |
|------|-------------|------------|
| Common Test I | Multi-class lensing classification (ResNet50) | Acc: 82.30% · AUC: 0.9452 |
| Specific Test VII | EfficientNet-B3 + Physics-Informed Neural Network | Acc: 86.67% · AUC: 0.9702 |
| Specific Test IX(A) | MAE Self-supervised Pre-training + Fine-tuning (ViT) | Acc: 89.95% · AUC: 0.96–0.99 |
| Specific Test IX(B) | Super-Resolution via SRResNet (fine-tuned) | SSIM: 0.9750 · PSNR: 41.55 dB |

All models trained and evaluated on a **90:10 train-test split**.

---

## Common Test I — ResNet50 Classifier

- Architecture: ResNet50 with partial fine-tuning (layer3, layer4, custom FC head)
- Differential learning rates: layer3 → 1e-4, layer4 → 5e-4, FC → 1e-3
- Augmentation: random flips, rotation, affine, color jitter
- Classes: `no_substructure`, `sphere`, `vortex`

**Per-class AUC:** no: 0.9595 · sphere: 0.9172 · vort: 0.9590

---

## Specific Test VII — EfficientNet-B3 + PINN

- Backbone: EfficientNet-B3 (pretrained ImageNet)
- Physics branch predicts Einstein radius θ_E per image using SIS lensing model
- Combined loss: CrossEntropy + λ·Physics loss (λ=0.3) with margin constraint
- Learned θ_E separation at convergence: no_sub=0.323 · subhalo=0.589 · vortex=0.836

The physics constraint acts as a physically motivated regularizer, guiding the network
to learn features consistent with the SIS gravitational lensing equation.

---

## Specific Test IX(A) — MAE Pre-training + Classification

- Phase 1: Masked Autoencoder pre-trained on `no_sub` images only (no labels)
  - ViT encoder: 6 layers, embed_dim=256, 8 heads, 75% masking ratio
  - 100 epochs, AdamW, CosineAnnealing · Final loss: 0.000013
- Phase 2: Encoder fine-tuned for 3-class classification (axion / cdm / no_sub)
  - 89,104 total images across 3 classes

**Per-class AUC:** axion: 0.9727 · cdm: 0.9600 · no_sub: 0.9968

---

## Specific Test IX(B) — Super-Resolution

- Architecture: SRResNet (8 residual blocks, PixelShuffle ×2 upsampling)
- Input: 75×75 LR → Output: 150×150 SR
- Two-stage: trained from scratch (VI.A baseline) then fine-tuned (IX.B)
- Fine-tuning freezes first 4 residual blocks, trains remaining layers at lr=1e-5

| Model | MSE | SSIM | PSNR |
|-------|-----|------|------|
| Trained from scratch | 0.000076 | 0.9731 | 41.27 dB |
| Fine-tuned (IX.B) | 0.000071 | 0.9750 | 41.55 dB |

---

## Environment

- Platform: Google Colab
- GPU: NVIDIA Tesla T4
- Python: 3.12
- PyTorch: 2.10.0+cu128

---

## Notes

- All notebooks are self-contained and reproducible end-to-end.
- Model weights saved to Google Drive during training and available on request.
- Datasets provided by ML4Sci / DeepLense mentors.
- Dataset loading assumes the original directory structure provided by mentors.
