# Salesforce Forecast Accuracy Tracker

A framework for measuring, tracking, and continuously improving sales forecast
accuracy — built for Revenue Operations teams managing pipeline in Salesforce.

---

## 🎯 Purpose

Forecast accuracy tracking exists to:
- Hold Sales and RevOps accountable to committed numbers
- Identify patterns in over/under forecasting by rep, team, or segment
- Build a data-driven forecasting culture across Sales and Leadership
- Reduce revenue surprises at quarter end

> Based on real-world implementation achieving **93% forecast accuracy**
> across a $10M+ revenue portfolio.

---

## 📐 Core Forecast Accuracy Formula
Forecast Accuracy % = 100 - ABS((Forecast - Actual) ÷ Actual × 100)

### Example
| Month | Forecast | Actual | Variance | Accuracy |
|---|---|---|---|---|
| January | $500,000 | $487,000 | -$13,000 | 97.4% |
| February | $520,000 | $561,000 | +$41,000 | 92.7% |
| March | $480,000 | $423,000 | -$57,000 | 88.1% |

### Benchmarks
| Accuracy | Status |
|---|---|
| 95%+ | ✅ Excellent |
| 90% – 94% | 🟢 Strong |
| 80% – 89% | 🟡 Needs Improvement |
| Below 80% | 🔴 At Risk |

---

## 📊 Report 1 — Monthly Forecast vs Actual Report

### Salesforce Setup
- **Report Type:** Opportunities
- **Filters:**
  - Stage = Closed Won
  - Close Date = Last Month / This Quarter
- **Group By:** Owner, Month
- **Summary Fields:** Sum of Amount

### Columns to Include
| Column | Source |
|---|---|
| Rep Name | Opportunity Owner |
| Committed Forecast | Manually logged or forecast field |
| Closed Won Amount | Salesforce Sum |
| Variance ($) | Formula: Actual - Forecast |
| Variance (%) | Formula: Variance ÷ Forecast × 100 |
| Accuracy % | Formula: 100 - ABS(Variance %) |

---

## 📊 Report 2 — Rep Level Forecast Accuracy Report

### What It Measures
Individual rep forecasting patterns — who over-commits, who sandbaggs,
and who forecasts consistently.

### Salesforce Setup
- **Report Type:** Opportunities
- **Filters:**
  - Close Date = This Quarter
  - Stage = Closed Won OR Stage = Commit
- **Group By:** Owner
- **Summary Fields:** Sum of Amount, Count of Opportunities

### Forecast Categories in Salesforce
| Category | Definition |
|---|---|
| Commit | Rep is highly confident — will close this period |
| Best Case | Could close if everything goes right |
| Pipeline | Early stage — possible but not committed |
| Omitted | Excluded from forecast intentionally |

### Patterns to Watch
| Pattern | What It Means |
|---|---|
| Rep consistently over-forecasts | Needs coaching on deal qualification |
| Rep consistently under-forecasts | May be sandbagging — review incentives |
| High variance quarter to quarter | Inconsistent pipeline hygiene |
| Accurate within 5% consistently | Strong forecaster — document their process |

---

## 📊 Report 3 — Quarter End Variance Report

### What It Measures
Total forecast vs actual at the team and company level for the full quarter.

### Salesforce Setup
- **Report Type:** Opportunities
- **Filters:**
  - Close Date = Last Quarter
  - Stage = Closed Won, Closed Lost
- **Group By:** Stage, Owner
- **Summary Fields:** Sum of Amount

### Executive Summary Format
Q[X] FORECAST ACCURACY SUMMARY
─────────────────────────────────────────
Total Committed Forecast:    $[amount]
Total Closed Won:            $[amount]
Variance:                    $[amount] ([+/-]%)
Overall Forecast Accuracy:   [%]
By Team:
├── Enterprise:            [accuracy %]
├── Mid-Market:            [accuracy %]
└── SMB:                   [accuracy %]
Top Accurate Reps:           [names]
Highest Variance Reps:       [names]
─────────────────────────────────────────

---

## 📊 Report 4 — Rolling Forecast Trend Report

### What It Measures
Forecast accuracy trend over the last 6–12 months — shows whether
forecasting is improving or deteriorating over time.

### Salesforce Setup
- **Report Type:** Opportunities
- **Filters:**
  - Close Date = Custom Range (Last 6 Months)
  - Stage = Closed Won
- **Group By:** Close Month
- **Summary Fields:** Sum of Amount

### Visualize As
- **Line chart** — Forecast vs Actual over time
- **Bar chart** — Accuracy % per month
- Build in **Salesforce Dashboard** or export to **Looker Studio / Power BI**

---

## ✅ Forecast Accuracy Improvement Checklist

- [ ] All reps update forecast category weekly (by Friday EOD)
- [ ] Pipeline reviewed and cleaned every Monday before forecast call
- [ ] Deals without activity in 14+ days flagged and reviewed
- [ ] Close dates are realistic — not pushed just to stay in quarter
- [ ] Commit deals have a clear next step and decision maker confirmed
- [ ] Monthly variance review shared with Sales Manager and Leadership
- [ ] Quarterly accuracy trends reviewed in QBR

---

## 📅 Forecasting Cadence

| Activity | Frequency | Owner |
|---|---|---|
| Rep updates forecast categories | Weekly (Friday) | Sales Rep |
| Manager reviews team forecast | Weekly (Monday) | Sales Manager |
| RevOps publishes forecast report | Weekly | Revenue Operations |
| Forecast vs Actual review | Monthly | RevOps + Sales Director |
| Full accuracy trend review | Quarterly | Leadership + RevOps |

---

## 📝 Notes

> Forecast accuracy improves significantly when combined with a strong
> pipeline health process. See the Pipeline Health Report in this repo
> for the full framework.
> Built from hands-on Revenue Operations experience achieving 93% forecast
> accuracy across a $10M+ revenue portfolio.
