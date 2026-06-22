# 🏨 Revenue Insights in Hospitality Domain — AtliQ Grands

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-Data%20Analysis-217346?logo=microsoft-excel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Measures-blue)
![Domain](https://img.shields.io/badge/Domain-Hospitality-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

# 📋 Table of Contents

- 📌 Project Overview
- 🎯 Objective
- 🗂️ Dataset Information
- 🧠 Key Business Metrics
- 🛠️ Tools & Techniques Used
- ⚙️ Data Transformation Steps
- 📊 Dashboard Screenshots
- 💡 Key Insights
- 📈 Dashboard Analysis Approach
- 📁 Repository Structure
- 🚀 How to Use This Project

---

# 📌 Project Overview

AtliQ Grands is a well-established hospitality company that owns multiple five-star hotels across India. With over 20 years in the industry, it operates in both the Luxury and Business hotel categories across major cities — Mumbai, Delhi, Hyderabad, and Bangalore.

Recently, AtliQ Grands has been losing market share and revenue due to strategic moves from competitors and ineffective decision-making. To counter this, the Managing Director decided to adopt Business and Data Intelligence as a strategic initiative.

Since the company lacked an in-house analytics team, a third-party service provider (that's me!) was hired to analyze historical data and deliver actionable revenue insights through an interactive Power BI dashboard.

---

# 🎯 Objective

Build a comprehensive Revenue Intelligence Dashboard that empowers stakeholders to:

- Identify performance gaps.
- Understand booking behaviour.
- Analyze occupancy trends.
- Track revenue performance.
- Support data-driven decision-making.

---

## 🗂️ Dataset Information

The dataset consists of **5 CSV files** covering the period **May – July (Weeks 19 to 31)**.

| File | Description |
|--------|------------|
| **dim_date.csv** | Dates with week number, month, and day type (Weekday/Weekend) |
| **dim_hotels.csv** | Hotel property details — name, city, and category (Luxury/Business) |
| **dim_rooms.csv** | Room types mapped to class (Standard, Elite, Premium, Presidential) |
| **fact_aggregated_bookings.csv** | Successful bookings and room capacity per property, date, and room type |
| **fact_bookings.csv** | Individual booking records with revenue, status, platform, and ratings |

## Column Highlights (fact_bookings)

| Column | Description |
|----------|------------|
| booking_id | Unique booking identifier |
| booking_status | Checked Out / Cancelled / No Show |
| booking_platform | Booking platform |
| revenue_generated | Potential revenue |
| revenue_realized | Actual revenue received |
| ratings_given | Customer rating |
| no_guests | Number of guests |


> 📁 **Full column descriptions are available in `meta_data_hospitality.txt`.**,
---

## 🧠 Key Business Metrics (Hospitality Jargon)

| Metric | Formula | What It Tells You |
|----------|---------|-------------------|
| **RevPAR** | Total Revenue ÷ Total Rooms Available or ADR × Occupancy% | Revenue efficiency per available room |
| **ADR** | Total Room Revenue ÷ Rooms Sold | Average price at which rooms were sold |
| **Occupancy %** | Rooms Occupied ÷ Rooms Available × 100 | How well room capacity is being utilised |
| **DSRN** | Daily Sellable Room Nights | Available rooms each day (highlights blocking/maintenance issues) |
| **Realisation %** | URN ÷ BRN | Ratio of customers who actually stayed vs. those who booked |
| **URN** | Utilized Room Nights | Rooms where the customer actually checked in and stayed |
| **BRN** | Booked Room Nights | Total rooms booked (includes cancellations and no-shows) |

> ⚠️ **Industry Note:** In hospitality, **Weekdays = Sunday to Thursday** and **Weekends = Friday & Saturday**.
---

## 🛠️ Tools & Techniques Used

### Tools

- **Power BI Desktop** — Dashboard design and visualisation
- **Power Query (M Language)** — Data loading, transformation, and modelling
- **DAX (Data Analysis Expressions)** — Calculated columns and measures
- **Excel** — Metrics list and reference data

### Power BI Skills Applied

- Data modelling (Star Schema)
- Calculated columns using DAX
- 26+ custom measures including RevPAR, ADR, Occupancy, Realisation %
- Bookmarks and page navigation buttons
- KPI indicators and conditional formatting
- Dynamic titles based on applied filters
- Week-on-Week change indicators

---

## ⚙️ Data Transformation Steps

### Power Query Processing

- Removed the pre-built `day_type` column from `dim_date` (industry definition differs — Fri/Sat = Weekend)
- Recreated `day_type` as a DAX calculated column using `WEEKDAY()` logic
- Applied **"Use First Row as Headers"** fix for `dim_rooms`
- Loaded all 5 CSV files via a folder connector and expanded each as a separate table

### Key DAX Measures

#### Revenue

```DAX
Revenue =
SUM(fact_bookings[revenue_realized])
```

#### Total Bookings

```DAX
Total Bookings =
COUNT(fact_bookings[booking_id])
```

#### Occupancy %

```DAX
Occupancy % =
DIVIDE([Total Rooms Occupied], [Total Rooms Available])
```

#### ADR

```DAX
ADR =
DIVIDE([Revenue], [Rooms Sold])
```

#### RevPAR

```DAX
RevPAR =
DIVIDE([Revenue], [Total Rooms Available])
```

#### Realisation %

```DAX
Realisation % =
DIVIDE([URN], [BRN])
```

#### day_type (Calculated Column)

```DAX
day_type =
VAR wkd = WEEKDAY(dim_date[date])
RETURN IF(wkd > 5, "Weekend", "Weekday")
```

📊 **All 26+ measures are documented in `metrics list.xlsx`.**

---

# 📊 Dashboard Screenshots

## 🔹 Main Revenue Insights Dashboard

![Revenue Insights](Images/Revenue-Insights.png)

---

## 🔹 Property-Level Key Metrics

![Property Metrics](Images/property_key_metrics.png)

---

## 🔹 Revenue Trend by Week

![Revenue Trend](Images/Revenue_trend_by_week.png)

---

## 🔹 Occupancy Percentage

![Occupancy Percentage](Images/occupancy_percentage.png)

---

## 🔹 RevPAR

![RevPAR](Images/Revpar.png)

---

## 🔹 ADR

![ADR](Images/ADR.png)

---

## 🔹 DSRN

![DSRN](Images/DSRN.png)

---

## 🔹 Realisation Percentage

![Realisation Percentage](Images/realisation_percentage.png)

---

## 🔹 Detailed Revenue Insights

![Revenue Details](Images/revenue_insights.png)

---

# 💡 Key Insights

- 📍 Mumbai generates the highest revenue.
- 🏆 AtliQ Exotica is the top-performing property.
- 🛏️ AtliQ Bay has the highest occupancy rate (66%).
- 📅 Week 24 recorded peak revenue at ₹139.6M.
- 🌆 Delhi leads in occupancy and ratings.
- ❌ ₹298M revenue loss due to cancellations.
- 🛎️ Elite room class has the highest bookings and cancellations.
- 💰 Luxury hotels contribute ~61.62% of total revenue.
- 📉 Weekends consistently outperform weekdays.
- 📱 MakeYourTrip drives ~41% of bookings.
- 🔄 Realisation % remains around 70%.

---

# 📈 Dashboard Analysis Approach

### Level 1 — Diagnostic Analysis

KPIs:

- Revenue
- RevPAR
- Occupancy %
- ADR
- DSRN
- Realisation %

### Level 2 — Deep Dive Analysis

Breakdown by:

- City
- Property
- Platform
- Room Class

---

# 📁 Repository Structure

```text
📦 Revenue-Insights-Hospitality-Domain
├── 📂 Images
│   ├── Revenue-Insights.png
│   ├── property_key_metrics.png
│   ├── Revenue_trend_by_week.png
│   ├── occupancy_percentage.png
│   ├── Revpar.png
│   ├── ADR.png
│   ├── DSRN.png
│   ├── realisation_percentage.png
│   └── revenue_insights.png
├── Revenue Insights in Hospitality Domain.pbix
└── README.md
```

---

# 🚀 How to Use

### Clone Repository

```bash
git clone https://github.com/wasif32/Revenue-Insights-Hospitality-Domain.git
```

### Open Power BI File

Open:

```
Revenue Insights in Hospitality Domain.pbix
```

using Power BI Desktop.

Update the data source path if required.

Explore using filters:

- Property
- City
- Booking Status
- Platform
- Month

---

# ⭐ Support

If you found this project useful, please give it a ⭐ on GitHub.

**Happy Analyzing! 🚀**
