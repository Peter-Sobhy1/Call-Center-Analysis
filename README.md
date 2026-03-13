# 2024 Call Center Analysis — Power BI Dashboard

## Overview

A comprehensive end-to-end Power BI project analyzing 100,000 call center records across 2024. The report covers operational performance, customer behavior, agent efficiency, and satisfaction metrics — structured across five pages with full interactivity, custom navigation, and a clean star schema data model.

## 🔗 Live Dashboard Link
👉 [View Interactive Report](https://app.powerbi.com/view?r=eyJrIjoiMTAxNThjYTAtNTA1Ni00MmU4LTg4YWUtOGE5NzQzNDE1NDdiIiwidCI6IjJiYjZlNWJjLWMxMDktNDdmYi05NDMzLWMxYzZmNGZhMzNmZiIsImMiOjl9)

---

## Pages

### 🏠 Home Page
A branded welcome screen with a background wallpaper and navigation buttons directing users to each of the four analytical pages.


![Home Page](https://github.com/Peter-Sobhy1/Call-Center-Analysis/blob/main/Assets/Home%20Page.png?raw=true)


### 📊 Overview
High-level summary combining the most critical KPIs across all domains in one glance:
- **5** Teams | **71K** Agents | **15%** Transfer Rate | **75%** FCR | **-2.1%** NPS | **38.1%** CSAT | **100K** Total Customers & Calls
- Calls over Time (monthly trend), Calls by Tier, Customers by Type, CSAT % by Team and Contact Channel

![Overview](https://github.com/Peter-Sobhy1/Call-Center-Analysis/blob/main/Assets/Overview.png?raw=true)


### 📞 Calls
Deep dive into call operations:
- **100K** Total Calls | **50/50** Inbound vs Outbound | **14s** AHT | **15%** Transfer Rate | **15K** Escalated Calls | **762** Dropped Calls | **75%** FCR
- Calls by Tier, Calls over Time, Calls by Contact Channel (Phone/App/WhatsApp/Web), Calls by Team, AHT by Team

![Calls](https://github.com/Peter-Sobhy1/Call-Center-Analysis/blob/main/Assets/Calls.png?raw=true)


### 👥 Customers
Geographic and segmentation analysis:
- **33.1%** New Customer Acquisition Rate | **38K** Cities | **100K** Total Customers
- World map of Customers by Location, Top 20 Cities by volume, Customers by Type (New / Returning / VIP), Customer by Account Age Segment (Established / New / Loyal)


![Customers](https://github.com/Peter-Sobhy1/Call-Center-Analysis/blob/main/Assets/Customers.png?raw=true)


### ⭐ CSAT
Customer satisfaction and loyalty metrics:
- **-2.1%** NPS | **71K** Agents | **38.1%** CSAT | **16** Languages | **5** Teams
- CSAT % over Time, CSAT by Customer Type, CSAT by Skill Level (Tier), CSAT by Contact Channel, CSAT by Team


![CSAT](https://github.com/Peter-Sobhy1/Call-Center-Analysis/blob/main/Assets/CSAT.png?raw=true)

---

## Data Model

Star schema with four tables:

| Table | Type | Description |
|---|---|---|
| `fact_table` | Fact | Core call records — Call ID, Date, Agent ID, Customer ID, Call Type, Duration, Handle Time, Hold Time, Queue Time, Transfer Count, Escalation Level, FCR, CSAT, Contact Channel, Call Reason, Callback Requested, Dropped Call, Hour of Day |
| `customers_table` | Dimension | Customer ID, Type, Location, Account Age (days), Account Age Segment |
| `agents_table` | Dimension | Agent ID, Name, Tenure (months), Team, Skill Level (Tier), Languages |
| `date_table` | Dimension | Date, Day, Day of Week, Day of Week Number, Month Name, Month Number, Quarter, Year |
| `_Measures` | Measures Table | Isolated table holding all 20+ DAX measures |

All relationships are **one-to-many**, connecting dimension tables to the fact table.


![Data Model](https://github.com/Peter-Sobhy1/Call-Center-Analysis/blob/main/Assets/Data%20Model.png?raw=true)
---

## Power Query Transformations

- **Source:** Single CSV file imported and used as the base for all tables
- **Dimension extraction:** `customers_table` and `agents_table` created as references from the source; dimension columns removed from the fact table; source table loading disabled to exclude it from the data model
- **DateTime split:** Timestamp column split into separate Date and Time columns to reduce cardinality and improve query performance
- **CSAT recoding:** Numeric CSAT scores replaced with semantic labels — *Promoter*, *Passive*, *Detractor*
- **Column quality checks:** Validated null counts, error rates, and data distributions for all columns
- **Step naming:** Every Power Query step was renamed for readability and maintainability
- **Column cleanup:** Irrelevant and redundant columns removed at each table level

---

## DAX Measures

All measures are organized in a dedicated `_Measures` table. 20+ measures were created, including:

| Measure | Description |
|---|---|
| `Total Calls` | Count of all call records |
| `Inbound Calls` / `Outbound Calls` | Filtered call type counts |
| `Inbound vs Outbound` | Ratio string for KPI card |
| `AHT` | Average Handling Time per second |
| `FCR` | First Call Resolution rate |
| `Transfer Rate` | % of calls transferred |
| `Total Call Dropped` | Count of dropped calls |
| `NO. Escalated Calls` | Count of escalated calls |
| `CSAT %` | Customer satisfaction percentage |
| `NPS` | Net Promoter Score (Promoters − Detractors) |
| `NO. Promoters` / `NO. Detractors` | NPS component counts |
| `Total Customers` | Distinct customer count |
| `New Customers Acquired` | % of new customers |
| `NO. New Customer` / `NO. Returning Customer` / `NO. VIP Customer` | Segmented customer counts |
| `NO. Agents` / `NO. Teams` / `NO. Languages` / `NO. Cities` | Operational dimension counts |
| `Dropped calls per [Team]` | Team-level dropped call breakdown (5 measures) |


![DAX Measures](https://github.com/Peter-Sobhy1/Call-Center-Analysis/blob/main/Assets/Measures.png?raw=true)

---

## Report Features

- **Custom navigation buttons** — page-to-page navigation with active state highlighting per page
- **Clear All Slicers button** — clears all slicer selections AND any manually applied visual-level filters across the page
- **Drill-through** — enabled on area/map visuals for contextual deep dives
- **Color-coded pages** — each page uses a distinct accent color (blue for Calls, green for Customers, pink/red for CSAT, orange for Overview)
- **Consistent layout** — uniform KPI card row, two-slicer filter bar, and back navigation button across all analytical pages

---

## Tools & Technologies

| Tool | Usage |
|---|---|
| Power BI Desktop | Report development, data modeling, DAX |
| Power Query | Data cleaning, data transformation and table structuring |
| DAX | All KPI calculations and measures |
| CSV | Source data format |
| Microsoft Bing Maps | Geographic visualization on Customers page |

---

## Files

```
call_center_analysis.pbix   # Main Power BI report file
call_center_data.csv        # Source dataset (100K rows)
README.md                   # This file
```

---

Let's stay in touch!

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/peter-sobhy/)
