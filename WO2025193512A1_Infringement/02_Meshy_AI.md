# Meshy AI
## Potential Infringement of WO/2025/193512A1

**Company:** Meshy Inc.
**Product:** Meshy AI 3D Model Generator
**Status:** Commercial SaaS product, 1M+ users

---

## How It Works

Meshy accepts a single image upload, generates multi-view images (front, side, back), then converts these into a textured 3D mesh. Exports in FBX, GLB, OBJ, STL, 3MF, USDZ, BLEND.

**Pipeline:**
1. Input: Single image or text prompt
2. AI generates front/side/back views (implies classification + segmentation)
3. 3D mesh generation with geometry and textures
4. PBR textures applied (Diffuse, Roughness, Metallic, Normal maps)
5. Browser-based 3D viewer for multi-angle inspection
6. Smart Remesh for mesh optimization (1k-300k triangles)

---

## Claim Mapping

| Element | Evidence |
|---------|----------|
| (a) Obtaining 2D image | Single image upload |
| (b) Classifying object | Multi-view generation implies object understanding/classification |
| (c) Segmenting object | Object isolated from background for multi-view generation |
| (d) Dimensional sampling | Geometry extracted, mesh triangle counts adjustable |
| (e) Extracting texture | PBR texture extraction (Diffuse, Roughness, Metallic, Normal) |
| (f) Generating 3D mesh | Explicit mesh generation, multiple export formats |
| (g) Rendering texture onto mesh | Textures rendered onto mesh, multiple style options |
| Claim 5 (neural network) | AI/neural network-based generation |
| Claim 9 (multiple views) | Browser preview from any angle |
| Claim 10 (user input) | User rotates model interactively |

---

## Evidence Sources

- https://www.meshy.ai/
- Product documentation and marketing materials

## Strength: HIGH

Meshy's pipeline is a near-exact match to Claim 1. Single image in, classified/segmented, mesh generated, texture rendered. The explicit PBR texture pipeline and multi-format mesh export directly map to claim elements.
