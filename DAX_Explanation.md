
---

# 📘 DAX Measures Explanation

**Project:** COVID-19 Trend, Severity & Ops Analysis (Power BI)
**Author:** *Your Name*
**Purpose:** Explain all DAX measures used in the dashboard with clear intent and logic.

---

## 1️⃣ Base Measures

### **Total Confirmed**

**Purpose:**
Returns the total number of confirmed COVID-19 cases in the current filter context.

**Logic:**
Filters the fact table to include only records where the metric is *Confirmed* and sums their values.

```DAX
Total Confirmed =
CALCULATE (
    SUM ( FactCovid[Value] ),
    FactCovid[Metric] = "Confirmed"
)
```

---

### **Total Deaths**

**Purpose:**
Returns the total number of COVID-19 related deaths.

**Logic:**
Similar to *Total Confirmed*, but filters for *Deaths*.

```DAX
Total Deaths =
CALCULATE (
    SUM ( FactCovid[Value] ),
    FactCovid[Metric] = "Deaths"
)
```

---

### **CFR % (Case Fatality Rate)**

**Purpose:**
Measures severity by showing the proportion of deaths relative to confirmed cases.

**Logic:**
Uses `DIVIDE` to safely compute deaths divided by confirmed cases.

```DAX
CFR % =
DIVIDE ( [Total Deaths], [Total Confirmed] )
```

---

## 2️⃣ Daily Change Measures

### **Daily New Confirmed Cases**

**Purpose:**
Calculates day-over-day increase in confirmed cases.

**Logic:**
Subtracts yesterday’s total from today’s total.
Negative values are clamped to zero to handle reporting anomalies.

```DAX
Daily New Confirmed Cases =
VAR TodayTotal = [Total Confirmed]
VAR YesterdayTotal =
    CALCULATE (
        [Total Confirmed],
        DATEADD ( DimDate[Date], -1, DAY )
    )
VAR Delta = TodayTotal - YesterdayTotal
RETURN
IF (
    ISBLANK ( YesterdayTotal ),
    BLANK (),
    MAX ( 0, Delta )
)
```

---

### **Daily New Deaths**

**Purpose:**
Calculates day-over-day increase in deaths.

```DAX
Daily New Deaths =
VAR TodayTotal = [Total Deaths]
VAR YesterdayTotal =
    CALCULATE (
        [Total Deaths],
        DATEADD ( DimDate[Date], -1, DAY )
    )
VAR Delta = TodayTotal - YesterdayTotal
RETURN
IF (
    ISBLANK ( YesterdayTotal ),
    BLANK (),
    MAX ( 0, Delta )
)
```

---

## 3️⃣ Smoothed Trend Measures (7-Day Averages)

### **7D Moving Avg New Confirmed Cases**

**Purpose:**
Removes daily noise to highlight true infection trends.

**Logic:**
Averages daily new confirmed cases over the last 7 days.

```DAX
7D Moving Avg New Confirmed Cases =
VAR EndDate = MAX ( DimDate[Date] )
VAR Last7Days =
    DATESINPERIOD ( DimDate[Date], EndDate, -7, DAY )
RETURN
AVERAGEX ( Last7Days, [Daily New Confirmed Cases] )
```

---

### **7D Moving Avg New Deaths**

**Purpose:**
Shows smoothed mortality trends.

```DAX
7D Moving Avg New Deaths =
VAR EndDate = MAX ( DimDate[Date] )
VAR Last7Days =
    DATESINPERIOD ( DimDate[Date], EndDate, -7, DAY )
RETURN
AVERAGEX ( Last7Days, [Daily New Deaths] )
```

---

## 4️⃣ Cumulative Measures

### **Cumulative Confirmed**

**Purpose:**
Shows cumulative growth of confirmed cases over time.

**Logic:**
Sums confirmed cases up to the current date using a rolling date filter.

```DAX
Cumulative Confirmed =
CALCULATE (
    [Total Confirmed],
    FILTER (
        ALL ( DimDate[Date] ),
        DimDate[Date] <= MAX ( DimDate[Date] )
    )
)
```

---

### **Cumulative Deaths**

**Purpose:**
Shows cumulative deaths over time.

```DAX
Cumulative Deaths =
CALCULATE (
    [Total Deaths],
    FILTER (
        ALL ( DimDate[Date] ),
        DimDate[Date] <= MAX ( DimDate[Date] )
    )
)
```

---

## 5️⃣ Peak Intensity Measures

### **Peak 7D Moving Avg New Confirmed**

**Purpose:**
Identifies the maximum infection intensity for ops analysis.

```DAX
Peak 7D Moving Avg New Confirmed =
MAXX (
    VALUES ( DimDate[Date] ),
    [7D Moving Avg New Confirmed Cases]
)
```

---

### **Peak 7D Moving Avg New Deaths**

**Purpose:**
Identifies the maximum mortality intensity.

```DAX
Peak 7D Moving Avg New Deaths =
MAXX (
    VALUES ( DimDate[Date] ),
    [7D Moving Avg New Deaths]
)
```

---

## 6️⃣ Peak Timing Measures

### **Peak Date – New Confirmed (7D Avg)**

**Purpose:**
Returns the earliest date when peak confirmed cases occurred.

```DAX
Peak Date – New Confirmed (7D Avg) =
VAR PeakValue = [Peak 7D Moving Avg New Confirmed]
RETURN
CALCULATE (
    MIN ( DimDate[Date] ),
    FILTER (
        ALL ( DimDate[Date] ),
        [7D Moving Avg New Confirmed Cases] = PeakValue
    )
)
```

---

### **Peak Date – New Deaths (7D Avg)**

**Purpose:**
Returns the earliest date when peak deaths occurred.

```DAX
Peak Date – New Deaths (7D Avg) =
VAR PeakValue = [Peak 7D Moving Avg New Deaths]
RETURN
CALCULATE (
    MIN ( DimDate[Date] ),
    FILTER (
        ALL ( DimDate[Date] ),
        [7D Moving Avg New Deaths] = PeakValue
    )
)
```

---

## 7️⃣ Lag & Severity Measures (Ops / Program Insights)

### **Lag (Deaths after Cases) – Days**

**Purpose:**
Measures the response window between case peak and death peak.

**Logic:**
Computes the date difference and clamps negative values to zero to handle multi-wave effects.

```DAX
Lag (Deaths after Cases) – Days =
VAR CasePeakDate = [Peak Date – New Confirmed (7D Avg)]
VAR DeathPeakDate = [Peak Date – New Deaths (7D Avg)]
VAR LagDays =
    DATEDIFF ( CasePeakDate, DeathPeakDate, DAY )
RETURN
IF (
    ISBLANK ( CasePeakDate ) || ISBLANK ( DeathPeakDate ),
    BLANK (),
    MAX ( 0, LagDays )
)
```

---

### **Cases at Case Peak (7D Avg)**

```DAX
Cases at Case Peak (7D Avg) =
VAR PeakDate = [Peak Date – New Confirmed (7D Avg)]
RETURN
CALCULATE (
    [7D Moving Avg New Confirmed Cases],
    KEEPFILTERS ( DimDate[Date] = PeakDate )
)
```

---

### **Deaths at Case Peak (7D Avg)**

```DAX
Deaths at Case Peak (7D Avg) =
VAR PeakDate = [Peak Date – New Confirmed (7D Avg)]
RETURN
CALCULATE (
    [7D Moving Avg New Deaths],
    KEEPFILTERS ( DimDate[Date] = PeakDate )
)
```

---

### **Deaths at Death Peak (7D Avg)**

```DAX
Deaths at Death Peak (7D Avg) =
VAR PeakDate = [Peak Date – New Deaths (7D Avg)]
RETURN
CALCULATE (
    [7D Moving Avg New Deaths],
    KEEPFILTERS ( DimDate[Date] = PeakDate )
)
```

---

### **Cases at Death Peak (7D Avg)**

```DAX
Cases at Death Peak (7D Avg) =
VAR PeakDate = [Peak Date – New Deaths (7D Avg)]
RETURN
CALCULATE (
    [7D Moving Avg New Confirmed Cases],
    KEEPFILTERS ( DimDate[Date] = PeakDate )
)
```

---

### **Deaths per 1,000 Cases at Case Peak**

**Purpose:**
Measures severity when system load was highest.

```DAX
Deaths per 1,000 Cases at Case Peak =
VAR d = [Deaths at Case Peak (7D Avg)]
VAR c = [Cases at Case Peak (7D Avg)]
RETURN
IF (
    ISBLANK ( d ) || ISBLANK ( c ),
    BLANK (),
    DIVIDE ( d, c ) * 1000
)
```

---

## 8️⃣ Display Measures (For Cards Only)

### **Peak Month-Year – Cases**

```DAX
Peak Month-Year – Cases =
VAR d = [Peak Date – New Confirmed (7D Avg)]
RETURN IF ( ISBLANK ( d ), BLANK (), FORMAT ( d, "MMM YYYY" ) )
```

---

### **Peak Month-Year – Deaths**

```DAX
Peak Month-Year – Deaths =
VAR d = [Peak Date – New Deaths (7D Avg)]
RETURN IF ( ISBLANK ( d ), BLANK (), FORMAT ( d, "MMM YYYY" ) )
```

---

## ✅ Notes & Assumptions

* Recovered data excluded due to inconsistent reporting
* 7-day averages used to reduce noise
* Lag values reflect peak alignment, not individual outcomes
* All analysis is descriptive, not predictive

---


