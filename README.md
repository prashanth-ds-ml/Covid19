
---

# 📊 COVID-19 Trends, Severity & Peak Analysis (Power BI)

An end-to-end analytical dashboard built in **Power BI** using publicly available COVID-19 time-series data.
The project focuses on **trend evolution, severity, peak stress periods, and timing relationships** between confirmed cases and deaths.

🔗 **Interactive Dashboard (Public):**
👉 [https://app.powerbi.com/view?r=eyJrIjoiOWMyZGU4MWItYjhiNC00MDA1LTkzNjItOTdkOGE5N2EwZmU3IiwidCI6IjBkNGYwMzExLWYwMmUtNDE2MS05ZTc4LTg3M2ZmYTk5OWIwOCJ9](https://app.powerbi.com/view?r=eyJrIjoiOWMyZGU4MWItYjhiNC00MDA1LTkzNjItOTdkOGE5N2EwZmU3IiwidCI6IjBkNGYwMzExLWYwMmUtNDE2MS05ZTc4LTg3M2ZmYTk5OWIwOCJ9)

---

## 📌 Project Objectives

* Analyze global and country-level COVID-19 trends
* Identify infection waves and peak intensity periods
* Assess severity using deaths and case fatality metrics
* Understand timing relationships (lag) between cases and deaths
* Present insights in a clean, decision-oriented dashboard

---

## 📂 Data Source

* **Johns Hopkins CSSE COVID-19 Time Series Dataset**
* Public, globally aggregated daily data
* Metrics used:

  * Confirmed cases
  * Deaths

Recovered data was intentionally excluded due to inconsistent reporting across regions.

---

## 🧠 Key Analytical Concepts Used

* Daily change analysis
* 7-day moving averages to reduce reporting noise
* Cumulative trend analysis
* Peak intensity detection
* Lag analysis between leading (cases) and lagging (deaths) indicators
* Severity assessment at peak system load

---

## 📄 Dashboard Structure

### **Page 1 — Executive Overview**

* Total Confirmed Cases
* Total Deaths
* Case Fatality Rate (CFR %)
* Smoothed trends of new confirmed cases vs deaths

**Purpose:** Establish overall scale and severity.

---

### **Page 2 — Trend & Wave Analysis**

* Daily vs smoothed infection trends
* Cross-country wave comparison
* Peak infection intensity by country (7-day average)

**Purpose:** Identify major waves and peak stress periods.

---

### **Page 3 — Country Deep-Dive**

* Daily and smoothed trends for selected country
* Cumulative confirmed cases and deaths over time

**Purpose:** Country-level evolution and case-study analysis.

---

### **Page 4 — Peak Severity & Lag Snapshot**

* Peak month-year for cases and deaths
* Cases and deaths at peak load (7-day average)
* Deaths per 1,000 cases at peak
* Lag (in days) between case peak and death peak

**Purpose:** Summarize peak severity, timing, and response lag in a single view.

---

## 📐 Key Design & Modeling Decisions

* 7-day moving averages used instead of raw daily values
* Peak analysis based on maximum smoothed values
* Lag calculated using peak alignment, not individual records
* All measures implemented using DAX with a star-schema model
* DimDate table used for consistent time intelligence

---

## 📘 Documentation

* **DAX Measures Explanation:**
  See `DAX_Explanation.md` for detailed measure-by-measure logic and intent.

* **Dashboard Interpretation:**
  See `Dashboard_Explanation.md` for page-wise insights and interpretation.

---

## 🔍 Tools & Technologies

* Power BI Desktop & Power BI Service
* DAX (Time intelligence, filtering, aggregation)
* Public health time-series data
* GitHub for version control and documentation

---

## ⚠️ Notes & Limitations

* Analysis is descriptive, not predictive
* Reporting delays and backfills may affect peak alignment
* CFR values depend on confirmed case reporting quality
* Results should be interpreted as analytical insights, not clinical conclusions

---

