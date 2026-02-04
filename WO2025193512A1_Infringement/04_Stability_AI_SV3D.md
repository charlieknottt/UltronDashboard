# Stability AI — SV3D (Stable Video 3D)
## Potential Infringement of WO/2025/193512A1

**Company:** Stability AI
**Product:** SV3D (Stable Video 3D), Stable Fast 3D
**Status:** Released, open-source + commercial license, published at ECCV 2024

---

## How It Works

SV3D is a latent video diffusion model that takes a single object image as input, generates multi-view orbital video frames, then optimizes a 3D mesh from those views.

**Pipeline:**
1. Input: Single image (background removed and centered)
2. Multi-view generation: 21 frames at 576x576 via video diffusion model
3. 3D optimization: NeRF and mesh representations optimized from novel views
4. Output: Textured 3D mesh

Two variants: SV3D_u (unconditional orbits) and SV3D_p (specified camera paths).

Trained on renders from the Objaverse dataset.

---

## Claim Mapping

| Element | Evidence |
|---------|----------|
| (a) Obtaining 2D image | Single image input |
| (b) Classifying object | Trained on Objaverse object categories — classification inherent |
| (c) Segmenting object | Input requires "background removed and centered" — explicit segmentation |
| (d) Dimensional sampling | Camera pose estimation and 3D prior extraction |
| (e) Extracting texture | Texture captured through multi-view diffusion |
| (f) Generating 3D mesh | NeRF → mesh optimization pipeline |
| (g) Rendering texture onto mesh | Textured mesh output |
| Claim 5 (neural network) | Latent video diffusion neural network |
| Claim 9 (multiple views) | 21-frame orbital video, arbitrary camera paths |
| Claim 11 (capture 2D of views) | Each frame is a 2D capture of a novel view |

---

## Evidence Sources

- https://stability.ai/news/introducing-stable-video-3d
- https://sv3d.github.io/
- https://huggingface.co/stabilityai/sv3d
- ECCV 2024 paper (Voleti et al.)

## Strength: HIGH

Extremely well-documented pipeline. The academic paper and open-source code provide detailed evidence of every step. The explicit segmentation requirement (background removal) and neural network mesh generation are directly mappable to claims.
