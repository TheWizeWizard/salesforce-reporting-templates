# Salesforce Marketing Cloud Email Campaign Performance Report

A framework for measuring, analyzing, and optimizing email campaign
performance in Salesforce Marketing Cloud (SFMC).

---

## 🎯 Purpose

A structured email performance report helps you:
- Measure campaign effectiveness against industry benchmarks
- Identify underperforming sends before they damage deliverability
- Optimize send times, subject lines, and audience segments
- Prove email ROI to leadership with revenue-linked metrics

---

## 📐 Core Email Metrics Framework

### Delivery Metrics
| Metric | Formula | Benchmark |
|---|---|---|
| Delivery Rate | Delivered ÷ Total Sent × 100 | > 98% |
| Bounce Rate (Hard) | Hard Bounces ÷ Total Sent × 100 | < 0.5% |
| Bounce Rate (Soft) | Soft Bounces ÷ Total Sent × 100 | < 2% |
| Spam Complaint Rate | Complaints ÷ Delivered × 100 | < 0.08% |

### Engagement Metrics
| Metric | Formula | Benchmark |
|---|---|---|
| Open Rate | Unique Opens ÷ Delivered × 100 | 20% – 35% |
| Click Through Rate (CTR) | Unique Clicks ÷ Delivered × 100 | 2% – 5% |
| Click to Open Rate (CTOR) | Unique Clicks ÷ Unique Opens × 100 | 10% – 20% |
| Unsubscribe Rate | Unsubscribes ÷ Delivered × 100 | < 0.2% |

### Conversion Metrics
| Metric | Formula | Benchmark |
|---|---|---|
| Conversion Rate | Conversions ÷ Unique Clicks × 100 | Varies by goal |
| Revenue per Email | Total Revenue ÷ Emails Delivered | Varies by list size |
| ROI | (Revenue - Cost) ÷ Cost × 100 | > 3600% industry avg |

---

## 📊 Report 1 — Campaign Send Summary Report

### SFMC Setup
- **Location:** Email Studio → Tracking → Send Reports
- **Report:** Summary Send Report
- **Metrics to Pull:**
  - Total Sent
  - Total Delivered
  - Unique Opens
  - Unique Clicks
  - Unsubscribes
  - Bounces (Hard + Soft)
  - Spam Complaints

### Export Format
Export as CSV and load into:
- **Salesforce Reports** via Data Extension
- **Looker Studio** for visualization
- **Power BI** for executive dashboards

---

## 📊 Report 2 — Subject Line Performance Report

### What It Measures
Which subject lines drive the highest open rates — used to optimize
future send copy and A/B testing strategy.

### SFMC Setup
- **Location:** Email Studio → Tracking → Email Send Summary
- **Group By:** Email Name / Subject Line
- **Metrics:** Unique Opens, Open Rate, CTR, CTOR

### Subject Line Analysis Framework
| Element | What to Test | Winning Signal |
|---|---|---|
| Length | Short (< 40 chars) vs Long | Higher open rate |
| Personalization | First name vs no name | Higher open rate |
| Emoji | With vs without | Higher open rate |
| Question vs Statement | "Are you ready?" vs "Get ready" | Higher open rate |
| Urgency | "Last chance" vs standard | Higher CTR |

---

## 📊 Report 3 — Audience Segment Performance Report

### What It Measures
How different audience segments respond to email campaigns — identifies
your most and least engaged subscriber groups.

### SFMC Setup
- **Location:** Email Studio → Subscribers → Data Extensions
- **Group By:** Segment / Data Extension Name
- **Metrics:** Open Rate, CTR, Unsubscribe Rate, Conversion Rate

### Recommended Segments to Track
| Segment | Definition |
|---|---|
| Highly Engaged | Opened or clicked in last 30 days |
| Moderately Engaged | Opened or clicked in last 31–90 days |
| At Risk | No open or click in 91–180 days |
| Inactive | No open or click in 180+ days |
| New Subscribers | Subscribed in last 30 days |

---

## 📊 Report 4 — Deliverability Health Report

### What It Measures
Email deliverability indicators — catches issues before they impact
inbox placement and sender reputation.

### Key Deliverability Signals
| Signal | Healthy Range | Action if Outside Range |
|---|---|---|
| Hard Bounce Rate | < 0.5% | Remove hard bounces immediately |
| Soft Bounce Rate | < 2% | Monitor — suppress after 3 soft bounces |
| Spam Complaint Rate | < 0.08% | Review list quality and opt-in process |
| Unsubscribe Rate | < 0.2% | Review content relevance and frequency |
| Inbox Placement Rate | > 90% | Check authentication (SPF, DKIM, DMARC) |

### SFMC Deliverability Tools
- **Email Studio → Tracking** — bounce and complaint reports
- **Contact Builder** — suppression list management
- **Sender Authentication Package (SAP)** — SPF, DKIM, DMARC setup
- **Return Path / Everest** — inbox placement monitoring (third party)

---

## 📊 Report 5 — Revenue Attribution Report

### What It Measures
Links email campaign performance to pipeline and revenue in Salesforce
CRM — proves the business impact of email marketing.

### Setup Requirements
- UTM parameters on all email links (see UTM to CRM Tracking Guide)
- Google Analytics 4 connected to website
- Salesforce Campaign linked to SFMC Send
- Campaign Influence enabled in Salesforce

### Metrics to Report
| Metric | Source |
|---|---|
| Leads Generated from Email | Salesforce Campaign Members |
| MQLs from Email Campaigns | Salesforce Lead Reports |
| Pipeline Influenced by Email | Salesforce Campaign Influence |
| Closed Won Revenue from Email | Salesforce Opportunity Reports |
| Email Campaign ROI | Revenue ÷ Campaign Cost × 100 |

---

## 📅 Reporting Cadence

| Report | Frequency | Audience |
|---|---|---|
| Campaign Send Summary | After every send | Marketing Team |
| Subject Line Performance | Weekly | Email Marketing Manager |
| Segment Performance | Monthly | Marketing Manager |
| Deliverability Health | Weekly | Marketing Ops / Email Admin |
| Revenue Attribution | Monthly | Marketing Director, Leadership |

---

## ✅ Email Campaign Performance Checklist

- [ ] Delivery rate above 98% for every send
- [ ] Hard bounce rate below 0.5% — suppress immediately if exceeded
- [ ] Spam complaint rate below 0.08%
- [ ] Subject line A/B test running on every major campaign
- [ ] Audience segments reviewed and updated monthly
- [ ] Inactive subscribers (180+ days) moved to re-engagement or suppressed
- [ ] UTM parameters on every link in every email
- [ ] SFMC send linked to Salesforce Campaign for attribution
- [ ] Monthly revenue attribution report shared with leadership

---

## 📝 Notes

> SFMC tracking data is available for 6 months by default. Export and
> archive reports monthly to maintain historical performance data.
> Built from hands-on Salesforce Marketing Cloud and Revenue Operations
> experience managing multi-channel campaigns.
