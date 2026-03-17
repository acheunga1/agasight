# AGASIGHT 亞太區 — 供應商淨淨價分析儀表板

A single-file HTML dashboard for wine & spirits distributors to analyse supplier promotion packages and calculate true net-net prices after all discounts.

---

## Features

- **AI-powered email parsing** — paste or upload supplier promotion emails; Google Gemini extracts all deal terms automatically
- **Multi-format file support** — `.eml`, `.docx`, `.xlsx`, `.xls`, `.txt`
- **Direct text paste** — paste email content or any supplier quote text directly into the dashboard
- **FOC calculation (two modes)**
  - **均攤 (Package)** — free bottles given upon package completion; total FOC value spread proportionally across all SKUs by spend
  - **專屬 SKU (SKU-specific)** — 11+1 or X+Y deals; discount applied only to the specific SKU
- **Staff incentive tracking** — per-bottle incentives with bottle and dollar caps
- **Suite benefits** — display fees, travel vouchers, consumer dinners, rebates; assignable to all or specific SKUs
- **Trade offers** — buy X get Y free with net price calculation
- **Net-net price calculation** — invoice price minus all discount sources per bottle
- **Excel export** — full breakdown with per-SKU net-net prices and discount %
- **Print / PDF** — print-ready report layout
- **Historical records** — save and reload past promotions
- **CNY 2026 demo data** — one-click sample data load

---

## Setup

### 1. Get a Google Gemini API Key (free tier available)
1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Sign in → click **Get API key** → Create new key
3. Copy the key (starts with `AIza...`)

### 2. Configure the dashboard
1. Open the dashboard URL
2. Click **AI 智能解析設定** to expand the settings panel
3. Select **Google Gemini** as provider
4. Paste your API key
5. Click **自動偵測可用模型** — wait for "✓ Found X models"
6. Click **測試連線** to confirm

### 3. Parse a supplier email
- **Option A — Upload file**: Drag `.eml` / `.docx` / `.xlsx` / `.txt` onto the upload zone
- **Option B — Paste text**: Paste email content into the text box → click **解析文字**

### 4. Review and confirm
- Check the parsed data in the review panel
- Adjust any incorrect values
- Set FOC type per row: **均攤** (package) or **專屬 SKU** (11+1 deal)
- Click **確認並套用**

### 5. Calculate
- Click **計算淨淨價** to run the full discount analysis
- Export to Excel or print the report

---

## Discount Calculation Logic

### Overall discount %
```
Overall Discount % = Total Benefits / Total Order Value
```

### Per-SKU discount (per bottle)
```
Total Discount/btl = FOC Discount/btl + Staff Incentive/btl + Benefits/btl

FOC Discount/btl (均攤) = Package FOC Total × (SKU Revenue / Total Revenue) / SKU Qty
FOC Discount/btl (專屬)  = FOC Qty × Invoice Price / SKU Qty  [only for 11+1 SKUs]
Staff Incentive/btl      = $/btl × min(SKU Qty, Cap Bottles), capped by $ limit
Benefits/btl             = Benefit Value × (SKU Revenue / Total Revenue) / SKU Qty

Net-Net Price/btl = Invoice Price - Total Discount/btl
Discount %        = Total Discount/btl / Invoice Price
```

---

## Notes

- API keys are stored in your **browser's localStorage only** — never uploaded to any server
- Each user needs their own Gemini API key
- Recommended browser: Chrome or Edge
- All data stays local — no backend, no database

---

## Tech Stack

- Pure HTML / CSS / JavaScript (single file, no build step)
- [Google Gemini API](https://ai.google.dev/) for AI parsing
- [mammoth.js](https://github.com/mwilliamson/mammoth.js) for Word document parsing
- [SheetJS](https://sheetjs.com/) for Excel read/write
- [Chart.js](https://www.chartjs.org/) for visualisations

---

*Built for Wai Shing Wines & Spirits — AGASIGHT Asia Pacific*
