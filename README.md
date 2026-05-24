# NPS Vatsalya Report Generator

A free, single-page web tool for generating personalised **NPS Vatsalya** financial projection reports.

Built for NPS advisors and agents to quickly create client-ready reports showing corpus at 18, wealth at retirement, and monthly pension projections.

---

## 🔗 Live Tool

**[Open Generator →](https://prakharv8.github.io/Test-Cases/)**

---

## 📋 Features

- **Child & Returns** — enter child's name, current age, expected return %, annuity rate, and retirement age
- **Contribution before 18** — choose SIP Only / One Time / Both, with Monthly or Annual SIP option
- **Additional SIP after 18** — optional post-18 contribution
- **Live chart** — year-by-year wealth growth (Total Invested vs Wealth via Compounding)
- **Live report card** — updates as you type, with logos of NPS Vatsalya, PFRDA, NPS Trust
- **PDF download** — one-click download of the report card as a PDF
- **Works on all devices** — phone, tablet, desktop

---

## 📐 Calculation Method

| Formula | Used For |
|---|---|
| `M × [((1+r)^n − 1) / r] × (1+r)` | Monthly SIP future value |
| `A × [((1+R)^N − 1) / R] × (1+R)` | Annual SIP future value |
| `P × (1 + R)^years` | Lump sum compound growth |
| `Corpus × annuity% / 12` | Monthly pension |

Where `r = annual_rate / 12 / 100`, `n = months`, `R = annual_rate / 100`, `N = years`

**Verified against:**
- npsvatsalya.com — ₹10,000/yr @ 10% → ₹5L at 18 ✅
- Business Standard — ₹10,000/yr @ 10% → ₹2.75 Cr at 60 ✅

---

## 📁 Files

| File | Purpose |
|---|---|
| `index.html` | Complete self-contained tool (HTML + CSS + JS + logos) |
| `README.md` | This file |

---

## 🚀 How to Use

1. Open the link above on any device
2. Fill in child details and contribution amounts
3. Results update live as you type
4. Click **Download PDF Report** to save the report card

---

## 🛠 Tech Stack

- Pure HTML, CSS, JavaScript — no framework
- [Chart.js 4.4.0](https://cdn.jsdelivr.net/npm/chart.js@4.4.0/) — wealth growth chart
- [html2canvas 1.4.1](https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/) — PDF capture
- [jsPDF 2.5.1](https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/) — PDF generation
- [DM Sans](https://fonts.google.com/specimen/DM+Sans) — Google Fonts

---

## ⚠️ Disclaimer

Projections are illustrative only. Actual returns may vary. NPS is market-linked and subject to risk. Past performance is not indicative of future results.

---

*For internal use by NPS advisors. Powered by Compounding.*
