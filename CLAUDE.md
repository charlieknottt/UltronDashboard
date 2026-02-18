# UltronAI Patent Portfolio Network Analysis

## Project Overview
Cross-reference LinkedIn connections from team members against target tech companies to identify strategic contacts for patent/IP discussions, M&A/Corp Dev, or Product/Engineering roles.

## Target Roles (Priority Order)
1. **IP/Legal** (priority 0): Patent, intellectual property, licensing, legal, counsel, attorney, compliance, regulatory
2. **M&A/Corp Dev** (priority 1): M&A, mergers, acquisition, corp dev, corporate development, business development, strategic partner, ventures, investment, strategy
3. **Product/Engineering** (priority 2): Engineer, developer, architect, scientist, research, product, software, hardware, data, AI, machine learning, cloud, platform, infrastructure, security, UX/UI, CTO
4. **Other** (priority 3): Anything not matching above

### Role Classification Logic
- Roles are checked in priority order: IP/Legal first, then M&A/Corp Dev, then Product/Engineering
- First match wins — a "Patent Counsel" is IP/Legal even though "counsel" could overlap
- "Other" is the default for roles like recruiter, marketing, PR, finance (unless they contain strategy/investment keywords)

### Role Regex Patterns (exact)
```python
IP_LEGAL: r'\b(patent|intellectual\s*property|licensing|legal|counsel|attorney|compliance|regulatory)\b'
MA_CORPDEV: r'\b(m&a|mergers?|acquisition|corp\s*dev|corporate\s*development|business\s*development|strategic\s*partner|ventures?|investment|strategy)\b'
PROD_ENG: r'\b(engineer|developer|architect|scientist|research|product|software|hardware|data|ai\b|artificial\s*intelligence|machine\s*learning|cloud|platform|infrastructure|security|ux|ui\b|cto)\b'
```

## Target Seniority Levels
- **Executive (6)**: CEO, CTO, CFO, COO, CPO, Chief, President, Founder
- **VP (5)**: VP, Vice President, SVP, EVP
- **Director (4)**: Director
- **Head/GM (3)**: Head of, General Manager
- **Senior (2)**: Senior, Sr.
- **Staff/Principal (1)**: Staff, Principal, Lead, Manager
- **Other (0)**: No seniority keywords matched

### Seniority Classification Logic
- Checked top-down (Executive first), first match wins
- "Senior Vice President" matches VP (level 5) before Senior (level 2) because VP is checked first
- "Senior Director" matches Director (level 4) — Director checked before Senior
- "Head of" requires the space after "Head" to avoid matching "Headcount"

### Seniority Regex Patterns (exact)
```python
Executive (6): r'\b(CEO|CTO|CFO|COO|CPO|Chief|President|Founder)\b'
VP (5):        r'\b(VP|Vice\s*President|SVP|EVP)\b'
Director (4):  r'\bDirector\b'
Head/GM (3):   r'\b(Head\s+of|General\s*Manager)\b'
Senior (2):    r'\b(Senior|Sr\.)\b'
Staff/Prin(1): r'\b(Staff|Principal|Lead\b|Manager)\b'
```

## Max Impact Definition
- **Max Impact = Seniority Level >= 3 (Head/GM and above)**
- Includes: Executive, VP, Director, Head/GM
- Excludes: Senior, Staff/Principal, Other

## Target Companies (12)
- **NVIDIA**: `\bnvidia\b`
- **Google**: `\bgoogle\b`, `\balphabet\b`, `\bdeepmind\b`, `\byoutube\b`, `\bwaymo\b`, `\bnest\b`
- **Apple**: `\bapple\b`
- **Microsoft**: `\bmicrosoft\b`, `\blinkedin\b`, `\bgithub\b`
- **Amazon**: `\bamazon\b`, `\baws\b`, `\bwhole\s*foods\b`, `\btwitch\b`, `\bzappos\b`, Ring (strict), `\beero\b`, `\blab\s*126\b` — **NOTE: Do NOT include Audible**
- **Meta**: `\bmeta\b`, `\bfacebook\b`, `\binstagram\b`, `\bwhatsapp\b`, `\boculus\b`, `\breality\s*labs\b`
- **Tesla**: `\btesla\b`
- **xAI**: STRICT exact match only — `^xAI$|^x\.ai$|\bxAI\b|x\.ai`
- **Samsung**: `\bsamsung\b`
- **OpenAI**: `\bopenai\b`
- **Qualcomm**: `\bqualcomm\b` (also match subsidiary "Edge Impulse (a Qualcomm company)")
- **SoftBank/ARM**: `\bsoftbank\b`, `\barm\s+holdings\b`, `\barm\s+ltd\b`, `^arm$`, `\barm\b(?!s|y|o|a|e|chair|strong|ed\b)`

## Team Members (8 CSV files)

| Code | Name | CSV Filename | Total Connections | Matched |
|------|------|-------------|-------------------|---------|
| CK | Charlie | Connections - CK.csv | 2,260 | 14 |
| Hadi | Hadi | Connections - Hadi.csv | 1,918 | 152 |
| KP | KP | Connections - KP.csv | 1,448 | 38 |
| MGF | MGF | Connections - MGF.csv | 1,090 | 12 |
| MikeR | Mike R | Connections - MikeR.csv | 1,818 | 48 |
| SDR | SDR | Connections - SDR.csv | 730 | 37 |
| DW | DW | Connections - DW.csv | 3,541 | 146 |
| MS | Marios | Connections - Marios.csv | 5,334 | 256 |

## CSV Format
- **Skip first 3 rows** (LinkedIn export boilerplate/notes)
- Columns: `First Name`, `Last Name`, `URL`, `Email Address`, `Company`, `Position`, `Connected On`
- Use `pd.read_csv(filepath, skiprows=3)`
- Handle NaN values: check `pd.notna()` before converting to string

## Exclusion Rules

### Position-based exclusions (NOT current FTEs)
These are matched against the **Position** field using regex with word boundaries:

```python
POSITION_EXCLUDE = re.compile(
    r'\b(former|ex-|previously|retired|past\b|was\b|left\b|departed|alumni'
    r'|contractor|contract\b|freelance|consultant|via\s|magnit'
    r'|temp\b|temporary|part-time'
    r'|intern\b|internship|incoming|student|graduate\b|fellow\b'
    r'|seeking|looking\s+for|open\s+to'
    r'|visiting\b|independent\s+creator|^mentor$)\b', re.I
)
```

**Categories:**
- **Former/ex-employees**: "former", "ex-", "previously", "retired", "past", "was", "left", "departed", "alumni"
- **Contractors**: "contractor", "contract", "freelance", "consultant", "via " (staffing agency), "magnit" (staffing platform)
- **Temporary**: "temp", "temporary", "part-time"
- **Interns/Students**: "intern", "internship", "incoming", "student", "graduate", "fellow"
- **Job seekers**: "seeking", "looking for", "open to"
- **Non-FTE affiliations**: "visiting" (visiting researcher), "independent creator" (content creators), "mentor" (exact match only)

### Specific people excluded
```python
EXCLUDED_PEOPLE = [
    ("chester", "bedell"),    # Public Policy - not relevant to patent/IP
    ("luis", "bitencourt"),   # ex-Microsoft
    ("jess", "boddy"),        # Twitch "Partner" = content creator, not employee
    ("claudia", "romeo"),     # YouTube "Independent Creator" - not employee
    ("genia", "xasis"),       # Google "Mentor" - not FTE
    ("serena", "dayal"),      # Primary employer is Athena Capital, not SoftBank
]
```

### Non-FTE roles that PASS the filter (confirmed valid)
These look suspicious but are legitimate employees:
- **"Partner" in a title like "Partner Engineering Management"** — this is an employee role, not a business partner
- **"General Manager | Director (L8) | Head of..."** — Amazon level notation, legitimate employee
- **Twitch "Partner"** — this specifically means content creator and IS excluded (Jess Boddy)
- **"Edge Impulse (a Qualcomm company)"** — subsidiary, counts as Qualcomm

## Company Matching — False Positive Exclusion Rules

### Apple exclusions
```python
APPLE_EXCLUDE = re.compile(r"applebee|apple\s*bank|apple\s*federal|apple\s*leisure|apple\s*hospitality|apple\s*auto|apple\s*growth", re.I)
```

### Meta exclusions
```python
META_EXCLUDE = re.compile(r"metamask|metadata|metaboli|metaverse|metagen|metacognit|firma\s*meta|^former\b", re.I)
```
**Known false positives caught**: MetaProp, Metasteps, MetaFloor AI, Metabolic Health Summit, Metalium

### Tesla exclusions
```python
TESLA_EXCLUDE = re.compile(r"nikola\s*tesla", re.I)
```

### ARM exclusions (most complex — "arm" appears in many English words)
```python
ARM_EXCLUDE = re.compile(r"farm|army|pharma|armor|karma|carmax|armada|armani|disarm|firearm|charm|harmon|arm\s*institute|arm\s*candy", re.I)
```
The ARM match pattern itself uses negative lookahead: `\barm\b(?!s|y|o|a|e|chair|strong|ed\b)` to avoid arms, army, armor, armada, armed, armchair, armstrong.

**Valid ARM matches**: "SoftBank", "ARM Holdings", "ARM Ltd", or standalone "ARM"

### Amazon exclusions
```python
AMAZON_EXCLUDE = re.compile(r'\baudible\b|turing\.com|a&r\s+engineering', re.I)
```
- **Audible**: Explicitly excluded per project rules (even though Amazon owns it)
- **Ring**: Uses strict pattern `^ring$|^ring\s|\bring\.com\b|ring doorbell|ring llc` to avoid "engineering", "manufacturing", "catering", "Barrington", "Turing", etc.

### Google exclusions
```python
GOOGLE_EXCLUDE = re.compile(r'google\s*developer\s*group|youtube\s*channel|transdev|^former\b|^the\s+nest$', re.I)
```
- "Google Developer Group" = community group, not Google employee
- "YouTube channel" = content creator
- "The Nest" standalone = not Google Nest

### Microsoft exclusions
```python
MICROSOFT_EXCLUDE = re.compile(r'linkedin\s*group|".*linkedin\s*group', re.I)
```

### xAI matching (strictest)
Pattern: `^xAI$|^x\.ai$|\bxAI\b|x\.ai` — must be exact "xAI" or "x.ai", never part of another name like "Alex AI" or "GrowthX AI"

## Deduplication Logic
- **Key**: LinkedIn URL
- When duplicate found:
  1. **Merge Via fields**: Comma-separated list of all team members who know this person (e.g., "Hadi, DW, MS")
  2. **Keep highest seniority**: If one CSV has them as "Senior Engineer" and another as "Director", keep Director
  3. **Keep email**: If one version has email and other doesn't, preserve the email
- After dedup, sort by: Target Company (alpha) → Role Priority (IP > M&A > Prod/Eng > Other) → Seniority Level (desc) → Full Name (alpha)

## Output Files

### Primary Processing Script
- **`update_network_ms.py`** — Master script that processes ALL 8 CSVs from scratch
  - Contains all regex patterns, exclusion rules, classification logic
  - Outputs `ultronai_network.xlsx` and `ultronai_max_impact.xlsx`
  - Run with: `python update_network_ms.py`

### Excel Files
1. **`UltronAI_Network_Complete.xlsx`** — Comprehensive multi-sheet workbook
   - **Overview** sheet: Title, stats (total/max impact/companies), 4 summary tables (Team, Company, Seniority, Role)
   - **Max Impact (Director+)** sheet: Head/GM+ contacts (seniority >= 3) — columns: Via, Name, Position, Company, Role Type, Seniority, LinkedIn (hyperlinked "Profile" text)
   - **All Contacts** sheet: Full 660 contacts — same columns + Email
   - **12 per-company sheets**: Google, Amazon, Apple, Meta, Microsoft, NVIDIA, OpenAI, Qualcomm, Samsung, Tesla, SoftBank-ARM, xAI — columns: Via, Name, Position, Role Type, Seniority, LinkedIn
   - **Note**: SoftBank/ARM sheet is named "SoftBank-ARM" (slash invalid in Excel sheet names)
   - **Formatting**: Header row 1 = title (Font 16, blue), row 2 = blank, row 3 = column headers (white on dark blue #2F5496), data starts row 4, freeze panes at A4
   - **LinkedIn column**: Display text "Profile" with hyperlink to actual LinkedIn URL, blue underlined font (#0563C1)
   - Generated by inline Python script (no standalone .py file) — rebuild by reading `ultronai_network.xlsx` + `ultronai_max_impact.xlsx`

2. **`ultronai_network.xlsx`** — Flat export of all contacts
   - Columns: Full Name, First Name, Last Name, Target Company, Company (Listed), Position, Role Type, Seniority, Via, LinkedIn URL, Email
   - Header: white on dark blue (#2F5496), freeze panes at A2
   - This is the SOURCE DATA for UltronAI_Network_Complete.xlsx

3. **`ultronai_max_impact.xlsx`** — Flat export of Head/GM+ contacts (seniority >= 3)
   - Same columns as ultronai_network.xlsx
   - Subset: only contacts with Seniority Level >= 3

### HTML Dashboards (generated separately, may be stale)
1. **ultronai_network.html** — Full network
2. **ultronai_max_impact.html** — Director+ level only
3. **ultronai_max_impact_full.html** — All Staff+ level

## Key Statistics (as of 2026-02-07)

### Totals
- **Total unique contacts: 660**
- **Max Impact (Head/GM+): 153**
- **Companies represented: 12**
- **Team members: 8**

### By Company

| Company | Total | Head/GM+ |
|---------|-------|----------|
| Google | 164 | 38 |
| Amazon | 128 | 28 |
| Apple | 103 | 20 |
| Meta | 98 | 23 |
| Microsoft | 62 | 16 |
| NVIDIA | 45 | 9 |
| OpenAI | 17 | 3 |
| Qualcomm | 15 | 4 |
| Samsung | 14 | 9 |
| Tesla | 9 | 0 |
| SoftBank/ARM | 3 | 3 |
| xAI | 2 | 0 |

### By Role

| Role | Count |
|------|-------|
| Product/Engineering | 351 |
| Other | 280 |
| M&A/Corp Dev | 23 |
| IP/Legal | 6 |

### By Seniority

| Level | Label | Count |
|-------|-------|-------|
| 0 | Other | 218 |
| 1 | Staff/Principal | 179 |
| 2 | Senior | 110 |
| 4 | Director | 88 |
| 3 | Head/GM | 30 |
| 6 | Executive | 18 |
| 5 | VP | 17 |

### By Team Member (contacts contributed, including shared)

| Member | Matched Contacts | CSV Total Rows |
|--------|-----------------|----------------|
| MS (Marios) | 256 | 5,334 |
| Hadi | 152 | 1,918 |
| DW | 146 | 3,541 |
| MikeR | 48 | 1,818 |
| KP | 38 | 1,448 |
| SDR | 37 | 730 |
| CK | 14 | 2,260 |
| MGF | 12 | 1,090 |

## Rebuild Instructions

### Step 1: Regenerate flat xlsx files
```bash
cd "/Users/charlieknott/Downloads/Ultron Internship"
python update_network_ms.py
```
This reads all 8 CSVs, applies all filters, deduplicates, and writes:
- `ultronai_network.xlsx` (all 660 contacts)
- `ultronai_max_impact.xlsx` (153 Head/GM+ contacts)

### Step 2: Regenerate UltronAI_Network_Complete.xlsx
Run the inline Python that:
1. Reads `ultronai_network.xlsx` and `ultronai_max_impact.xlsx`
2. Creates Overview sheet with stats tables
3. Creates Max Impact sheet with hyperlinked LinkedIn profiles
4. Creates All Contacts sheet with emails
5. Creates 12 per-company sheets
6. Saves as `UltronAI_Network_Complete.xlsx`

Key formatting details:
- Title font: Bold, size 16, color #2F5496
- Header font: Bold, white (#FFFFFF), size 11
- Header fill: #2F5496 (dark blue)
- Section headers on Overview: white on #4472C4 (medium blue)
- LinkedIn cells: display "Profile", hyperlink to URL, font color #0563C1, underlined
- Sheet name for SoftBank/ARM: use "SoftBank-ARM" (no slashes allowed)
- Freeze panes: A4 on all data sheets (row 3 = headers)
- Column widths: Via=14, Name=24, Position=55, Company=18, Role Type=18, Seniority=14, LinkedIn=12, Email=30

### Step 3: (Optional) Regenerate HTML dashboards
These are generated by separate scripts (not currently maintained). The xlsx files are the primary deliverable.

## Adding New Team Members
1. Get their LinkedIn CSV export, name it `Connections - [Name].csv`
2. Add entry to `ALL_CSVS` dict in `update_network_ms.py`: `'CODE': f"{BASE_DIR}/Connections - [Name].csv"`
3. Run `python update_network_ms.py`
4. Rebuild `UltronAI_Network_Complete.xlsx`
5. **Spot-check new contacts**: Run verification to ensure:
   - No false positive company matches (especially ARM, Meta, Ring, Apple, Nest)
   - No ex-employees or non-FTEs slipped through
   - Check for content creators (YouTube/Twitch "Partner"/"Creator"), visiting researchers, mentors, advisors
   - Verify anyone with a company field that differs from the target company name is legit (e.g., subsidiary)
6. Update this CLAUDE.md with new stats

## Edge Cases & Lessons Learned

### Company field ≠ Target company name
Some people list subsidiaries or divisions:
- "Amazon Web Services (AWS)" → Amazon
- "Amazon Lab126" → Amazon
- "Ring" → Amazon (but ONLY if standalone, not "engineering")
- "Google DeepMind" → Google
- "Waymo" → Google
- "Facebook" → Meta (old branding, still valid)
- "Oculus VR" → Meta
- "Reality Labs" → Meta
- "Edge Impulse (a Qualcomm company)" → Qualcomm
- "Samsung Research America (SRA)" → Samsung
- "Samsung SDS America" → Samsung
- "SoftBank Investment Advisers" → SoftBank/ARM
- "Softbank Robotics Japan" → SoftBank/ARM

### Twitch "Partner" trap
Twitch uses "Partner" to mean content creator with a partnership agreement. This is NOT an employee. Must be excluded individually since "Partner" in other contexts (e.g., "Partner Engineering Management" at Google) is a valid employee title.

### YouTube "Independent Creator" trap
People list "YouTube" as their company but are content creators, not Google employees.

### "Visiting Researcher" trap
Not an FTE. "Visiting" is now in the position exclusion regex.

### "Mentor" at Google
Some people list Google as company with "Mentor" as their sole title. These are external mentors in Google programs, not employees.

### Company field says one thing, person works somewhere else
Example: Serena Dayal listed "Athena Capital | SoftBank Vision Fund" — primary employer is Athena Capital, SoftBank is advisory. Excluded by name.

### Nest ambiguity
"Nest" matches Google (Google Nest), but "The Nest" standalone or "Nest Labs" before Google acquisition could be false positives. Current exclusion: `^the\s+nest$`.

---

# Patent Outreach Dashboard (`build_dashboard.py`)

## Overview
Single-file Python script (~2600 lines) that reads `ultronai_network.xlsx`, enriches each contact with product mappings and scoring, and outputs a self-contained HTML SPA at `Product Research/dashboard.html`. No external JS/CSS dependencies.

## Data Flow
```
ultronai_network.xlsx ──→ load_network() ──→ raw contacts (660 dicts)
                                                │
UltronPatentLinks.xlsx ──→ patent PDF URLs      │
                                                ▼
                                    map_contact_to_product()   → (division, product, conflict, patent_areas)
                                    map_contact_products_tiered() → (most_relevant[], probable[], possible[])
                                    compute_outreach_score()    → int score
                                                │
                                                ▼
                                    enriched contact dicts (660)
                                                │
                                    ┌───────────┼───────────┐
                                    ▼           ▼           ▼
                              render functions  stats    product_contacts_json
                                    │           │           │
                                    ▼           ▼           ▼
                              HTML f-string template (CSS + HTML + JS)
                                                │
                                                ▼
                              Product Research/dashboard.html
```

## File Anatomy (line ranges approximate)

| Lines | Section |
|-------|---------|
| 1-14 | Imports, paths |
| 16-188 | `PRODUCT_MAP` — per-company regex→product tuples |
| 190-230 | `GENERIC_CATCHALLS` + `COMPANY_CORE_AREAS` |
| 232-389 | `PRODUCT_TAB_DESCRIPTIONS` — one-line product descriptions |
| 391-716 | `PRODUCT_BRIEFS` — 3-sentence what/impact/connection per product |
| 718-721 | `_CATCHALL_EXCLUDE` regex |
| 726-734 | `load_network()` — xlsx loader |
| 738-845 | `CONTACT_OVERRIDES` — ~80 manual name→product overrides |
| 850-881 | `map_contact_to_product()` — primary mapping |
| 888-1043 | `PRODUCT_NAME_KEYWORDS` — strict product-name regexes for tiered matching |
| 1045-1103 | `map_contact_products_tiered()` — 3-tier assignment |
| 1106-1119 | `compute_outreach_score()` |
| 1122-1200 | Main pipeline: load → enrich → filter → stats |
| 1207-1574 | Render functions (esc, render_tags, render_rating, render_contact_row, etc.) |
| 1576-1838 | Build company tabs, network rows, product cards, filter options |
| 1840-2017 | `PATENT_PORTFOLIO` data + patent HTML builder |
| 2019-2612 | **HTML template** (CSS ~2025-2288, body ~2290-2391, JS ~2393-2611) |
| 2614-2617 | Write output file |

## Key Data Structures

### PRODUCT_MAP
```python
PRODUCT_MAP = {
    'Google': [
        (r'regex_pattern', 'Division Name', 'Product Name', conflict_int, ['Patent', 'Areas']),
        ...
    ],
    ...  # 12 companies, ~140 patterns total
}
```
- Regex applied to `f"{position} {company_listed}"` (combined text, case-insensitive)
- Highest conflict_rating wins when multiple patterns match
- If best_rating < 2, falls through to `GENERIC_CATCHALLS` (position-only, not combined)

### Enriched Contact Dict
```python
{
    'name', 'position', 'company', 'company_listed', 'role_type', 'seniority',
    'seniority_level' (int 0-6), 'via', 'linkedin', 'email',
    'most_relevant' (list), 'probable' (list), 'possible' (list),
    'division', 'product', 'conflict' (int 0-4), 'patent_areas' (list),
    'score' (int), 'mapped' (bool)
}
```

### Two Contact Lists
- `all_enriched`: all 660 — used for company tabs, network page, product contacts
- `enriched`: seniority_level >= 3 only (Max Impact) — used for headline stats

### Product Tiers
- **Most Relevant (max 2):** `PRODUCT_NAME_KEYWORDS` regex on position text only. Strict product name mentions.
- **Probable (max 4):** Same division as matched product. Division matching on combined text.
- **Possible (max 5):** Different division, but 2+ shared patent areas, rating >= 2.

## Scoring Formula
```
Score = (conflict × 10) + (seniority_level × 5) + role_bonus + (len(patent_areas) × 2)
```
- role_bonus: IP/Legal=15, M&A=10, Prod/Eng=3, Other=0
- Range: 0–105 theoretical

## HTML SPA Structure

### Pages (sidebar nav, `<div class="page">`)
1. **Patents** (`page-patents`) — 63 patents in 10 categories, status badges, PDF links
2. **Products** (`page-products`) — all products as expandable accordion cards with embedded contacts
3. **Network** (`page-network`) — all 660 contacts, 5-column table, 5 filter dropdowns + tier chips
4. **12 Company tabs** (`page-co-{slug}`) — product summary table + 4-column contacts table
5. **Unmapped** (`page-unmapped`) — contacts with no product match

### Layout
```
body (flex row)
  nav.side (220px sidebar, dark #1e2a38)
  .main (flex column)
    .top (header bar with back/prev/next)
    .content (scrollable, contains all .page divs)
```

### CSS Architecture
- Custom properties: `--bg`, `--s`, `--c`, `--b`, `--t/t2/t3`, `--a/a2`, `--cr/hi/md/lo/gn`, `--sh`
- Font: Georgia/serif for body, system sans-serif for UI elements
- `body { zoom: 1.1 }`
- Responsive: `@media (max-width: 768px)` collapses sidebar; `@media (max-width: 480px)` further mobile
- No dark mode

### Key CSS Classes
- `.ct-table` — contact table (4-col company tabs), `table-layout:fixed`
- `.ct-table.net-table` — network table override (5-col: 10%/16%/30%/34%/10%)
- `.ct-name`, `.ct-pos`, `.ct-meta`, `.ct-sen`, `.ct-via`, `.ct-conflict` — contact cells
- `.net-co` — company name cell in network table
- `.pi`, `.pi-head`, `.pi-body` — product accordion cards
- `.pt-mr`, `.pt-pr`, `.pt-po` — product tier tags (most relevant, probable, possible)
- `.r-critical`, `.r-high`, `.r-medium`, `.r-low` — conflict badges
- `.pat-section`, `.pat-row` — patent portfolio

### JavaScript (all inline, no deps)
- **Navigation:** `sp(i)` switches pages, `_navStack` for back history, arrow keys for prev/next, hash-based URL routing
- **Network filters:** `applyNetFilters()` — AND-combines 5 dropdowns (company, via, seniority, product, tier) + text search. Each row has `data-*` attributes for filtering.
- **Company tab filters:** `applyCtFiltersAll(card)` — AND-combines search + product dropdown + tier chips
- **Product page:** `toggleProd(el)` expands accordion, injects contacts from `const PC = {...}` (JSON embedded at build time). `applyPiFilters()` filters by company chip + search.
- **Cross-linking:** `goPatCat(el)` jumps to patent category; `goDiv(el)` jumps to company tab division
- **Seniority sort order:** Custom mapping `{6:6, 3:5, 5:4, 4:3, 2:2, 1:1, 0:0}` — ranks Head/GM (3) directly below Executive (6), above VP (5) and Director (4). Applied in both network page sort and company tab sort.

### render_contact_row Modes
- `mode='network'`: 5 cols — Company, Name+meta, Position, Products, Conflict
- `mode='default'` + `show_company=False`: 4 cols — Name+meta, Position, Products, Conflict (company tabs)
- `mode='default'` + `show_company=True`: 10 cols — full layout (unmapped page)

All rows carry `data-conflict`, `data-seniority`, `data-name`, `data-score`, `data-products`, `data-tiers`, `data-company`, `data-via` for JS filtering.

## How to Make Common Edits

### Add a new product to a company
1. Add regex tuple to `PRODUCT_MAP[company]` (~line 16-188)
2. Add description to `PRODUCT_TAB_DESCRIPTIONS[company]` (~line 232-389)
3. Add brief to `PRODUCT_BRIEFS[company]` if CRITICAL (~line 391-716)
4. Add strict keywords to `PRODUCT_NAME_KEYWORDS[company]` (~line 888-1043)
5. Add URL to `PRODUCT_URLS` (~line 1259-1413)

### Add a manual contact override
Add to `CONTACT_OVERRIDES` dict (~line 738-845), keyed by full name (case-insensitive match).

### Change table column widths
- Company tabs (4-col): `.ct-table th:nth-child(N)` (~line 2083-2086)
- Network tab (5-col): `.ct-table.net-table th:nth-child(N)` (~line 2087-2091)

### Add a new filter to the network page
1. Add `<select>` element in the HTML template (~line 2320-2327)
2. Add filtering logic in `applyNetFilters()` JS function (~line 2525-2569)
3. Add event listener (~line 2551)

### Add a new page/tab
1. Add nav item in sidebar HTML (~line 2303-2314)
2. Add `<div class="page" id="page-xxx">` in content area
3. Add to JS `P` array and `T` title dict (~line 2394-2395)

### Change scoring weights
Edit `compute_outreach_score()` at ~line 1106-1119.

### Rebuild
```bash
cd "/Users/charlieknott/Downloads/Ultron Internship"
python build_dashboard.py
# Output: Product Research/dashboard.html
```

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
