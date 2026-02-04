# Google Shopping — 3D Product Viewer
## Potential Infringement of WO/2025/193512A1

**Company:** Google (Alphabet)
**Product:** Google Shopping 3D Product Visualizations
**Status:** Deployed at scale across shoes, furniture, electronics, apparel

---

## How It Works

Google generates interactive 360° product spins from as few as 1-3 product images. Their latest (Gen 3) pipeline uses the Veo video generation model fine-tuned on millions of 3D synthetic assets to produce 360° spin videos conditioned on input images.

**Pipeline:**
1. Input: 1-3 product photos
2. Background removal / segmentation
3. 3D representation generation via Veo (captures light, material, texture, geometry)
4. Output: Interactive 360° spins viewable on Google Shopping

Earlier generations used NeRF (Gen 1) and Score Distillation Sampling with diffusion models (Gen 2).

---

## Claim Mapping

| Element | Evidence |
|---------|----------|
| (a) Obtaining 2D image | Accepts as few as 1 product image |
| (b) Classifying object | Generalizes across product categories (shoes, furniture, electronics) — implies classification |
| (c) Segmenting object | Blog confirms "removing unwanted backgrounds" |
| (d) Dimensional sampling | 3D priors predicted, camera positions estimated from sparse images |
| (e) Extracting texture | Veo captures "complex interactions between light, material, texture, and geometry" |
| (f) Generating 3D mesh | Generates 3D representations (NeRF/mesh via optimization) |
| (g) Rendering texture onto mesh | Produces photorealistic textured 3D views |
| Claim 9 (multiple views) | 360° interactive spins |
| Claim 10 (user input) | Users rotate/interact with product on Google Shopping |
| Claim 11 (capture 2D of each view) | Novel view frames captured from 360° video |

---

## Evidence Sources

- https://research.google/blog/bringing-3d-shoppable-products-online-with-generative-ai/
- https://support.google.com/merchants/answer/13671720
- https://support.google.com/merchants/answer/13675100

## Strength: HIGH

Google's own research blog documents nearly every claim element. The pipeline clearly takes a small number of 2D images, processes them through neural networks, generates a 3D representation with texture, and outputs multiple viewpoints. The grocery-specific claims (3-4) could also apply if Google extends to grocery product categories.
