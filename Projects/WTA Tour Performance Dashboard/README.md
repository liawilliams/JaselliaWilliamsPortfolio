# 🎾 WTA Tour Performance Dashboard

A data visualisation dashboard built in **Tableau** which analyses player and match performance across the **2024 Women's Tennis Association (WTA) Tour season**, created as part of an end-of-module assignment exploring data analysis, dashboard design and visual communication principles.

---

## 📌 Introduction

Tennis is one of the world's most widely followed sports, with over **100 million players globally** and a WTA broadcast audience exceeding **1.1 billion** during the 2024 season alone. Despite this scale, accessible and structured performance analytics for the WTA Tour remain limited outside of proprietary systems.

This project addresses that gap by building an interactive performance dashboard using publicly available match data, designed to serve coaches, analysts, journalists and tournament organisers who require rapid access to player and match insights.

The dataset is sourced from [Jeff Sackmann's tennis_wta GitHub repository](https://github.com/JeffSackmann/tennis_wta), which contains match-level records for every WTA tour event including serve statistics, rankings, surface, round and match duration.

---

## 🎯 Project Aims

- Design and build an interactive dashboard in Tableau featuring multiple charts
- Implement interactive features including drill-down functionality and dynamic filters
- Demonstrate the analytical value of performance data in the context of professional women's tennis

---

## 🛠️ Dashboard Build Summary

<img width="1114" height="684" alt="Screenshot 2026-04-18 at 16 51 43" src="https://github.com/user-attachments/assets/32c0ba5b-3719-4ca4-a1b4-b0b3ee3c3ee3" />

### Data Source
| Field | Detail |
|-------|--------|
| Dataset | `wta_matches_2024.csv` |
| Source | [JeffSackmann/tennis_wta](https://github.com/JeffSackmann/tennis_wta) |
| Records | ~2,800 match-level rows |
| Key columns | `winner_name`, `surface`, `tourney_name`, `winner_rank`, `w_ace`, `w_df`, `w_svpt`, `w_1stIn`, `w_bpSaved`, `w_bpFaced`, `minutes`, `winner_ioc`, `winner_age` |

### Calculated Fields
Four custom fields were created in Tableau to derive meaningful performance metrics:

```
1st Serve %       = [w_1stIn] / [w_svpt]
BP Save %         = [w_bpSaved] / [w_bpFaced]
Double Fault Rate = [w_df] / [w_svpt]
Result Type       = IF [winner_rank] > [loser_rank] THEN "Upset" ELSE "Expected" END
```

### Charts Included

| Sheet | Chart Type | What it Shows |
|-------|-----------|---------------|
| 1 | Stacked Bar Chart | Top 10 players by total wins, broken down by surface |
| 2 | Scatter Plot | First serve % vs break point save rate, coloured by result type |
| 3 | Box Plot | Match duration distribution by court surface |
| 4 | Dual-Axis Line Chart | Average winner ranking and match duration by month |
| 5 | Bar Chart | Average double fault rate — upset vs expected results |
| 6 | Match Detail Table | Individual match records (drill-down target) |
| — | KPI Cards ×5 | Tournaments covered, avg duration, avg aces, avg double faults, upset rate |

### Interactive Features

**Drill-down** — Clicking a player bar in Sheet 1 simultaneously filters both the scatter plot and the match detail table to show only that player's matches.

**Filters** — Three dashboard-wide filters apply across all worksheets simultaneously:
- `Surface` — Hard / Clay / Grass
- `Tournament Level` — All events or Grand Slams only
- `Round` — e.g. Quarter-Finals and beyond

---

## 📊 Key Findings

- **Clay court matches run longest** — the box plot reveals Clay as the surface with the highest median match duration and widest spread, consistent with the slower, more defensive style of play the surface demands.

- **First serve consistency correlates with break point resilience** — the scatter plot trend line shows a positive relationship between 1st Serve % and BP Save %, suggesting that players who get more first serves in face fewer break points and handle them more effectively when they do arise.

- **Upsets produce lower double fault rates** — the double fault rate chart shows that match winners in upset results (lower-ranked beating higher-ranked) tend to commit fewer double faults than winners in expected results, indicating that serve reliability may be a contributing factor in shock results.

---

## 📁 Project Documents

| Document | Description | Link |
|----------|-------------|------|
| 📄 Design & Analysis Report | 1000-word academic report justifying dashboard design decisions with peer-reviewed sources | [View Report](https://your-link-here.com) |
| 📄 Presentation Script | ~500-word script covering context, benefit/impact and future vision | [View Script](https://your-link-here.com) |
| 📄 User Manual | 500 word manual defining key terms and explaining dashboard functionality | [View Manual](https://your-link-here.com) |

---

## 🗂️ Repository Structure

```
📦 wta-dashboard
 ┣ 📄 README.md
 ┣ 📊 WTA_Dashboard.twbx          ← Tableau packaged workbook
 ┣ 📂 data/
 ┃ ┗ 📄 wta_matches_2024.csv      ← Raw dataset
 ┣ 📂 docs/
 ┃ ┣ 📄 WTA_Dashboard_Report.docx
 ┃ ┣ 📄 WTA_Dashboard_Script.docx
 ┃ ┗ 📄 WTA_Dashboard_Manual.docx
```

---

## 🔧 Tools Used

- **Tableau Desktop** — dashboard build and visualisation
- **Microsoft Excel** — data preparation and inspection
- **GitHub** — version control and project documentation

---

## 📚 References

Bach, B., Freeman, E., Abdul-Rahman, A., Turkay, C., Khan, S., Fan, Y. and Chen, M. (2023) 'Dashboard design patterns', *IEEE Transactions on Visualization and Computer Graphics*, 29(1), pp. 342–352. https://doi.org/10.1109/TVCG.2022.3209448

Eberhard, K. (2023) 'The effects of visualization on judgment and decision-making: a systematic literature review', *Management Review Quarterly*, 73(1), pp. 167–214. https://doi.org/10.1007/s11301-021-00235-8

International Tennis Federation (2024) *ITF Global Tennis Report: participation surges to 106 million*. Available at: https://www.itftennis.com/en/news-and-media/articles/itf-global-tennis-report-participation-hits-106-million-in-five-years/

Roland-Garros (2024) *Grand Slam tennis celebrates a record-setting season*. Available at: https://www.rolandgarros.com/en-us/article/worldwide-audiences-grand-slam-tennis-record-onsite-tv-social-media

Shneiderman, B. (1996) 'The eyes have it: a task by data type taxonomy for information visualizations', *Proceedings of the IEEE Symposium on Visual Languages*, Boulder, CO, USA, 3–6 September. IEEE, pp. 336–343.

WTA (2025) *WTA smashes record with 1.1 billion global audience*. Available at: https://www.wtatennis.com/news/4213973/wta-smashes-record-with-11-billion-global-audience

---

*Data sourced from [JeffSackmann/tennis_wta](https://github.com/JeffSackmann/tennis_wta) under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License.*
