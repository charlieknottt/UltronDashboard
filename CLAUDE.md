# UltronAI Patent Portfolio Network Analysis

## Project Overview
Cross-reference LinkedIn connections from team members against target tech companies to identify strategic contacts for patent/IP discussions, M&A/Corp Dev, or Product/Engineering roles.

## Target Roles (Priority Order)
1. **IP/Legal**: Patent, intellectual property, licensing, legal, counsel, attorney, compliance, regulatory
2. **M&A/Corp Dev**: M&A, mergers, acquisition, corp dev, corporate development, business development, strategic partner, ventures, investment, strategy
3. **Product/Engineering**: Engineer, developer, architect, scientist, research, product, software, hardware, data, AI, machine learning, cloud, platform, infrastructure, security, UX/UI, CTO

## Target Seniority Levels
- **Executive (6)**: CEO, CTO, CFO, COO, CPO, Chief, President, Founder
- **VP (5)**: VP, Vice President, SVP, EVP
- **Director (4)**: Director
- **Head/GM (3)**: Head of, General Manager
- **Senior (2)**: Senior, Sr.
- **Staff/Principal (1)**: Staff, Principal, Lead, Manager

## Target Companies (11)
- NVIDIA
- Google (includes Alphabet, DeepMind, YouTube, Waymo, Nest)
- Apple (exclude Applebee's, Apple Bank, Apple Federal, etc.)
- Microsoft (includes LinkedIn, GitHub)
- Amazon (includes AWS, Whole Foods, Twitch, Zappos) - NOTE: Do NOT include Audible
- Meta (includes Facebook, Instagram, WhatsApp, Oculus, Reality Labs) - NOTE: exclude Metamask, Metadata, etc.
- Tesla (exclude "Nikola Tesla" references)
- xAI (STRICT: only exact "xAI" or "x.ai" - exclude "Alex AI", "GrowthX AI", etc.)
- Samsung
- OpenAI
- Qualcomm
- SoftBank/ARM (ARM must be "ARM Holdings", "ARM Ltd", etc. - exclude farms, army, pharma, etc.)

## Team Members (7 CSV files)
- CK (Connections - CK.csv)
- Hadi (Connections - Hadi.csv)
- KP (Connections - KP.csv)
- MGF (Connections - MGF.csv)
- MikeR (Connections - MikeR.csv)
- SDR (Connections - SDR.csv)
- DW (Connections - DW.csv)

## CSV Format
- Skip first 3 rows (LinkedIn export notes)
- Columns: First Name, Last Name, URL, Email Address, Company, Position, Connected On

## Exclusion Rules
### Position-based exclusions (NOT current FTEs):
- Former/ex-employees: "former", "ex-", "previously", "retired", "past", "was", "left", "departed", "alumni"
- Contractors: "contractor", "contract", "freelance", "consultant", "via ", "magnit"
- Temporary: "temp", "temporary", "part-time"
- Interns/Students: "intern", "internship", "incoming", "student", "graduate", "fellow"
- Job seekers: "seeking", "looking for", "open to"

### Specific people excluded:
- Chester Bedell (Public Policy - not relevant)
- Luis Bitencourt (ex-Microsoft)

### Company matching edge cases FIXED:
- "ring" must NOT match "engineering", "manufacturing", "catering" - use strict pattern: `^ring$|^ring\s|ring\.com|ring doorbell|ring llc`
- "arm" must NOT match "farms", "army", "pharma", "armor", "karma", "carmax", etc.
- "meta" must NOT match "metamask", "metadata", "metabolic", "metaverse"
- "xai" must be EXACT - not part of other company names

## Output Files Created

### HTML Dashboards
1. **ultronai_network.html** - Full network (~411 contacts)
   - Overview tab with top 5 strategic contacts per company
   - Browse All tab with filters (Search, Company, Via, Role Type, Seniority)
   - Top 5 prioritized by: IP/Legal > M&A/Corp Dev > Product/Engineering > Other

2. **ultronai_max_impact.html** - Director+ level only (~98 contacts)
   - Same layout as network
   - Only seniority >= 4 (Director, VP, Executive)

3. **ultronai_max_impact_full.html** - All Staff+ level (~298 contacts)
   - Seniority >= 1

### Excel Files
1. **UltronAI_Network_Complete.xlsx** - Single file with all data
   - Overview sheet: Dashboard with bar chart (contacts by company), pie chart (seniority), stats
   - Max Impact sheet: Director+ contacts with clickable LinkedIn links
   - All Contacts sheet: Full list with filters
   - Per-company sheets: Amazon, Apple, Google, Meta, Microsoft, NVIDIA, OpenAI, Qualcomm, Samsung, Tesla, xAI

2. **ultronai_network.xlsx** - Simple export of all contacts
3. **ultronai_max_impact.xlsx** - Simple export of Director+ contacts

## Key Statistics (as of last run)
- Total contacts: ~411
- Max Impact (Director+): ~98
- Companies represented: 11
- Team members: 7

### By Company:
- Google: ~122
- Apple: ~77
- Amazon: ~72
- Meta: ~58
- Microsoft: ~33
- NVIDIA: ~18
- OpenAI: ~15
- Samsung: ~7
- Tesla: ~5
- Qualcomm: ~3
- xAI: ~1

### By Role:
- Product/Engineering: ~226
- Other: ~165
- M&A/Corp Dev: ~18
- IP/Legal: ~5

## Python Processing Notes
- Use pandas with `skiprows=3` for LinkedIn CSVs
- Use `re.search(r'\bword\b', text)` for word boundary matching
- Deduplicate by LinkedIn URL, keeping highest seniority version
- Sort top 5 by role_priority first, then seniority descending

## Future Updates
When adding new team member CSVs:
1. Add filename to team list
2. Re-run the Python processing script
3. Regenerate HTML and Excel files
4. Verify no new false positives in company matching

---

# WO/2025/193512A1 Infringement Analysis Project

## Patent Overview
- **Patent:** WO/2025/193512A1
- **Title:** SINGLE SHOT 3D MODELLING FROM 2D IMAGE
- **Assignee:** Carnegie Mellon University
- **Inventor:** Marios Savvides et al.
- **Status:** International (WIPO) Application

## Claim 1 (Independent) — Key Elements
1. Obtaining a 2D image of an object
2. Classifying the object in the image
3. Segmenting the object from the image
4. Dimensionally sampling the segmented image of the object
5. Extracting texture information from the segmented image
6. Generating a 3D mesh model based on the dimensional sampling
7. Rendering the texture information onto the 3D mesh model

## Key Dependent Claims
- **Claim 5:** 3D mesh generated by trained neural network
- **Claim 7:** Texture represents primary face of object
- **Claim 8:** Primary face texture rendered on opposite sides
- **Claim 9:** Manipulating 3D to provide multiple views
- **Claim 10:** Manipulation based on user input
- **Claim 11:** Capturing 2D image of each manipulation

## Infringement Targets (4 Active)

### 1. Google Shopping (HIGH confidence)
- **Product:** Google Shopping 3D Product Viewer
- **Key Evidence:** Google Research Blog documents entire pipeline
- **Critical URL:** https://research.google/blog/bringing-3d-shoppable-products-online-with-generative-ai/
- **Strongest elements:** "removing unwanted backgrounds" (segmentation), "texture" explicitly named, Veo neural network

### 2. Meshy AI (HIGH confidence)
- **Product:** Meshy AI Image-to-3D Generator
- **Key Evidence:** Explicit mesh output (FBX, GLB, OBJ, STL), PBR textures
- **Critical URL:** https://www.meshy.ai/
- **Strongest elements:** Unambiguous mesh formats, Smart Remesh (1k-300k triangles), full PBR pipeline

### 3. Apple SHARP (MEDIUM-HIGH confidence)
- **Product:** SHARP + Spatial Scenes (iOS 26) + Vision Pro
- **Key Evidence:** Open-source on GitHub, Apple ML Research page
- **Critical URLs:** https://github.com/apple/ml-sharp, https://machinelearning.apple.com/research/sharp-monocular-view
- **CLAIM CONSTRUCTION ISSUE:** Outputs Gaussian splats (.ply), NOT polygon mesh. Element (f) "generating a 3D mesh model" is vulnerable.
- **Note:** Gaussian splats ≠ mesh (no vertices/faces/edges). Functional equivalence argument available but not certain.

### 4. Amazon (HIGH confidence)
- **Product:** Amazon 3D/AR (Seller App + View in 3D + AWS Pipeline)
- **Key Evidence:** AWS blog documents "image segmentation," GLB/GLTF mandate
- **Critical URLs:** https://sell.amazon.com/tools/3d-ar, https://aws.amazon.com/blogs/spatial/3d-gaussian-splatting-performant-3d-scene-reconstruction-at-scale/
- **Strongest elements:** AWS explicitly says "image segmentation and semantic labelling," GLB/GLTF are mesh formats by definition

## Output Files Created (in WO2025193512A1_Infringement/)

### Evidence of Use PowerPoints
- `EoU_Google_Shopping.pptx` — 4 slides
- `EoU_Meshy_AI.pptx` — 5 slides
- `EoU_Apple_SHARP.pptx` — 4 slides
- `EoU_Amazon.pptx` — 4 slides

### Supporting Documents
- `Screenshot_Guide.md` — Detailed instructions for what to screenshot from each URL
- `00_Patent_Summary.md` — Claim elements reference
- `01_Google_Shopping.md` through `09_Canva.md` — Initial target analysis files

### Python Scripts
- `build_eou_v6.py` — Current version generating clean EoU PowerPoints

## Key Technical Distinctions

### Mesh vs. Gaussian Splats
- **Mesh:** Vertices, edges, faces (polygons). Formats: OBJ, FBX, GLB, STL, GLTF
- **Gaussian Splats:** Point-based, millions of 3D Gaussian ellipsoids with position, covariance, opacity, color. Format: .ply
- **Patent says "3D mesh model"** — Apple SHARP outputs Gaussians, creating claim construction risk

### EoU Format (from Experian exemplar)
Each slide maps:
1. Exact claim language (quoted)
2. Product evidence showing that element
3. Source URLs for screenshots
4. Commentary on strength/risks

## Next Steps
1. Capture screenshots per Screenshot_Guide.md
2. Insert screenshots into EoU PowerPoints
3. Review Apple claim construction issue with patent counsel
4. Consider additional targets: Stability AI SV3D, Hexa, Nextech3D.ai, Canva

## Related Patents in Portfolio (same inventor/assignee)
- **US 8,861,800 B2** — Rapid 3D face reconstruction from 2D image (ISSUED)
- **US 10,755,145 B2** — 3D Spatial Transformer Network (ISSUED, face-specific)
- **US 9,916,685 B1** — Depth recovery of face from image (ISSUED)
