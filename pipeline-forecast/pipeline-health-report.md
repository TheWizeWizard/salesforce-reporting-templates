# Salesforce Pipeline Health Report

A structured framework for monitoring pipeline coverage, stage distribution,
deal velocity, and risk indicators — built for Revenue Operations and Sales
leadership teams.

---

## 🎯 Purpose

A healthy pipeline report answers three core questions:
- Do we have **enough** pipeline to hit our revenue target?
- Is the pipeline **moving** through stages at the right pace?
- Where are the **risks** and what needs immediate attention?

---

## 📊 Report 1 — Pipeline Coverage Report

### What It Measures
Pipeline coverage ratio — the total value of open opportunities vs revenue target.

### Salesforce Setup
- **Report Type:** Opportunities
- **Filters:**
  - Close Date = This Quarter
  - Stage ≠ Closed Won, Closed Lost
- **Columns:**
  - Opportunity Name
  - Account Name
  - Stage
  - Amount
  - Close Date
  - Probability (%)
  - Owner

### Key Formula
Pipeline Coverage Ratio = Total Open Pipeline Value ÷ Revenue Target
### Benchmarks
| Coverage Ratio | Health Status |
|---|---|
| Below 2x | 🔴 At Risk — insufficient pipeline |
| 2x – 3x | 🟡 Needs Attention — borderline |
| 3x – 4x | 🟢 Healthy |
| 4x+ | ✅ Strong — good buffer for slippage |

---

## 📊 Report 2 — Stage Distribution Report

### What It Measures
How deals are distributed across pipeline stages — identifies bottlenecks
and stage stagnation.

### Salesforce Setup
- **Report Type:** Opportunities
- **Filters:**
  - Stage ≠ Closed Won, Closed Lost
  - Close Date = This Quarter + Next Quarter
- **Group By:** Stage
- **Summary Fields:** Count of Opportunities, Sum of Amount

### What to Look For
| Signal | What It Means |
|---|---|
| Too many deals in early stages | Pipeline is top-heavy, unlikely to close this quarter |
| Too many deals in late stages | Short-term revenue is healthy but future pipeline is thin |
| Deals stuck in one stage 30+ days | Process bottleneck or deal stagnation — needs rep review |
| High volume, low average deal size | May need to focus on higher-value accounts |

---

## 📊 Report 3 — Deal Velocity Report

### What It Measures
How fast deals move through the pipeline — average time per stage and
overall sales cycle length.

### Salesforce Setup
- **Report Type:** Opportunities (with Stage History)
- **Filters:**
  - Close Date = Last 90 Days
  - Stage = Closed Won
- **Columns:**
  - Opportunity Name
  - Created Date
  - Close Date
  - Days to Close (formula field)
  - Stage Duration (per stage)
  - Amount

### Key Formula
Average Sales Cycle = Sum of Days to Close ÷ Total Closed Won Deals
Deal Velocity = (Number of Deals × Win Rate × Average Deal Size) ÷ Sales Cycle Length

### Benchmarks by Deal Size
| Deal Size | Healthy Sales Cycle |
|---|---|
| Under $10K | 14 – 30 days |
| $10K – $50K | 30 – 60 days |
| $50K – $100K | 60 – 90 days |
| $100K+ | 90 – 180 days |

---

## 📊 Report 4 — Pipeline Risk Report

### What It Measures
Identifies deals at risk of slipping, being lost, or going dark.

### Salesforce Setup
- **Report Type:** Opportunities
- **Filters:**
  - Close Date = This Quarter
  - Stage ≠ Closed Won, Closed Lost
  - Last Activity Date < 14 Days Ago
- **Columns:**
  - Opportunity Name
  - Account Name
  - Stage
  - Amount
  - Close Date
  - Last Activity Date
  - Days Since Last Activity (formula field)
  - Owner

### Risk Flags to Monitor
| Risk Signal | Action Required |
|---|---|
| No activity in 14+ days | Rep follow-up required immediately |
| Close date pushed 2+ times | Re-qualify or mark at risk |
| Probability dropped by 20%+ | Review with rep — understand blockers |
| No next step logged | Manager review and coaching |
| Single stakeholder contact only | Expand relationship — multi-thread |

---

## 📅 Reporting Cadence

| Report | Frequency | Audience |
|---|---|---|
| Pipeline Coverage | Weekly | Sales Manager, RevOps |
| Stage Distribution | Weekly | Sales Manager, Marketing |
| Deal Velocity | Monthly | Sales Director, Leadership |
| Pipeline Risk | Weekly | Sales Manager, Rep Level |
| Full Pipeline Review | Quarterly | Executive Team |

---

## ✅ Pipeline Health Checklist

- [ ] Pipeline coverage ratio is 3x+ against quarterly target
- [ ] No deals stuck in same stage for 30+ days
- [ ] All deals have a next step and activity logged within 14 days
- [ ] Average sales cycle is within benchmark for deal size
- [ ] Risk report reviewed weekly with Sales Manager
- [ ] Pipeline reviewed and updated by reps every Friday

---

## 📝 Notes

> Salesforce formula fields for Days to Close and Days Since Last Activity
> may need to be created by your Salesforce Admin if not already available.
> Built from hands-on Revenue Operations and Salesforce Admin experience.





