
---

# 📊 Dashboard Explanation

**Project:** COVID-19 Trends, Severity, and Peak Analysis
**Tool:** Power BI
**Data Source:** Johns Hopkins CSSE COVID-19 Time Series (Public Data)

---

## Overview

This dashboard provides a structured, multi-level view of the COVID-19 pandemic using publicly available global time-series data.
The focus is on **trend evolution, severity, peak stress periods, and timing relationships** between confirmed cases and deaths.

The dashboard is organized into four pages, each answering a different class of analytical questions — from high-level overview to detailed peak analysis.

---

## Page 1 — Executive Overview

**Title:** *COVID-19 Impact Overview: Scale, Severity, and Trends*

### What this page shows

* Overall scale of the pandemic using **Total Confirmed Cases** and **Total Deaths**
* Severity using **Case Fatality Rate (CFR %)**
* Smoothed trends of **new confirmed cases vs new deaths (7-day averages)**

### How to interpret

* KPI cards provide a **snapshot of cumulative impact**
* The 7-day average trend removes daily reporting noise and highlights **true directional movement**
* Comparing confirmed cases and deaths together helps understand **how severity evolved relative to spread**

### Why this matters

This page answers foundational questions such as:

* How large was the impact?
* How severe was it overall?
* Did deaths track cases proportionally over time?

It establishes **context and scale** before deeper analysis.

---

## Page 2 — Trend & Wave Analysis

**Title:** *Infection Waves and Peak Intensity Analysis*

### What this page shows

* Daily new confirmed cases with smoothed trends
* Comparison of infection waves across top countries
* Peak infection intensity using **maximum 7-day average new cases**

### How to interpret

* Multiple waves are visible, showing that the pandemic evolved in **distinct phases**
* Different countries experienced peaks at different times and magnitudes
* Peak intensity highlights periods of **maximum system stress**, not just cumulative totals

### Why this matters

This page helps identify:

* When major waves occurred
* Which regions experienced higher peak loads
* How wave patterns differed across countries

Such insights are useful for **trend monitoring, escalation planning, and comparative analysis**.

---

## Page 3 — Country Deep-Dive

**Title:** *Country-Level COVID-19 Evolution*

### What this page shows

* Daily and smoothed trends for a selected country
* Cumulative confirmed cases and deaths over time

### How to interpret

* Daily vs smoothed trends show short-term volatility versus long-term direction
* Cumulative curves illustrate how quickly impact accumulated during waves
* Selecting a single country allows focused analysis without cross-country noise

### Why this matters

This page supports:

* Country-specific assessments
* Timeline-based interpretation of policy periods or response phases
* Deeper understanding of how trends unfolded locally

It acts as a **case-study view** within the broader global context.

---

## Page 4 — Peak Severity & Lag Snapshot

**Title:** *Peak Severity and Response Lag Snapshot (7-Day Averages)*

### What this page shows

Key peak-related indicators presented as cards:

* Peak month-year for confirmed cases
* Peak month-year for deaths
* Cases at peak (7-day average)
* Deaths at peak load
* Deaths per 1,000 cases at peak load
* Lag (in days) between case peak and death peak

### How to interpret

* Peak month-year shows **when maximum stress occurred**
* Cases and deaths at peak quantify **system load at its worst point**
* Deaths per 1,000 cases at peak reflects **severity under maximum pressure**
* Lag measures how long after infections peaked that deaths peaked, highlighting **response and outcome timing**

### Why this matters

This page brings together timing, severity, and lag into a **single snapshot**, making it easier to:

* Compare peak characteristics across countries
* Understand how outcomes lag leading indicators
* Identify differences between spread intensity and fatal impact

It is especially useful for **post-event analysis, risk assessment, and compliance or audit-style reviews**, where understanding *when*, *how severe*, and *how delayed* outcomes were is critical.

---

## Key Design Choices & Assumptions

* **Recovered data excluded** due to inconsistent reporting across regions
* **7-day moving averages** used to reduce daily reporting noise
* **Lag analysis** based on peak alignment, not individual-level outcomes
* Analysis is **descriptive**, not predictive

These choices prioritize **clarity, comparability, and interpretability** over raw volume.

---

## Summary

Together, the four pages provide:

* A clear overview of scale and severity
* Insight into wave patterns and peak stress
* Country-level evolution over time
* A focused snapshot of peak severity and timing relationships

The dashboard is designed to support **analytical reasoning and interpretation**, enabling users to explore trends, assess severity, and understand timing dynamics without relying on domain-specific assumptions.

---

### End of Document

---
