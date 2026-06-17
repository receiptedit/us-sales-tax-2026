# 🇺🇸 US State Sales Tax Dataset 2026

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Data: 2026](https://img.shields.io/badge/Data-2026-green.svg)](#)
[![States: 50](https://img.shields.io/badge/States-50-orange.svg)](#)
[![API: live](https://img.shields.io/badge/API-live-success.svg)](https://receiptedit.com/api/sales-tax)

**A free, MIT-licensed dataset of US state sales tax rates and lodging tax rates for 2026.** Statewide rate, average combined rate (state + local), lodging-specific taxes (TOT, occupancy, tourism assessment), grocery taxation rules, top 5 cities, and state nicknames — for all 50 US states.

Compiled and maintained by [ReceiptEdit](https://receiptedit.com), the free receipt generator. **Attribution is required** — please credit the source when you use this data.

---

## 🚀 Quick Start

### Option 1 — Free Public REST API (no auth, CORS-enabled)

```bash
# All 50 states
curl https://receiptedit.com/api/sales-tax

# One state
curl https://receiptedit.com/api/sales-tax/california
```

Returns JSON. CORS-enabled. No auth. No rate limit for normal use. Cache responses for 24+ hours.

Full API docs: **https://receiptedit.com/developers**

### Option 2 — Download the dataset files

| File | Size | Purpose |
|---|---|---|
| [`us-sales-tax-2026.json`](./us-sales-tax-2026.json) | ~29 KB | Full nested dataset with all fields |
| [`us-sales-tax-2026.csv`](./us-sales-tax-2026.csv) | ~6 KB | Flat CSV for spreadsheets / pandas |
| [`us-lodging-taxes-2026.csv`](./us-lodging-taxes-2026.csv) | ~4 KB | Long-format lodging tax breakdown (one row per tax) |
| [`STATES_TABLE.md`](./STATES_TABLE.md) | ~2 KB | Markdown summary table (preview below) |

### Option 3 — Embeddable calculator widget

```html
<iframe
  src="https://receiptedit.com/api/embed/sales-tax/california"
  width="380" height="540"
  style="border:0;max-width:100%"
  loading="lazy"
  title="California Sales Tax Calculator">
</iframe>
```

Swap `california` for any state slug. Mobile-responsive, no JS dependencies on your side.

---

## 📊 What's in the data

Each state has:
- **`name`** — Full state name
- **`code`** — Two-letter US state code
- **`slug`** — URL-safe lowercase name
- **`nickname`** — Official state nickname
- **`salesTaxRate`** — Statewide sales tax (%)
- **`avgCombinedTaxRate`** — Average combined state + local rate (%)
- **`groceryTaxed`** — `true` (taxed) / `false` (exempt) / `"reduced"` (lower rate)
- **`topCities`** — 5 most-populated cities in the state
- **`lodgingTaxes`** — Array of state-level lodging taxes (TOT, occupancy, tourism, etc.) with name + rate

### Example: California

```json
{
  "name": "California",
  "code": "CA",
  "slug": "california",
  "nickname": "Golden State",
  "salesTaxRate": 7.25,
  "avgCombinedTaxRate": 8.85,
  "groceryTaxed": true,
  "topCities": ["Sacramento", "Los Angeles", "San Diego", "San Francisco", "San Jose"],
  "lodgingTaxes": [
    {"name": "Occupancy Room Tax", "amount": 6.61},
    {"name": "Transient Occupancy Tax (TOT)", "amount": 6.73},
    {"name": "Tourism Assessment Fee", "amount": 5.89}
  ]
}
```

---

## 🧑‍💻 Use it from your language

### JavaScript / TypeScript

```js
const res = await fetch('https://receiptedit.com/api/sales-tax/california');
const { state_sales_tax_pct, avg_combined_sales_tax_pct } = await res.json();
console.log(`CA: ${state_sales_tax_pct}% state, ${avg_combined_sales_tax_pct}% combined avg`);
```

### Python (pandas)

```python
import pandas as pd
df = pd.read_csv('https://raw.githubusercontent.com/receiptedit/us-sales-tax-2026/main/us-sales-tax-2026.csv')
print(df.head())
```

### Python (requests)

```python
import requests
data = requests.get('https://receiptedit.com/api/sales-tax/texas').json()
print(f"Texas state rate: {data['state_sales_tax_pct']}%")
```

### Shell

```bash
curl -s https://receiptedit.com/api/sales-tax/florida | jq '.state_sales_tax_pct'
```

---

## 🗺️ All 50 States (preview)

See [`STATES_TABLE.md`](./STATES_TABLE.md) for the full sortable table.

**Notable facts:**
- 🆓 **0% statewide sales tax** (5 states): Alaska, Delaware, Montana, New Hampshire, Oregon
- 📈 **Highest combined avg**: Louisiana & Tennessee (~9.55%)
- 📉 **Lowest combined avg (non-zero)**: Connecticut (6.35%)
- 🥬 **Grocery-exempt states**: 26 states fully exempt groceries from state sales tax
- 🏨 **Highest lodging-tax burden** (state-level): Florida, California, Hawaii

---

## 🎯 Use Cases

This dataset is being used for:

- **Tax-prep blog posts** — embed per-state rates in articles
- **E-commerce checkout estimators** — rough tax calculation before address entry
- **Freelancer & SBDC tools** — practical tax lookup for clients
- **Educational sites** — teaching state tax variation
- **Receipt generators** — itemized tax math on generated receipts
- **Travel planners** — total hotel cost including all lodging taxes
- **Data journalism** — comparative state taxation analysis

---

## 📜 License & Attribution

**MIT License with attribution requirement.**

You may use this data for any purpose — commercial or personal — provided you include a visible attribution link on the page or app where the data appears:

> Data by [ReceiptEdit](https://receiptedit.com)

The API responses already include this in an `attribution` field. The embeddable widget already displays it. For raw data files, please add the link manually.

See [`LICENSE`](./LICENSE) for the full text.

---

## 🔄 Updates

Data is reviewed and updated annually. Subscribe to releases on this repo to be notified when the 2027 dataset ships. State sales tax rates change rarely (most adjustments are at the local level), so this data is stable for most use cases.

**Last reviewed:** 2026-06-17

---

## 🐛 Found an error?

Open an [issue](https://github.com/receiptedit/us-sales-tax-2026/issues) or PR. Cite the state department of revenue source so we can verify and update.

Sources used for compilation:
- [Tax Foundation 2026 State and Local Sales Tax Rates](https://taxfoundation.org/)
- State departments of revenue
- US Census Bureau city population data
- ReceiptEdit internal data on lodging tax rates

---

## 🤝 Related

- **[ReceiptEdit](https://receiptedit.com)** — Free receipt generator (500+ brand templates)
- **[Sales Tax Calculator by State](https://receiptedit.com/sales-tax)** — Interactive calculator for all 50 states
- **[Developer API + Widget Docs](https://receiptedit.com/developers)** — Embed code + REST API reference

---

⭐ Star this repo if the data is useful to you.
