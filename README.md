# FP20 Analytics Challenge #35
 B2B Sales Pipeline &amp; Deals Analytics - Challenge #35  


---

## 🚀 Overview

A **3-page executive Power BI report** built for the **B2B Sales Pipeline & Deals Analytics — Challenge #35** by FP20 Analytics, analyzing an enterprise sales pipeline of **11,750 deals** across **55 sales reps**, **6 product categories**, and **4 global regions**.

Built with **ZoomCharts Drill Down visuals**, **advanced DAX**, and a **dark executive theme** to transform raw pipeline data into clear, actionable business insights.


---

## 🖥️ Report Preview

| Page 1 | Page 2 | Page 3 |
|--------|--------|--------|
| Pipeline Overview | Pipeline Health Monitor | Sales Execution Analysis |
| KPIs · Funnel · Trends | Risk Tiers · Velocity · Activity | Reps · Heatmap · Map |

---
![business](https://github.com/dstar211/Enterprise-Sales-Pipeline-Intelligence-/blob/main/p%201%20-%20Copy.jpg) 

![ pipli](https://github.com/dstar211/Enterprise-Sales-Pipeline-Intelligence-/blob/main/p%202.jpg)

![Pipline](https://github.com/dstar211/Enterprise-Sales-Pipeline-Intelligence-/blob/main/P%203.jpg)

![Pipline](https://github.com/dstar211/Enterprise-Sales-Pipeline-Intelligence-/blob/main/p%203%202%20.jpg) 

![Pipline](https://github.com/dstar211/Enterprise-Sales-Pipeline-Intelligence-/blob/main/p%204.jpg) 

---

## 📄 Report Pages 

### Page 1 —  Pipeline Overview
> End-to-end pipeline visibility with executive KPIs

| KPI | Value |
|-----|-------|
| 💰 Total Pipeline Value | £606M |
| ✅ Revenue Closed | £241M |
| 🎯 Win Rate | 60.2% |
| ⚖️ Weighted Pipeline | £252M |
| 📦 Avg Deal Size | £87K |

**Visuals:**
- Pipeline Funnel by Stage
- Win Rate by StageName (Green/Red bars)
- Revenue vs Pipeline Trend (Area Chart)
- Deals by ProductCategory (Column)
- Deals by Status (Donut)
- Weighted Pipeline by Country (Bar)

---

### Page 2 —  Pipeline Health Monitor
> Catch stalled deals before they are lost

#### -Tier Deal Risk Classification System

**Visuals:**
- Pipeline Funnel by Stage
- Stage Conversion Rate (Green/Red)
- Deal Velocity Trend (Area)
- Stage Age Heatmap (Color matrix)
- Activity Volume by Type (Stacked bar)
- Deal Risk Distribution (4-tier cards)

---

### Page 3 —  Sales Execution Analysis
> Rep performance, productivity and impact

**Visuals:**
- 📈 Revenue Trend by Product *(ZoomCharts Combo Bar PRO)*
- ⬡ Rep Performance Health Scatter (Activity vs Win Rate)
- ▣ Pipeline Ownership by Rep *(ZoomCharts Drill Down Bar PRO)*
- 🌍 Total Deals by Country (Bubble Map)
- ◫ Industry × Region Revenue Heatmap (Matrix)

---

## 🛠️ DAX Measures — Key Highlights

### Base Measures
```dax
Revenue Closed =
CALCULATE(
    SUM(FactDeals[DealValueEUR]),
    FactDeals[Status] = "Won"
)

Win Rate % =
DIVIDE(
    CALCULATE(COUNTROWS(FactDeals), FactDeals[Status] = "Won"),
    CALCULATE(COUNTROWS(FactDeals), FactDeals[Status] IN {"Won","Lost"}),
    0
)
```



### ▲▼→ Reference Labels (All KPI Cards)
```dax
Revenue Closed Label =
VAR curr  = [Revenue Closed]
VAR lm    = CALCULATE([Revenue Closed], DATEADD(DimDate[Date],-1,MONTH))
VAR pct   = DIVIDE(curr - lm, lm, 0)
VAR arrow = IF(pct > 0, "▲", IF(pct < 0, "▼", "→"))
RETURN arrow & " " & FORMAT(ABS(pct),"0.0%") & " vs Last Month"
```

### Rep Quadrant Scoring
```dax
Rep Quadrant =
VAR wr     = [Rep Win Rate]
VAR ac     = [Rep Activity Count]
VAR avg_wr = [Avg Win Rate All Reps]
VAR avg_ac = [Avg Activity Count All Reps]
RETURN
SWITCH(
    TRUE(),
    wr >= avg_wr && ac >= avg_ac,  Star Performer",
    wr >= avg_wr && ac <  avg_ac,  Efficient Closer",
    wr <  avg_wr && ac >= avg_ac, High Effort Low Win",
                                   Needs Coaching"
)
```

> 📄 Full DAX reference (35+ measures) available in the `/DAX` folder

---

## 🗄️ Data Model

```
FactDeals (11,750 rows)
    ├── CreatedDateKey      ──▶  DimDate[DateKey]       ← ACTIVE
    ├── LastActivityDateKey ──▶  DimDate[DateKey]       ← INACTIVE
    ├── CompanyID           ──▶  DimCompany[CompanyID]
    └── RepID               ──▶  DimSalesRep[RepID]

FactActivities (117,500 rows)
    ├── DealID              ──▶  FactDeals[DealID]
    └── RepID               ──▶  DimSalesRep[RepID]

DimDate        (1,492 rows)   ← Marked as Date Table
DimCompany     (1,000 rows)
DimSalesRep    (55 rows)
```

---



## ⚡ Technical Highlights

| Feature | Detail |
|---------|--------|
| ZoomCharts | Drill Down Combo Bar PRO + Bar PRO with breadcrumb navigation |
| Date Handling | YYYYMMDD integer keys converted via DATE(LEFT/MID/RIGHT) |
| Inactive Relationship | USERELATIONSHIP for LastActivityDateKey → DimDate |
| Reference Labels | ▲▼→ vs Last Month on every KPI card |
| Risk Engine | 4-tier SWITCH with conditional formatting |
| Rep Benchmarking | AVERAGEX per-rep quadrant scoring |
| Toggles | Bookmark actions for dynamic visual switching |
| Slicers | Synced across all 3 pages — Year · Region · Role · Size |

---

## 📊 Key Business Insights

| Insight | Finding |
|---------|---------|
| 🏆 Top Product | Cloud Migration — £230M · 64.5% win rate |
| 🌍 Top Region | Europe — £583M (57% of revenue) |
| 🇫🇷 Top Country | France — £29.6M |
| ⭐ Top Rep | Eva Pereira — £16.7M · 206 deals |
| 🎯 Best Role WR | Customer Success — 63.4% |
| 🏢 Enterprise vs SMB | £159K avg deal vs £39K |
| 📞 Best Activity | Meeting (highest Won ratio) |

---

## 🏆 Challenge Details

| | |
|-|-|
| **Challenge** | B2B Sales Pipeline & Deals Analytics — Challenge #35 |
| **Organiser** | FP20 Analytics |
| **Dataset Author** | Federico Pastor |
| **Tool** | Power BI Desktop |
| **Custom Visuals** | ZoomCharts Drill Down PRO |
| **Community** | Enterprise DNA |

---

## 🙏 Acknowledgements

A huge thank you to **Federico Pastor** for designing such a rich and challenging dataset, and to **ZoomCharts** for the incredible tooling — the drill-down experience and breadcrumb navigation made the storytelling feel genuinely executive-ready in a way standard Power BI visuals simply can't match. And to **Enterprise DNA** for the community and resources that make challenges like this possible.

---

## 📬 Connect

[![LinkedIn](https://www.linkedin.com/in/durvesh-patil23 )
[![Live Report](https://app.powerbi.com/view?r=eyJrIjoiMDUxZDg3ODItNWEyZC00YjlmLThhOGEtODM2ODU4Yjc2YjY1IiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9)

---

<p align="center">
Built with ❤️ for <strong>B2B Sales Pipeline & Deals Analytics — Challenge #35</strong>
<br/><br/>
<img src="https://img.shields.io/badge/FP20%20Analytics-Challenge%2035-2563EB?style=flat-square"/>
<img src="https://img.shields.io/badge/Power%20BI-Report-F2C811?style=flat-square&logo=powerbi&logoColor=black"/>
<img src="https://img.shields.io/badge/ZoomCharts-Drill%20Down-FFD700?style=flat-square"/>
</p>

