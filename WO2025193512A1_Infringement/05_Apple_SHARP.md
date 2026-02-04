# Apple — SHARP
## Potential Infringement of WO/2025/193512A1

**Company:** Apple Inc.
**Product:** SHARP (Sharp Monocular View Synthesis)
**Status:** Open-source research model (Dec 2025), potential Vision Pro integration

---

## How It Works

SHARP takes a single photograph and, in a single forward pass through a neural network (<1 second), regresses parameters for a 3D Gaussian representation. Uses Apple's Depth Pro for depth estimation.

**Pipeline:**
1. Input: Single photograph
2. Single feedforward neural network pass
3. Predicts position and appearance of 3D Gaussians
4. Outputs metric-scale 3D Gaussian splat (.ply)
5. Real-time rendering at 100+ FPS for nearby views

Already integrated into Splat Studio app for Vision Pro. Apple commercialized related tech as "Spatial Scenes" in iOS 26.

---

## Claim Mapping

| Element | Evidence |
|---------|----------|
| (a) Obtaining 2D image | Single photograph input |
| (b) Classifying object | Zero-shot generalization across datasets — implicit classification |
| (c) Segmenting object | Depth estimation isolates scene elements |
| (d) Dimensional sampling | Depth Pro estimates dimensions, Gaussian positions predicted |
| (e) Extracting texture | Appearance parameters of Gaussians encode texture |
| (f) Generating 3D model | 3D Gaussian splat representation (not traditional mesh) |
| (g) Rendering texture onto model | Photorealistic rendering of textured 3D scene |
| Claim 5 (neural network) | Single feedforward neural network pass |
| Claim 9 (multiple views) | Renders nearby novel views |

---

## Evidence Sources

- https://github.com/apple/ml-sharp
- https://apple.github.io/ml-sharp/
- https://machinelearning.apple.com/research/sharp-monocular-view
- https://huggingface.co/apple/Sharp

## Strength: MEDIUM

Strong match on most elements. Weakness: SHARP outputs Gaussian splats, not a traditional "mesh" — a potential design-around argument for claim element (f). However, the functional result (3D representation with texture) is equivalent. If Apple integrates this into Vision Pro / iOS commercially, enforcement value increases significantly.
