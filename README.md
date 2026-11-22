# MiPayroll
Tax Information For MiPayroll (c) Software.

## JSON Format (`SchemaVersion` 1.0 — Pure Integer Self-Documenting Format)
To completely eliminate floating-point rounding errors in JSON / JavaScript tools and make every field's unit obvious right where you edit it, **`tax_info.json`** stores **every monetary amount and every tax rate as an exact whole integer** (zero decimal points anywhere in numeric fields) using explicit field-name suffixes:

### 1. Dollar / Currency Amounts — `*_cents` (`AmountScale: 100`)
Every monetary field ends with **`_cents`** and is stored as **whole integer cents** (`dollars × 100`, divide by `100` to get dollars):
- `"BracketMin_cents": 78800000` → **$788,000.00** (788 thousand dollars)
- `"BracketMax_cents": null` → **No ceiling**
- `"BaseTax_cents": 20658350` → **$206,583.50**
- `"SocialSecurityWageCap_cents": 18450000` → **$184,500.00**
- `"FutaWageCap_cents": 700000` → **$7,000.00**
- `"WageCap_cents": 9534900` → **$95,349.00** (`null` = no cap)

### 2. Tax Rates — `*_pctX1000` (`RateScale: 100000`)
Every percentage rate field ends with **`_pctX1000`** and is stored as **whole integer thousandths of a percent** (`percent × 1000`, so `1000` = `1%`; divide by `1,000` for `%` or by `100,000` for the decimal multiplier):
- `"Rate_pctX1000": 37000` → **37%** (`0.37`)
- `"SocialSecurityEmployeeRate_pctX1000": 6200` → **6.2%** (`0.062`)
- `"MedicareEmployeeRate_pctX1000": 1450` → **1.45%** (`0.0145`)
- `"AdditionalMedicareRate_pctX1000": 900` → **0.9%** (`0.009`)
- `"FutaRate_pctX1000": 600` → **0.6%** (`0.006`)
- `"EmployeeRate_pctX1000": 432` → **0.432%** (`0.00432`, e.g. NY-PFL)
- `"Rate_pctX1000": 5525` → **5.525%** (`0.05525`, e.g. NJ bracket)
- `"Rate_pctX1000": 3876` → **3.876%** (`0.03876`, e.g. NYC local tax)

### 3. Versioning (`DataVersion`)
The filename remains stable as `tax_info.json` so MiPayroll always fetches the same URL. Every update bumps `"DataVersion"` using `YYYY.MM.DD.NN` (for example, `"2026.11.21.02"` → `"2026.11.26.01"`), allowing MiPayroll to detect updates and preview all changes before applying them.

## Disclaimer
The tax tables, brackets, and rates in this repository are compiled for informational and software configuration purposes only and **do not constitute tax, legal, or accounting advice**. 

While reasonable efforts are made to keep these files accurate, federal and state tax laws change frequently. **All data is provided "AS IS" without warranty of any kind.** 
Always verify rates against official IRS and state revenue agency publications before processing payroll or filing taxes. See the [LICENSE](LICENSE) file for full terms.
