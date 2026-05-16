# Salesforce Marketing Cloud Subscriber Engagement Tracker

A framework for tracking, scoring, and managing subscriber engagement
health in Salesforce Marketing Cloud — to protect deliverability and
maximize email performance.

---

## 🎯 Purpose

Subscriber engagement tracking helps you:
- Identify and re-engage at-risk subscribers before they go inactive
- Maintain a clean, high-quality email list
- Protect sender reputation and inbox placement
- Improve overall campaign performance by focusing on engaged audiences

---

## 📐 Engagement Scoring Model

Assign points to subscriber actions to calculate an engagement score:

| Action | Points |
|---|---|
| Email Opened | +3 |
| Link Clicked | +5 |
| Form Submitted | +10 |
| Purchase / Conversion | +15 |
| Email Ignored (no open) | -1 |
| Soft Bounce | -3 |
| Hard Bounce | -10 |
| Spam Complaint | -20 |
| Unsubscribe | Remove immediately |

### Engagement Tiers
| Score | Tier | Action |
|---|---|---|
| 50+ | 🟢 Highly Engaged | Priority audience — send full frequency |
| 25 – 49 | 🟡 Moderately Engaged | Maintain current cadence |
| 10 – 24 | 🟠 At Risk | Reduce frequency — launch re-engagement |
| Below 10 | 🔴 Inactive | Re-engagement campaign or suppress |

---

## 📊 Report 1 — Subscriber Engagement Overview

### SFMC Setup
- **Location:** Contact Builder → Data Extensions
- **Fields to Track:**
  - Subscriber Key
  - Email Address
  - Last Open Date
  - Last Click Date
  - Total Opens (Last 90 Days)
  - Total Clicks (Last 90 Days)
  - Engagement Score (calculated field)
  - Engagement Tier (calculated field)
  - Subscription Date
  - Last Send Date

### SQL Query for SFMC Automation Studio
```sql
SELECT
  s.SubscriberKey,
  s.EmailAddress,
  MAX(o.EventDate) AS LastOpenDate,
  MAX(c.EventDate) AS LastClickDate,
  COUNT(DISTINCT o.JobID) AS TotalOpens,
  COUNT(DISTINCT c.JobID) AS TotalClicks
FROM
  _Subscribers s
  LEFT JOIN _Open o ON s.SubscriberKey = o.SubscriberKey
  LEFT JOIN _Click c ON s.SubscriberKey = c.SubscriberKey
WHERE
  o.EventDate >= DATEADD(day, -90, GETDATE())
GROUP BY
  s.SubscriberKey,
  s.EmailAddress
```

---

## 📊 Report 2 — List Growth Report

### What It Measures
Net list growth over time — new subscribers vs unsubscribes, bounces,

### Key Formula
List Growth Rate = ((New Subscribers - Unsubscribes - Bounces)
÷ Total List Size) × 100

### Metrics to Track Monthly
| Metric | Source |
|---|---|
| New Subscribers | SFMC Subscriber Reports |
| Unsubscribes | SFMC Tracking Reports |
| Hard Bounces Removed | SFMC Bounce Reports |
| Spam Complaints Removed | SFMC Complaint Reports |
| Net List Growth | Formula above |
| Total Active Subscribers | Contact Builder |

### Benchmarks
| Metric | Healthy Target |
|---|---|
| Monthly List Growth Rate | > 2% |
| Unsubscribe Rate | < 0.2% per send |
| List Churn Rate | < 5% per quarter |

---

## 📊 Report 3 — Re-engagement Campaign Tracker

### What It Measures
Tracks the performance of re-engagement campaigns targeting inactive
or at-risk subscribers.

### Re-engagement Campaign Structure
| Email | Timing | Subject Line Approach |
|---|---|---|
| Email 1 | Day 0 | We miss you — here's what's new |
| Email 2 | Day 7 | Are you still interested? |
| Email 3 | Day 14 | Last chance — stay or go |
| Suppress | Day 21 | No response — move to suppression list |

### Metrics to Track
| Metric | Target |
|---|---|
| Re-engagement Open Rate | > 10% |
| Re-engagement Click Rate | > 2% |
| Subscribers Reactivated | Track monthly |
| Subscribers Suppressed | Track monthly |
| List Quality Improvement | Open rate lift after suppression |

---

## 📊 Report 4 — Suppression List Management Report

### What It Measures
Tracks all suppressed contacts and reasons — ensures compliance and
list hygiene.

### Suppression Categories in SFMC
| Category | Reason | Action |
|---|---|---|
| Hard Bounce | Invalid email address | Auto-suppressed by SFMC |
| Unsubscribe | Subscriber opted out | Auto-suppressed by SFMC |
| Spam Complaint | Marked as spam | Auto-suppressed by SFMC |
| Manual Suppression | Internal decision | Added via suppression list |
| Global Unsubscribe | Opted out of all sends | Highest priority suppression |

### Monthly Suppression Audit Checklist
- [ ] Review total suppression list size and growth rate
- [ ] Confirm hard bounces are excluded from all active sends
- [ ] Verify global unsubscribes are honored across all business units
- [ ] Check for any contacts suppressed in error — restore if needed
- [ ] Export suppression list and archive for compliance records

---

## 📅 Engagement Management Cadence

| Activity | Frequency | Owner |
|---|---|---|
| Engagement score update | Weekly | Marketing Ops |
| At-risk segment review | Monthly | Email Marketing Manager |
| Re-engagement campaign launch | Quarterly | Marketing Team |
| Suppression list audit | Monthly | Marketing Ops |
| List growth report | Monthly | Marketing Manager |
| Full subscriber health review | Quarterly | Marketing Director |

---

## ✅ Subscriber Health Checklist

- [ ] Engagement scoring model configured in SFMC or Data Extension
- [ ] Highly engaged segment updated weekly for priority sends
- [ ] At-risk subscribers (90+ days inactive) in re-engagement workflow
- [ ] Inactive subscribers (180+ days) suppressed or removed
- [ ] Hard bounces suppressed immediately after every send
- [ ] Global unsubscribe list honored across all business units
- [ ] List growth rate tracked and reported monthly
- [ ] Re-engagement campaign running every quarter
- [ ] Suppression list audited monthly for compliance

---

## 📝 Notes

> Maintaining a clean, engaged subscriber list is more valuable than
> a large but disengaged one. A smaller engaged list will always
> outperform a large inactive one.
> Built from hands-on Salesforce Marketing Cloud and Marketing Operations
> experience managing multi-channel subscriber databases.

and suppressions.

### Key Formula
