# 🏥 Lowell General Hospital — KPI Analysis (2020–2024)

> **A data analytics project investigating how hospital overcrowding affects nursing staff responsiveness and patient safety.**  
> Built with Python · Pandas · SciPy · Matplotlib

---

## 📌 What This Project Is About

Lowell General Hospital operates at **95–97% bed occupancy** — well above the nationally recommended safe zone of 85%. This project asks a simple but critical question:

> **Does an overcrowded hospital lead to slower staff response times — and does that put patients at risk of falling?**

Using **5 years of monthly data (2020–2024)** across three key performance indicators (KPIs), this analysis finds:

- ✅ Yes — high occupancy **predicts** higher fall rates (r = +0.70)
- ✅ Yes — lower staff responsiveness **closely tracks** more patient falls (r = −0.79)
- ✅ The problem is **seasonal** — January, September, and December are consistently the highest-risk months

---

## 📁 Repository Structure

```
lowell-hospital-kpi-analysis/
│
├── src/
│   └── analysis.py                  # Full Python script — loads data, cleans it, and produces all 7 charts
│
├── charts/                          # Output folder — all 7 charts are saved here after running the script
│   ├── chart_occupancy.png
│   ├── chart_staff.png
│   ├── chart_falls.png
│   ├── chart_all_kpis.png
│   ├── chart_scatter1.png
│   ├── chart_scatter2.png
│   └── chart_seasonal.png
│
├── data/
│   └── 2.RAW_DATA.xlsx              # Source data — monthly hospital records (not included; see Data section)
│
├── Lowell_Hospital_Lisha_Final.pptx # Presentation deck with full narrative and findings
│
└── README.md                        # This file
```

---

## 🗂️ The Dataset

| Field | Description |
|---|---|
| **Month** | Monthly timestamp from Jan 2020 to Dec 2024 (60 rows total) |
| **Occupancy_Rate** | % of licensed beds filled each day (decimal, e.g. 0.96 = 96%) |
| **Unassisted_Fall_Rate** | Falls per 1,000 patient days with no staff present |
| **Staff_Resp_Score** | HCAHPS "Top Box" score — % of patients rating staff response as "Always" |
| **Unassisted_Fall_Pct** | Unassisted falls as a % of all falls |
| **Staff_Resp_Score_Pct** | Responsiveness as a normalized % for correlation analysis |
| **Benchmark** | The national HCAHPS benchmark for staff responsiveness (65%) |

**Sources:**
- Bed occupancy → Internal hospital records
- Staff responsiveness → [HCAHPS Survey](https://www.hcahpsonline.org/) (post-discharge patient survey)
- Fall rate → [NDNQI](https://www.nursingquality.org/) (National Database of Nursing Quality Indicators)

> ⚠️ The raw Excel file is not included in this repo to protect hospital data. The script expects it at the path configured in `SAVE_DIR` inside `src/analysis.py`. Update that path before running.

---

## 📊 The Three KPIs — Explained Simply

### KPI 1 · Bed Occupancy Rate
**"How full is the hospital?"**

```
Formula:  (Patients in beds per day ÷ Total licensed beds) × 100
```

A **licensed bed** is a hospital bed officially approved for patient use by regulators. When this number stays above 95%, the hospital has almost no spare capacity — no room to absorb a surge, no time to thoroughly clean and prepare rooms, and nursing staff spread impossibly thin.

**Industry benchmark:** 65–75% for acute care hospitals nationally.  
**Lowell's reality:** 95–97% — every year, without exception.

---

### KPI 2 · Staff Responsiveness Top Box Score
**"Are patients getting help when they press the call button?"**

```
Formula:  (Patients who answered "Always" to both call-button questions ÷ Total respondents) × 100
```

This comes from the **HCAHPS survey** — a standardized, federally mandated patient satisfaction questionnaire given after discharge. Two questions specifically measure staff responsiveness:
1. *How often did you get help as soon as you wanted after you pressed the call button?*
2. *How often did you get help to the bathroom or bedpan as soon as you wanted?*

**"Top Box"** means only "Always" counts — "Usually" is not good enough.  
**National benchmark:** 65% (the minimum acceptable score)  
**Lowell's range:** 60.6% (2022 low) to 65.3% (2020 baseline)

---

### KPI 3 · Unassisted Patient Fall Rate
**"How often are patients falling with no one there to help them?"**

```
Formula:  (Number of unassisted falls ÷ Number of patient days) × 1,000
```

A **patient fall** is any unplanned descent to the floor. **Unassisted** means no staff member was present to help or catch the patient.

**Patient days** normalizes this for volume — 100 patients × 3 days each = 300 patient days. This makes fair comparison possible even when patient volume changes year to year.

**Why this matters:** Unassisted falls are largely preventable with adequate staffing and proactive check-ins. They are a direct signal of nursing capacity under strain.

**Lowell's range:** 2.25 (2020) → 2.82 (2022–23 peak) → 2.57 (2024)

---

## 📈 The Charts — What Each One Shows

### Chart 1 · `chart_occupancy.png` — Bed Occupancy Bar Chart
![Occupancy Chart](charts/chart_occupancy.png)

**What it shows:** Year-by-year average bed occupancy from 2020 to 2024 as a bar chart.

**Key insight:** Occupancy crept upward from 95% → 97% and never dipped below 95% in any year. This tells us the hospital has been operating at or above its safe ceiling for the entire analysis window. There is no buffer. Any unexpected surge immediately strains the system.

**How to read it:** Each bar = one year. The percentage label on top = average occupancy across all 12 months of that year. Higher bars = more crowded hospital.

---

### Chart 2 · `chart_staff.png` — Staff Responsiveness vs. Benchmark
![Staff Responsiveness Chart](charts/chart_staff.png)

**What it shows:** The staff responsiveness score over time as a line, compared against the national 65% benchmark shown as an orange dashed line.

**Key insight:** Lowell crossed below the benchmark in 2021 and did not recover to it by 2024. The worst year was 2022 at 60.6% — 7 percentage points below benchmark. The pink/red shaded area between the score line and the benchmark line visually represents the **"gap of dissatisfaction"** — wider shading = more patients feeling underserved.

**How to read it:** The teal line = Lowell's actual score. The orange dashed line = the 65% national standard. Red shading below the dashed line = below benchmark. Mint shading above = at or above benchmark.

---

### Chart 3 · `chart_falls.png` — Unassisted Fall Rate
![Falls Chart](charts/chart_falls.png)

**What it shows:** The unassisted fall rate per 1,000 patient days for each year from 2020 to 2024.

**Key insight:** Falls rose from 2.25 (2020) to a peak of 2.82 (2022–23), the same years staff responsiveness hit its lowest point. This is not a coincidence — the timing aligns precisely. The slight improvement to 2.57 in 2024 mirrors the partial recovery in responsiveness, but rates remain well above the 2020 baseline.

**How to read it:** Each bar = one year. The number on top = falls per 1,000 patient days (a standardized rate, not raw count). Higher bars = more patient safety risk.

---

### Chart 4 · `chart_all_kpis.png` — All 3 KPIs Side by Side
![All KPIs Chart](charts/chart_all_kpis.png)

**What it shows:** Three bars per year — one for each KPI — so you can see how all three metrics move together (or diverge) across time.

**Key insight:** Looking at all three together makes the pattern impossible to miss. As occupancy (teal) stays high, falls (orange) rise and responsiveness (navy) drops — in sync. This grouped view is the "headline slide" of the analysis: one chart, three signals, one story.

**How to read it:** For each year, there are three grouped bars. Teal = occupancy %. Orange = fall %. Navy = responsiveness %. The y-axis is a % scale shared across all three metrics for comparability.

---

### Chart 5 · `chart_scatter1.png` — Fall % vs. Staff Responsiveness (Correlation)
![Scatter 1 Chart](charts/chart_scatter1.png)

**What it shows:** A scatter plot where each dot is one month of data. The x-axis is the unassisted fall percentage; the y-axis is the staff responsiveness score. The orange diagonal line is the linear regression trend line.

**Key insight:** Pearson correlation coefficient **r = −0.791** — a strong negative relationship. This means: when falls go up, responsiveness goes down, and vice versa. The dots cluster tightly around the trend line, confirming this is not random. It is a real, measurable relationship.

**How to read it:** Each dot = one month. Dots in the upper-left = low falls + high responsiveness (good). Dots in the lower-right = high falls + low responsiveness (bad). The trend line shows the overall direction of the relationship.

---

### Chart 6 · `chart_scatter2.png` — Bed Occupancy vs. Fall Rate (Correlation)
![Scatter 2 Chart](charts/chart_scatter2.png)

**What it shows:** A scatter plot where each dot is one month. The x-axis is bed occupancy %; the y-axis is the unassisted fall %. The orange diagonal is the trend line.

**Key insight:** Pearson correlation coefficient **r = +0.700** — a strong positive relationship. When the hospital fills up more, patients fall more. This chart closes the causal loop: overcrowding → staff stretched thin → patients fall unassisted.

**How to read it:** Each dot = one month. Dots in the upper-right = high occupancy + high falls (dangerous). Dots in the lower-left = lower occupancy + fewer falls (safer). The upward-sloping trend line confirms the direction.

---

### Chart 7 · `chart_seasonal.png` — Monthly Seasonality (Dual-Axis)
![Seasonal Chart](charts/chart_seasonal.png)

**What it shows:** A dual-axis chart combining average fall rates by month (orange bars, left axis) with average staff responsiveness scores by month (teal line, right axis), averaged across all five years.

**Key insight:** Risk is not random — it is **predictable by month**. January, September, and December consistently show elevated fall rates alongside the lowest responsiveness scores. The pattern is driven by flu-season admissions surges, holiday staffing shortfalls, and year-end budget constraints. This means the hospital can forecast high-risk windows and staff proactively.

**How to read it:** Orange bars (left axis) = average fall rate for that month. Teal line (right axis) = average staff responsiveness for that month. When bars are tall AND the line dips simultaneously, the risk is highest. Note the inverse mirror pattern — the two metrics move in opposite directions almost every month.

---

## 🔬 Statistical Findings

| Relationship | Pearson r | Interpretation |
|---|---|---|
| Fall % ↔ Staff Responsiveness | **−0.791** | Strong negative — when staff are less responsive, more patients fall |
| Occupancy % ↔ Fall % | **+0.700** | Strong positive — more crowded = more falls |

> **What is Pearson r?** It ranges from −1 to +1. Values above ±0.7 are considered strong correlations in healthcare research. The negative sign means the two variables move in opposite directions; positive means they move together.

---

## 💡 Recommendations

Based on the data, three low-cost, high-impact interventions emerge:

| # | Recommendation | Data Rationale |
|---|---|---|
| 1 | **Dynamic Staffing Triggers** — When occupancy is forecast to exceed 95%, automatically assign float pool nurses to call-button coverage | r = +0.700 confirms overcrowding directly drives falls. Proactive staffing breaks this chain upstream. |
| 2 | **Proactive Bathroom Rounding** — Mandate 2-hour nursing check-ins during peak-risk months (Jan, Sep, Dec) and high-occupancy shifts | Monthly seasonal analysis shows these spikes are predictable — they can be staffed for, not just reacted to. |
| 3 | **Targeted Staff Training** — Train nurses on triage protocols for call-button responses during high-occupancy shifts to reduce time-to-response | r = −0.791 is the strongest signal in the dataset. Even small improvements in responsiveness can measurably reduce falls. |

---

## 🚀 How to Run This Project

### Prerequisites

```bash
pip install pandas numpy matplotlib scipy openpyxl
```

### Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/your-username/lowell-hospital-kpi-analysis.git
   cd lowell-hospital-kpi-analysis
   ```

2. **Add your data file**  
   Place `2.RAW_DATA.xlsx` in the `data/` folder. The Excel file must have a sheet named `Case Study Dataset` with columns in this order:
   ```
   [blank] | Month | Occupancy_Rate | Unassisted_Fall_Rate | Staff_Resp_Score | Unassisted_Fall_Pct | Staff_Resp_Score_Pct | Benchmark
   ```

3. **Update the path in the script**  
   Open `src/analysis.py` and change `SAVE_DIR` to point to your local `charts/` folder:
   ```python
   SAVE_DIR = r'path/to/lowell-hospital-kpi-analysis/charts'
   FILE_PATH = os.path.join(SAVE_DIR, '..', 'data', '2.RAW_DATA.xlsx')
   ```

4. **Run the script**
   ```bash
   python src/analysis.py
   ```
   Or open it in Jupyter Notebook — the `%matplotlib inline` directive at the top handles inline display automatically.

5. **View outputs**  
   All 7 charts are saved as `.png` files in the `charts/` folder.

---

## 🛠️ Tools & Libraries

| Tool | Purpose |
|---|---|
| **Python 3.x** | Core programming language |
| **Pandas** | Data loading, cleaning, and aggregation |
| **NumPy** | Numerical operations and array handling |
| **Matplotlib** | Chart creation and styling |
| **SciPy (stats)** | Pearson correlation and linear regression |
| **openpyxl** | Reading `.xlsx` Excel files |

---

## 👤 Author

**Lisha Bhowmik**  
BBA Graduate · Data & Business Analyst

This project was developed as a healthcare analytics case study to demonstrate end-to-end data analysis — from raw Excel data to statistical findings to actionable business recommendations.

---

## 📎 Resources

- 📊 **Full presentation:** [`Lowell_Hospital_Lisha_Final.pptx`](Lowell_Hospital_Lisha_Final.pptx) — includes slide-by-slide narrative, chart explanations, and recommendations
- 🏥 [HCAHPS Survey Information](https://www.hcahpsonline.org/)
- 📋 [NDNQI — Nursing Quality Indicators](https://www.nursingquality.org/)
