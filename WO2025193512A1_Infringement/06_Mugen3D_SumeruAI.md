# Mugen3D (SumeruAI)
## Potential Infringement of WO/2025/193512A1

**Company:** SumeruAI (Shenzhen, China)
**Product:** Mugen3D
**Status:** Launched January 2026, angel-funded (10M yuan round)

---

## How It Works

Mugen3D takes a single photograph of any object (human, animal, product) and generates a high-fidelity 3D Gaussian Splatting model. Uses a geometric backbone based on camera geometry, projection principles, and multi-view consistency.

**Pipeline:**
1. Input: Single 2D photograph
2. Geometric backbone processes camera geometry and projection
3. Generative AI + geometric algorithm produces 3D Gaussian Splat
4. 1:1 detail correspondence maintained with source image
5. Output: 3D model across characters, assets, environments
6. Supports watertight geometry for 3D printing

Trained on images and videos (not curated 3D asset libraries). Costs ~1/1000th of comparable systems.

---

## Claim Mapping

| Element | Evidence |
|---------|----------|
| (a) Obtaining 2D image | Single photograph input |
| (b) Classifying object | Handles humans, animals, objects — multi-class understanding |
| (c) Segmenting object | Object isolated from background for 3D generation |
| (d) Dimensional sampling | Geometric backbone with camera geometry and projection |
| (e) Extracting texture | 1:1 detail correspondence preserves texture |
| (f) Generating 3D model | 3DGS model with watertight geometry option |
| (g) Rendering texture onto model | Textured 3D output with "movie-level visual fidelity" |
| Claim 5 (neural network) | Generative AI neural network |
| Claim 9 (multiple views) | 3D model viewable from all angles |

---

## Evidence Sources

- https://sumeruai.us/mugen3d
- https://finance.yahoo.com/news/mugen3d-launch-marks-tipping-point-170000729.html

## Strength: MEDIUM-HIGH

Strong technical match. Same Gaussian splat vs. mesh nuance as Apple SHARP. Jurisdictional complexity — company is China-based, which complicates enforcement. However, if they operate in US markets, US patent still applies.
