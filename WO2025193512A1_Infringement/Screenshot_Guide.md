# Screenshot Guide for WO/2025/193512A1 Evidence of Use

For each source URL, this guide tells you exactly what to screenshot and where to find it on the page.

---

## GOOGLE SHOPPING

### Source 1: Google Research Blog
**URL:** https://research.google/blog/bringing-3d-shoppable-products-online-with-generative-ai/

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "obtaining a 2D image" | Text stating "as few as three images" or "single image" input | Early section describing input requirements, around paragraph 3-4 |
| "segmenting the object" | Text mentioning "removing unwanted backgrounds" | Section on preprocessing challenges, search Ctrl+F for "background" |
| "dimensionally sampling" | Pipeline diagram showing "3D priors" and "camera position estimation" | Gen 1 section, look for the technical pipeline figure |
| "generating a 3D mesh" | Diagram showing NeRF/mesh generation pipeline | Gen 1, 2, or 3 pipeline diagrams (there are multiple) |
| "trained neural network" | Any mention of "Veo," "NeRF," "diffusion model" | Throughout, but especially Gen 3 section describing Veo |
| "extracting texture" | Quote: "complex interactions between light, material, texture, and geometry" | Section describing Veo's capabilities, search for "texture" |
| "rendering texture onto 3D" | Example 360° product spin images/GIFs | Visual examples throughout the blog, especially shoes/furniture |

### Source 2: Google Merchant Center - Product Categories
**URL:** https://support.google.com/merchants/answer/6324436

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "classifying the object" | Product category taxonomy / category selection requirements | Main content showing Google's product category structure |

### Source 3: Google Merchant Center - 3D Models
**URL:** https://support.google.com/merchants/answer/13671720

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "multiple views / user input" | Description of interactive 3D viewer features | Section describing what customers can do with 3D views |
| "rendering texture onto 3D" | Description of 3D spins / 360° views | Section on "AI-generated spins" |

---

## MESHY AI

### Source 1: Meshy Homepage
**URL:** https://www.meshy.ai/

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "obtaining a 2D image" | Upload interface showing single image input | Hero section or "Try it" area showing image upload |
| "generating a 3D mesh" | Export format options (FBX, GLB, OBJ, STL, etc.) | Features section or export/download area |
| "dimensionally sampling" | Smart Remesh feature showing polygon count options (1k-300k) | Features section, search for "Remesh" |
| "multiple views / user input" | 3D viewer with rotation controls | Interactive demo or viewer interface |

### Source 2: Meshy Image-to-3D Feature Page
**URL:** https://www.meshy.ai/features/image-to-3d

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "obtaining a 2D image" | Feature description showing single image workflow | Main feature description |
| "classifying the object" | Examples of different object types being processed | Gallery or examples section |
| "segmenting the object" | Before/after showing input image vs. clean 3D output | Example outputs with no background |

### Source 3: Meshy AI Texturing Feature
**URL:** https://www.meshy.ai/features/ai-texturing

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "extracting texture" | PBR texture maps (Diffuse, Roughness, Metallic, Normal) | Feature description or texture output examples |
| "rendering texture onto 3D" | Textured 3D model examples | Gallery showing textured outputs |
| "primary face / opposite sides" | Model showing front texture applied to back | Examples or documentation about texture inference |

---

## APPLE SHARP

### Source 1: Apple ML-SHARP GitHub
**URL:** https://github.com/apple/ml-sharp

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "obtaining a 2D image" | README showing CLI command: `sharp predict -i image_path.png` | README.md, early section on usage |
| "trained neural network" | Description of single forward pass through neural network | README.md, technical description section |
| "generating a 3D model" | Output format description (.ply Gaussian splat) | README.md, output section |

### Source 2: Apple Machine Learning Research Page
**URL:** https://machinelearning.apple.com/research/sharp-monocular-view

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "obtaining a 2D image" | Quote: "Given a single photograph" | Abstract or introduction |
| "dimensionally sampling" | Description of metric-scale 3D Gaussian positions | Technical description section |
| "extracting texture" | Description of spherical harmonic appearance coefficients | Method section |
| "rendering texture onto 3D" | Performance stats: "100+ FPS," "photorealistic" | Results section |

### Source 3: Apple SHARP Project Page
**URL:** https://apple.github.io/ml-sharp/

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "multiple views" | Demo videos/images showing novel view synthesis | Visual examples on page |
| "rendering texture onto 3D" | Comparison images showing input vs. rendered output | Results gallery |

### Source 4: Hugging Face Paper
**URL:** https://huggingface.co/papers/2512.10685

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "trained neural network" | Paper abstract describing neural network approach | Abstract section |
| "dimensionally sampling" | Figures showing 3D Gaussian prediction | Paper figures |

### Source 5: UploadVR Article on Splat Studio
**URL:** https://www.uploadvr.com/apple-sharp-open-source-on-device-gaussian-splatting/

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "user input manipulation" | Description of Splat Studio on Vision Pro | Article body describing the app |
| "Commercial deployment" | Mention of Spatial Scenes in iOS 26 | Any mention of iOS integration |

---

## AMAZON

### Source 1: Amazon Seller 3D/AR Tools
**URL:** https://sell.amazon.com/tools/3d-ar

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "obtaining a 2D image" | Description of Seller App scanning / photo requirements | "Create 3D Models" section |
| "classifying the object" | Category eligibility text: "Eligibility depends on product category" | Eligibility section |
| "generating a 3D mesh" | GLB/GLTF format requirements | Technical requirements section |
| "multiple views / user input" | Description of View in 3D, View in Your Room, Virtual Try-On | Customer experience section |
| "extracting/rendering texture" | Photorealistic product examples | Visual examples on page |
| Conversion stats | "2X purchase conversion," "20% lower returns" | Business impact / stats section |

### Source 2: AWS 3D Gaussian Splatting Blog
**URL:** https://aws.amazon.com/blogs/spatial/3d-gaussian-splatting-performant-3d-scene-reconstruction-at-scale/

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "segmenting the object" | Quote: "image segmentation and semantic labelling" | Search Ctrl+F for "segmentation" — in pipeline description |
| "trained neural network" | Description of ML/AI services (SageMaker, Bedrock) | Section on AI integration |

### Source 3: AWS Human Mesh Recovery Blog
**URL:** https://aws.amazon.com/blogs/spatial/from-2d-to-3d-building-a-scalable-human-mesh-recovery-pipeline-with-amazon-sagemaker-ai/

| Claim Element | What to Screenshot | Where on Page |
|---------------|-------------------|---------------|
| "dimensionally sampling" | Description of ScoreHMR extracting body parameters from images | Technical pipeline section |
| "trained neural network" | ScoreHMR as diffusion-based neural network | Model description section |
| "generating a 3D mesh" | "Human Mesh Recovery" output description | Results/output section |

---

## SCREENSHOT BEST PRACTICES

1. **Include the URL** in the browser address bar in every screenshot
2. **Include the date** — either visible on screen or annotate the screenshot with capture date
3. **Highlight the key text** — use a red box or yellow highlight to draw attention to the infringing language
4. **Capture full context** — include surrounding paragraphs so the quote isn't taken out of context
5. **Save originals** — keep unedited screenshots as well as annotated versions
6. **Use PDF print** — for important pages, also save as PDF via browser print function as backup
7. **Archive pages** — consider using archive.org Wayback Machine to preserve the page state

---

## PRIORITY SCREENSHOTS (Most Important)

### Google (3 critical screenshots):
1. Research blog: "removing unwanted backgrounds" quote
2. Research blog: "texture" quote in Veo description
3. Research blog: Pipeline diagram for any generation

### Meshy (3 critical screenshots):
1. Export formats showing FBX, GLB, OBJ, STL
2. PBR texture output (Diffuse, Roughness, Metallic, Normal)
3. Smart Remesh polygon count slider

### Apple (3 critical screenshots):
1. GitHub README with CLI command
2. Research page: "single photograph" quote
3. Output format showing .ply Gaussian splat (NOTE: flag this as claim construction issue)

### Amazon (3 critical screenshots):
1. AWS blog: "image segmentation and semantic labelling" quote
2. Seller page: GLB/GLTF format requirement
3. Seller page: "Eligibility depends on product category"
