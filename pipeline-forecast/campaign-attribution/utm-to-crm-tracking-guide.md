# UTM to CRM Tracking Guide

A complete end-to-end guide for passing UTM parameter data cleanly into
Salesforce — ensuring every lead is tracked from first click to closed revenue.

---

## 🎯 Purpose

UTM to CRM tracking closes the loop between marketing spend and revenue.
Without it:
- You know clicks happened but not which ones became customers
- Campaign ROI is guesswork
- Marketing and Sales argue about lead quality with no data

With it:
- Every lead carries its original source through the entire funnel
- Closed Won revenue is attributed back to the exact campaign and channel
- Budget decisions are based on actual revenue, not vanity metrics

---

## 🔁 How UTM to CRM Tracking Works
User clicks ad
↓
Landing page URL captures UTM parameters
↓
Hidden form fields read UTM values from URL
↓
Form submission creates Lead in Salesforce
↓
UTM values stored in Lead Source fields
↓
Lead converts to Contact + Opportunity
↓
UTM data carried to Opportunity via field mapping
↓
Closed Won revenue attributed to original campaign
---

## 📐 Step 1 — UTM Parameter Setup

### Standard UTM Parameters to Always Use
| Parameter | Purpose | Example Value |
|---|---|---|
| utm_source | Traffic origin | `google` `linkedin` `newsletter` |
| utm_medium | Marketing channel | `cpc` `email` `paid-social` |
| utm_campaign | Campaign name | `2025-q2-product-launch` |
| utm_content | Ad or link variant | `banner-blue` `cta-button-a` |
| utm_term | Paid search keyword | `salesforce+crm+consultant` |

### Example Tagged URL
https://yourwebsite.com/demo?utm_source=linkedin&utm_medium=paid-social&utm_campaign=2025-q2-demo-request&utm_content=banner-v1
---

## ⚙️ Step 2 — Salesforce Field Setup

### Custom Fields to Create on Lead Object
| Field Label | API Name | Field Type |
|---|---|---|
| UTM Source | UTM_Source__c | Text (255) |
| UTM Medium | UTM_Medium__c | Text (255) |
| UTM Campaign | UTM_Campaign__c | Text (255) |
| UTM Content | UTM_Content__c | Text (255) |
| UTM Term | UTM_Term__c | Text (255) |
| Landing Page URL | Landing_Page_URL__c | URL |

### Custom Fields to Create on Contact & Opportunity
Mirror the same fields on Contact and Opportunity objects so UTM data
carries through when a Lead converts.

---

## 🌐 Step 3 — Hidden Form Fields Setup

### How It Works
Add hidden fields to your web forms that automatically capture UTM values
from the page URL and pass them to Salesforce on submission.

### JavaScript to Add to Your Landing Pages
```javascript
// Add this script to capture UTMs and store in sessionStorage
function getUTMParams() {
  const params = new URLSearchParams(window.location.search);
  const utms = [
    'utm_source',
    'utm_medium',
    'utm_campaign',
    'utm_content',
    'utm_term'
  ];
  utms.forEach(param => {
    if (params.get(param)) {
      sessionStorage.setItem(param, params.get(param));
    }
  });
}

// Populate hidden form fields from sessionStorage
function populateHiddenFields() {
  const utms = [
    'utm_source',
    'utm_medium',
    'utm_campaign',
    'utm_content',
    'utm_term'
  ];
  utms.forEach(param => {
    const field = document.querySelector(`input[name="${param}"]`);
    if (field && sessionStorage.getItem(param)) {
      field.value = sessionStorage.getItem(param);
    }
  });
}

getUTMParams();
document.addEventListener('DOMContentLoaded', populateHiddenFields);
```

### Hidden Form Fields to Add (HTML)
```html
<input type="hidden" name="utm_source" value="" />
<input type="hidden" name="utm_medium" value="" />
<input type="hidden" name="utm_campaign" value="" />
<input type="hidden" name="utm_content" value="" />
<input type="hidden" name="utm_term" value="" />
```

---

## 🔄 Step 4 — Lead Conversion Field Mapping

### Salesforce Setup
When a Lead converts to a Contact and Opportunity, UTM fields must be
mapped so data is not lost.

1. Go to **Setup → Lead Fields**
2. Click **"Map Lead Fields"**
3. Map each UTM field on Lead to the corresponding field on Contact
   and Opportunity

| Lead Field | Maps To (Contact) | Maps To (Opportunity) |
|---|---|---|
| UTM_Source__c | UTM_Source__c | UTM_Source__c |
| UTM_Medium__c | UTM_Medium__c | UTM_Medium__c |
| UTM_Campaign__c | UTM_Campaign__c | UTM_Campaign__c |
| UTM_Content__c | UTM_Content__c | UTM_Content__c |
| UTM_Term__c | UTM_Term__c | UTM_Term__c |

---

## 📊 Step 5 — Salesforce Reports to Build

### Report 1 — Leads by UTM Source
- **Report Type:** Leads
- **Group By:** UTM Source
- **Summary:** Count of Leads, Count Converted

### Report 2 — Pipeline by UTM Campaign
- **Report Type:** Opportunities
- **Filters:** Stage ≠ Closed Lost
- **Group By:** UTM Campaign
- **Summary:** Count of Opportunities, Sum of Amount

### Report 3 — Closed Won Revenue by UTM Medium
- **Report Type:** Opportunities
- **Filters:** Stage = Closed Won
- **Group By:** UTM Medium
- **Summary:** Sum of Amount, Count of Opportunities

---

## ✅ UTM to CRM Setup Checklist

- [ ] UTM custom fields created on Lead, Contact, and Opportunity
- [ ] Hidden form fields added to all landing pages
- [ ] JavaScript UTM capture script installed on all landing pages
- [ ] Lead field mapping configured in Salesforce Setup
- [ ] Test submission completed — verify UTM data appears in Lead record
- [ ] Lead conversion tested — verify UTM data carries to Opportunity
- [ ] Salesforce reports built for UTM source, medium, and campaign
- [ ] UTM naming convention documented and shared with Marketing team

---

## 🚫 Common Mistakes to Avoid

| Mistake | Impact | Fix |
|---|---|---|
| Not using UTMs on all paid campaigns | Blind spots in attribution | Enforce UTM policy across all channels |
| UTM values with spaces or caps | Data fragmentation in reports | Always lowercase, use hyphens |
| Not mapping fields on Lead conversion | UTM data lost at conversion | Set up Lead Field Mapping in Salesforce |
| Using the same UTM for multiple ads | Can't differentiate ad performance | Use utm_content to separate variants |
| Overwriting first touch with last touch | Loses awareness channel data | Store first touch separately |

---

## 📝 Notes

> For platforms that strip UTM parameters (e.g. some email clients),
> use redirect URLs or link shorteners that preserve UTM data.
> Built from hands-on Revenue Operations and Salesforce Admin experience
> managing multi-channel attribution across $10M+ revenue portfolios.
