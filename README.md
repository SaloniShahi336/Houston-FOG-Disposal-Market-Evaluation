# Houston FOG Disposal Market Evaluation

> Spatial market evaluation of the Greater Houston metro area for grease trap waste (GTW) disposal infrastructure — analyzing 14,532 food establishments, 10 registered processing facilities, and 54 high-density restaurant zones to identify market-entry opportunities for a private capital-backed pretreatment platform.

---

## 🛠️ Tools & Technologies

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white)
![Folium](https://img.shields.io/badge/Folium-77B829?style=flat)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![OpenStreetMap](https://img.shields.io/badge/OpenStreetMap-7EBC6F?style=flat&logo=openstreetmap&logoColor=white)
![GeoJSON](https://img.shields.io/badge/GeoJSON-4E9A06?style=flat)

---

## 📌 Business Problem

A private capital-backed pretreatment platform needed to evaluate the Greater Houston metro area as a potential market for new grease trap waste (GTW) disposal facilities. The core questions:

- Where is restaurant density concentrated across the 9-county MSA — and where are the gaps in disposal infrastructure?
- Which counties have the highest demand-to-supply imbalance?
- What regulatory and economic factors create tailwinds for market entry?
- Where should the first facility be located for maximum impact?

This analysis was built as a complete market evaluation exercise combining geospatial analysis, competitive intelligence, regulatory research, and market sizing.

---

## 📊 Data

| Source | Dataset | Records | Application |
|---|---|---|---|
| U.S. Census Bureau | County Business Patterns 2023 | 14,532 establishments | Demand baseline (NAICS 722) |
| OpenStreetMap | Overpass Turbo API | 4,502 geocoded locations | Spatial density mapping |
| TCEQ Registry | MSW Facility Database | 22 liquid waste facilities | Competitive landscape |
| EPA ECHO | NPDES Permit Database | — | WWTP capacity verification |
| City of Houston | Public Works FOG Program | 9 counties | Surcharge rates & FOG limits |
| Southwaste.com | Public volume reporting | — | Market sizing benchmark |

---

## ⚙️ Methodology

1. **Data Collection** — Queried OpenStreetMap Overpass Turbo API separately for each of 9 MSA counties; pulled Census CBP data for official establishment counts; extracted and filtered TCEQ facility registry for 5GG, 5TL, and 5LV facility types
2. **Data Cleaning** — Removed entries with missing coordinates, standardized county assignments, deduplicated records, and verified operational status of all 10 registered 5GG facilities through company research
3. **Interactive Heat Map** — Built a folium map with real GeoJSON county boundaries, restaurant density layer, color-coded competitor markers (red = 5GG, orange = 5TL, blue = 5LV), county labels with restaurant counts, and a custom legend
4. **Automated Gap Analysis** — Divided the MSA into a 2km × 2km grid (783 cells with restaurants), identified top 15% by density, clustered into 54 high-density zones, calculated haversine distance from each zone to every 5GG facility, classified zones into 4 tiers (Underserved > 15 mi, Moderate Gap 10–15 mi, Slight Gap 5–10 mi, Served < 5 mi)
5. **Neighborhood Identification** — Built coordinate-to-name lookup to replace generic "Houston" labels with specific neighborhoods (Galleria/Uptown, Chinatown/Bellaire, Memorial/Spring Branch, etc.)
6. **Competitor Deep-Dive** — Verified operational status of all 10 5GG facilities; discovered 3 were permitted but never constructed (one since 1989); identified Southwaste as dominant operator controlling ~62% of mapped service area across two facilities
7. **Market Sizing** — Used Southwaste's public volume data (275M+ gallons in 2025) and industry tip fee benchmarks ($0.05–$0.15/gal) to estimate $13.75M–$41.25M annual revenue for a single dominant operator
8. **Regulatory Analysis** — Researched FOG discharge limits, surcharge rate structures, EPA Consent Decree obligations, and 2026 hauler enforcement changes across all 9 counties
9. **Visualization** — Created 6 analytical charts (matplotlib), interactive map (folium), treemap and facility table (Power BI)

---

## 📈 Key Results

| Finding | Detail |
|---|---|
| Infrastructure imbalance | **8 of 9 counties** have zero GTW processing facilities |
| Underserved zones | **50%** of high-density restaurant zones are 10+ miles from nearest disposal |
| Average disposal distance | **11.7 miles** across all 54 zones |
| Active competitors | Only **6 of 10** registered 5GG facilities are operating |
| Market concentration | Southwaste controls **~62%** of mapped service area |
| Primary recommendation | **Fort Bend County** — 1,522 establishments, zero competitors, 870K population |
| Regulatory tailwind | Houston FOG limit tightened **400 → 200 mg/L** (Dec 2023) — doubles addressable market |
| Market size (single operator) | **$13.75M–$41.25M** estimated annual tip fee revenue |

---

## 🖼️ Visualizations

| Visualization | Description |
|---|---|
| [`Houston_Market_Map2.html`](Houston_Market_Map2.html) | Interactive heat map — open in browser to explore restaurant density, county boundaries, and competitor locations |
| [`Chart1_Distance_By_County.png`](Charts/Chart1_Distance_By_County.png) | Distance from restaurant hot spots to nearest 5GG facility, grouped by county |
| [`Chart2_County_Gap_Summary.png`](Charts/Chart2_County_Gap_Summary.png) | Stacked bar chart — high-density zones per county by gap classification |
| [`Chart3_Opportunity_By_County.png`](Charts/Chart3_Opportunity_By_County.png) | Scatter plot — restaurant count vs. distance to nearest facility, colored by county |
| [`Chart_Surcharge_Rates.png`](Charts/Chart_Surcharge_Rates.png) | Surcharge rate ranges by county with FOG limits on secondary axis |
| [`Chart_FOG_Limits.png`](Charts/Chart_FOG_Limits.png) | FOG discharge limits by county with regulatory strictness color coding |


---

## ▶️ How to Run

```bash
# Clone the repo
git clone https://github.com/SaloniShahi336/Houston-FOG-Disposal-Market-Evaluation.git
cd Houston-FOG-Disposal-Market-Evaluation

# Install dependencies
pip install pandas folium matplotlib numpy geopy squarify openpyxl

# Run the notebook
jupyter notebook Houston.ipynb
```

**To view the interactive map:** Open `Houston_Market_Map2.html` directly in any browser — no dependencies required.

---

## 📁 Repository Structure

```
Houston-FOG-Disposal-Market-Evaluation/
├── Houston_Clean.ipynb                    # Main analysis notebook
├── Houston_Market_Evaluation_Report.pdf   # Written market evaluation report
├── Houston_Market_Map2.html               # Interactive heat map (open in browser)
├── Houston_All_Restaurants.csv            # 4,502 geocoded restaurant locations
├── Houston_GTW_Competitors.xlsx           # TCEQ competitor facility data
├── Houston_Gap_Analysis_Complete.csv      # 54-zone gap analysis output
├── CBP2023_CB2300CBP-Data.csv             # Census County Business Patterns data
├── Surcharge_county.xlsx                  # Surcharge rate data by county
├── msw-facilities-texas.xls               # Full TCEQ MSW facility registry
├── Chart1_Distance_By_County.png          # Distance analysis chart
├── Chart2_County_Gap_Summary.png          # Gap assessment chart
├── Chart3_Opportunity_By_County.png       # Opportunity matrix chart
├── Chart_Surcharge_Rates.png              # Surcharge rate comparison
├── Chart_FOG_Limits.png                   # FOG discharge limit comparison
├── Chart_Infrastructure_Gap.png           # Infrastructure gap infographic
└── README.md
```

---

## 💡 Learnings

- **Haversine distance matters for real-world logistics analysis** — Euclidean distance would underestimate disposal distances by 10–15% in a metro area this spread out; using haversine gave operationally realistic gap assessments
- **Public data stacking creates institutional-grade analysis** — combining Census CBP (demand), TCEQ registry (supply), and municipal rate structures (economics) produced a market evaluation comparable to consulting deliverables, using only free data sources
- **Permit ≠ operational** — 3 of 10 registered facilities were permitted but never constructed (one since 1989); blindly trusting regulatory filings would have overstated competitive pressure by 50%
- **Grid-based spatial analysis scales better than manual zoning** — the 2km grid approach automatically identified density clusters without subjective boundary decisions, and the threshold-based classification made the output reproducible
- **Regulatory research is a data source** — the FOG limit tightening (400 → 200 mg/L) wasn't in any dataset but fundamentally changed the market sizing; combining quantitative analysis with qualitative regulatory intelligence produced the strongest recommendations

---

## 📄 Data Sources

- [U.S. Census Bureau — County Business Patterns 2023](https://data.census.gov/table/CBP2023.CB2300CBP)
- [OpenStreetMap — Overpass Turbo](https://overpass-turbo.eu/)
- [TCEQ Municipal Solid Waste Facility Registry](https://www.tceq.texas.gov/permitting/waste_permits/msw_permits/msw-facilities)
- [EPA ECHO Database](https://echo.epa.gov/)
- [City of Houston — FOG Program](https://www.publicworks.houstontx.gov/)
