# Indirect Rate Calculator: Government Contract Cost Model

An Excel model that shows how a U.S. government contractor builds its **fringe, overhead and G&A indirect rates** from the general ledger. It removes **FAR 31.205 unallowable costs**, **monitors actual vs. provisional billing rates** each quarter, prices a **cost-plus-fixed-fee (CPFF) contract**, and projects **forward pricing rates** for the next three years.

> ⚠️ **Sample data.** "Apex Avionics Systems" and every account and amount in this model are fictional. The numbers are made up but realistic, and they exist only to demonstrate the method.

![Rate calculation](screenshots/rate_calc.png)

---

## Why I built this

Government contractors recover overhead and administrative costs through indirect rates. Those rates are billed provisionally during the year, monitored quarterly, and settled at final rates through the **Incurred Cost Proposal (ICP)**. Future contracts are priced with **Forward Pricing Rate Proposals (FPRP)**. DCAA audits both. I built this model to practice the full rate cycle end to end, using the same structure and FAR rules an analyst on a government compliance and finance team works with.

## What's inside

| Sheet | What it does |
|---|---|
| **README** | Purpose, sheet guide, rate structure and color legend |
| **Assumptions** | Provisional billing rates, variance threshold, fee, escalation and business-volume inputs (yellow cells) |
| **GL_Detail** | 116-line sample general ledger (29 accounts × 4 quarters), stored as Excel table `GL` and ready for PivotTables |
| **Rate_Calc** | Quarterly and full-year fringe, overhead and G&A pools, bases and rates, with fringe cascaded onto indirect labor and a zero-balance check |
| **Rate_Monitoring** | Year-to-date actual vs. provisional rates, variance in points and %, review flags, under/over-billing impact and a trend chart |
| **Contract_Pricing** | Cost build-up of a sample CPFF task order at provisional vs. actual rates, showing the final-rate adjustment |
| **Forward_Pricing** | FY2027–FY2029 projected pools, bases and forward pricing rates |
| **Unallowables_ICP** | Unallowable costs by FAR 31.205 reference and claimed pools after exclusion (ICP view) |

## Rate structure

| Rate | Pool | Allocation base |
|---|---|---|
| **Fringe** | Health insurance, payroll taxes, 401(k), PTO, workers' comp | Total labor $ (direct + indirect) |
| **Overhead** | Indirect engineering/manufacturing labor + its fringe, facilities, depreciation, utilities, supplies, engineering IT | Direct labor $ |
| **G&A** | Finance, executive and HR labor + its fringe, legal, insurance, corporate IT, bid & proposal | Total Cost Input (DL + fringe + OH + material + subcontracts + ODC) |

All pools hold **allowable cost only**. Expressly unallowable items (entertainment, alcohol, lobbying, donations, fines, bad debt) are flagged in the ledger and excluded with `SUMIFS` logic.

## Key results (sample data, FY2026)

| Rate | Provisional | Actual | Variance | Status |
|---|---|---|---|---|
| Fringe | 33.0% | 34.0% | +1.0 pts (+3.0%) | Within range |
| Overhead | 76.0% | 80.6% | +4.6 pts (+6.0%) | **Review** |
| G&A | 10.0% | 10.4% | +0.4 pts (+4.4%) | Within range |

- **Under-billing:** actual pools exceeded the amounts billed at provisional rates by about **$856K**. The overhead rate went past the 5% review threshold, so it would be flagged for a provisional rate adjustment.
- **Unallowable costs:** **$199K** was identified across six FAR 31.205 categories and excluded from claimed pools (1.1% of indirect expense).
- **Contract impact:** on the sample CPFF task order, final rates add about **$72K** of cost. The fee stays fixed (FAR 16.306).
- **Forward pricing:** business-volume growth spreads fixed costs over a larger base, so overhead falls from **80.6% to 69.7%** and G&A from **10.4% to 9.3%** by FY2029. Benefit inflation above wage growth pushes fringe up from **34.0% to 37.1%**.

![Rate monitoring](screenshots/rate_monitoring.png)

## How to use it

1. Download `Indirect_Rate_Calculator.xlsx` and open it in Excel.
2. Change any **yellow cell** on the `Assumptions` sheet, such as a provisional rate or a volume growth rate. `Rate_Monitoring`, `Contract_Pricing` and `Forward_Pricing` update automatically.
3. To slice the ledger, click inside `GL_Detail` → **Insert → PivotTable**. Rows: Pool, Account Description · Columns: Quarter · Values: Sum of Amount · Filter: Allowable.

**Color legend:** blue text = input · black = formula · green = link from another sheet · yellow fill = key assumption.

## Skills demonstrated

Indirect rate development · Variance analysis and quarterly trending · Unallowable cost review (FAR 31.205) · Incurred Cost Proposal logic · Forward pricing rates · CPFF contract pricing · Advanced Excel (`SUMIFS`, `INDEX`, structured tables, PivotTable-ready data, charts) · Python (`openpyxl`) for model generation

## More screenshots

| | |
|---|---|
| ![Contract pricing](screenshots/contract_pricing.png) | ![Forward pricing](screenshots/forward_pricing.png) |
| ![Unallowables](screenshots/unallowables_icp.png) | ![Assumptions](screenshots/assumptions.png) |

## Repository layout

```
├── Indirect_Rate_Calculator.xlsx   # the model
├── docs/methodology.md             # step-by-step method and FAR references
├── screenshots/                    # sheet images used in this README
└── src/build_model.py              # Python script that generates the workbook
```

## References

Public at [acquisition.gov](https://www.acquisition.gov/browse/index/far):
- FAR Part 31: Contract Cost Principles and Procedures
- FAR Subpart 42.7: Indirect Cost Rates
- FAR 16.306: Cost-Plus-Fixed-Fee Contracts
- FAR 15.404-4: Profit

---

**Author:** Sai Supraja · Financial Analyst · [LinkedIn](https://www.linkedin.com/in/sai-supraja-kumar)
# Indirect-Rate-Calculator-forward-pricing-style-
