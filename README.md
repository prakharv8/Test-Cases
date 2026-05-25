# Yatinidhi Solar — Quotation Generator v1.0
### First Draft · For Internal Review

---

## What's in This Build

**File:** `yatinidhi-quotation-v1.html`
**Type:** Single HTML file — no server, no dependencies, works offline

---

## How to Open & Use

1. **Double-click** `yatinidhi-quotation-v1.html` to open in browser
2. Fill the **Build Quotation** form
3. Click **Generate Quotation** to see the preview
4. Click **Print / Save PDF**
   - Chrome: Set margins to **None**, enable **Background graphics**
   - Edge: Same settings

---

## Features Included

### Form Side
| Feature | Status |
|---|---|
| Customer Name, Mobile, Email, Address, Roof Type | ✅ Editable |
| Employee Name, Designation, Contact | ✅ Editable |
| System Size (1kW – 10kW) click cards | ✅ |
| Custom Rate Override | ✅ |
| System Type (On-Grid / Off-Grid / Hybrid) | ✅ |
| Panel, Inverter, Structure, Wire, ACDB brand dropdowns | ✅ |
| AMC 1yr / 3yr / 5yr toggle | ✅ with live price |
| Battery Backup toggle | ✅ with live price |
| **Roof White Heat-Reflective Paint** | ✅ NEW |
| Extra Civil Work / Extra Cable (at actual) | ✅ |
| Live GROSS TOTAL + Subsidy + NET calculation | ✅ |
| Subsidy toggle (Central CFA + UP State) | ✅ |
| Additional Notes / Remarks | ✅ |

### Roof White Paint — How It Works
- Rate: ₹30/sq.ft (editable)
- **Auto mode:** 100 sq.ft per kW (so 3kW = 300 sq.ft = ₹9,000)
- **Manual mode:** Enter exact sq.ft directly
- Shows live breakup: `X sq.ft × ₹30 = ₹Y`
- Cost flows into add-on total and GROSS TOTAL automatically

### Pricing Calculator
- Add-on prices sum correctly into GROSS TOTAL
- "At Actual" items (civil, cable) show as label only — not counted in total
- Grand Total shown in words (Indian number system: Lakhs/Crore)
- Subsidy rows shown separately and subtracted to NET COST

### Quotation Document
- Company header with branding, GSTN, UPNEDA/MNRE badge
- Customer + Proposal detail boxes side by side
- Full Bill of Materials table (dynamically includes selected add-ons)
- Grand Total row + Subsidy rows + Net Cost row
- GST / Structure / Finance note boxes
- Roof paint breakup note (if selected)
- Government Subsidy table (if subsidy toggle ON)
- Warranty details grid (4 items)
- Payment terms bar (20% / 70% / 10%)
- Bank account details
- Dual signature block (Yatinidhi + Customer)

---

## Draft Issues — Please Review

| # | Item | Action Needed |
|---|---|---|
| 1 | Solar panel warranty years left blank in source PDF | Filled as "25–30 Years" — confirm with OEM |
| 2 | Quotation serial number not in source | Add if needed (e.g. YS/2026/0001) |
| 3 | GSTN on header: 09AABCY0047K1Z7 | Confirm this is current |
| 4 | Roof paint sqft ratio: 100 sqft/kW | Confirm with operations team |
| 5 | AMC pricing: 1yr=₹5k, 3yr=₹12k, 5yr=₹18k | Confirm current rates |
| 6 | Battery add-on: ₹25,000 flat | Confirm or change to "at actual" |

---

## To Embed on Website

**Option A — iframe (simplest)**
```html
<iframe src="yatinidhi-quotation-v1.html" width="100%" height="800px" frameborder="0"></iframe>
```

**Option B — Full page embed**
Upload file to your hosting and link directly as a page.

**Option C — Developer conversion**
Hand the file to a developer to convert to React/Vue if integrating into an existing CMS or website stack.

---

## Next Steps After Review

- [ ] Confirm draft issues above
- [ ] Add quotation serial number logic
- [ ] Add logo image (currently text-based)
- [ ] Test print output on actual printer / PDF
- [ ] Add more panel wattage options if needed
- [ ] Consider adding customer WhatsApp share option
