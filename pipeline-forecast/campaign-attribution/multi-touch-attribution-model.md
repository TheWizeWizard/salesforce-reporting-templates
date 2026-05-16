# Multi-Touch Attribution Model in Salesforce

A framework for attributing revenue and pipeline across multiple marketing
touchpoints — built for Marketing Operations and Revenue Operations teams
using Salesforce CRM.

---

## 🎯 Purpose

Multi-touch attribution answers the key question every marketing leader asks:

> **"Which campaigns and channels actually drove revenue?"**

A proper attribution model allows you to:
- Justify marketing spend with revenue data
- Identify highest performing channels and campaigns
- Optimize budget allocation based on actual impact
- Align Marketing and Sales on what drives pipeline

---

## 📐 Attribution Models Explained

### The 4 Core Models

| Model | How Credit is Distributed | Best Used For |
|---|---|---|
| First Touch | 100% credit to first touchpoint | Brand awareness measurement |
| Last Touch | 100% credit to last touchpoint | Direct response campaigns |
| Linear | Equal credit across all touchpoints | Full funnel visibility |
| W-Shaped | 30% First, 30% MQL, 30% Closed Won, 10% middle touches | B2B Revenue Operations |
W-Shaped Distribution Example (4 touchpoints):
─────────────────────────────────────────────
Touchpoint 1 — Google Ad (First Touch):       30%
Touchpoint 2 — Webinar Registration:          10%
Touchpoint 3 — Demo Request (MQL Created):    30%
Touchpoint 4 — Case Study Email (Closed Won): 30%
─────────────────────────────────────────────
Total Revenue Attributed: $10,000
Google Ad receives:        $3,000
Webinar receives:          $1,000
Demo Request receives:     $3,000
Case Study Email receives: $3,000

---

## 📊 Report 1 — Campaign Influence Report

### What It Measures
Which Salesforce campaigns influenced opportunities — regardless of
whether they were the first or last touch.

### Salesforce Setup
- **Report Type:** Campaign with Influenced Opportunities
- **Filters:**
  - Campaign Start Date = This Year
  - Opportunity Stage = Closed Won
- **Group By:** Campaign Name
- **Summary Fields:**
  - Count of Influenced Opportunities
  - Sum of Influenced Revenue
  - Number of Contacts Reached

### Columns to Include
| Column | Source |
|---|---|
| Campaign Name | Campaign Object |
| Campaign Type | Campaign Object |
| Total Contacts | Campaign Members |
| Influenced Opportunities | Campaign Influence |
| Influenced Revenue | Campaign Influence |
| Campaign Cost | Campaign Object |
| Pipeline ROI | Formula: Influenced Revenue ÷ Campaign Cost |

---

## 📊 Report 2 — First Touch Attribution Report

### What It Measures
Which campaign or channel first introduced a contact to your brand —
measures top of funnel effectiveness.

### Salesforce Setup
- **Custom Field Required:** `Lead Source Detail` (text field on Lead/Contact)
- **Populated By:** UTM Source + Medium passed via form hidden fields
- **Report Type:** Opportunities with Contact Roles
- **Filters:**
  - Opportunity Stage = Closed Won
  - Close Date = This Quarter
- **Group By:** Lead Source (First Touch)
- **Summary Fields:** Count of Opportunities, Sum of Amount

---

## 📊 Report 3 — Revenue by Campaign Type Report

### What It Measures
Which campaign types (email, paid search, events, content) drive the most
pipeline and closed revenue.

### Salesforce Setup
- **Report Type:** Campaigns with Opportunities
- **Filters:**
  - Opportunity Stage = Closed Won
  - Campaign Start Date = This Year
- **Group By:** Campaign Type
- **Summary Fields:** Sum of Opportunity Amount, Count of Opportunities

### Standard Campaign Types to Use
| Type | Examples |
|---|---|
| Paid Search | Google Ads, Bing Ads |
| Paid Social | LinkedIn Ads, Meta Ads |
| Email | Newsletter, Nurture, Promotional |
| Event | Webinar, Conference, Trade Show |
| Content | Ebook, Whitepaper, Case Study |
| Organic | SEO, Direct, Referral |

---

## 📊 Report 4 — Marketing Sourced vs Influenced Pipeline

### What It Measures
The difference between pipeline Marketing directly sourced (first touch)
vs pipeline Marketing influenced (any touch).

### Key Metrics
Marketing Sourced Pipeline   = Opportunities where Lead Source = Marketing Campaign
Marketing Influenced Pipeline = Opportunities with ANY campaign touch before close
Marketing Source Rate (%)    = Marketing Sourced Deals ÷ Total Deals × 100
Marketing Influence Rate (%) = Marketing Influenced Deals ÷ Total Deals × 100

### Benchmark Targets
| Metric | B2B Benchmark |
|---|---|
| Marketing Source Rate | 30% – 45% |
| Marketing Influence Rate | 60% – 80% |
| Pipeline ROI | 5x – 10x campaign spend |

---

## ⚙️ Salesforce Configuration Requirements

### Required Fields
| Field | Object | Type | Purpose |
|---|---|---|---|
| Lead Source | Lead / Contact | Picklist | First touch channel |
| Lead Source Detail | Lead / Contact | Text | UTM source + medium |
| Campaign Member Status | Campaign Member | Picklist | Responded / Sent |
| Primary Campaign Source | Opportunity | Lookup | First touch campaign |

### Required Settings
- ✅ Enable **Customizable Campaign Influence** in Salesforce Setup
- ✅ Set Campaign Influence **time decay window** (recommend 90 days)
- ✅ Enable **Campaign Member** tracking on all campaigns
- ✅ Connect web forms to Salesforce via native connector or Zapier

---

## ✅ Attribution Setup Checklist

- [ ] Customizable Campaign Influence enabled in Salesforce
- [ ] All campaigns created in Salesforce before launch
- [ ] UTM parameters mapped to Lead Source fields via hidden form fields
- [ ] Campaign Member status updated automatically on form submission
- [ ] Primary Campaign Source field populated on all new Opportunities
- [ ] Campaign Influence report built and shared with Marketing leadership
- [ ] Monthly attribution review scheduled with Marketing and Sales

---

## 📝 Notes

> True multi-touch attribution requires clean UTM tracking from the first
> click. See the UTM to CRM Tracking Guide in this repo for the full
> end-to-end setup.
> Built from hands-on Revenue Operations and Salesforce Admin experience
> managing $10M+ revenue portfolios.
>
> 

### Recommended Model for B2B RevOps
**W-Shaped Attribution** — because it values the touchpoints that matter
most in a B2B sales cycle: initial awareness, lead conversion, and deal close.
