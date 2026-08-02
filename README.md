# Clinic Appointments — Data Cleaning Project

Cleaned a messy 1,000-row clinic appointments dataset (sourced from Kaggle) using
Excel / Google Sheets, producing a 950-row cleaned dataset with standardized
categorical fields and parsed billing information.

## Dataset

| | Raw | Cleaned |
|---|---|---|
| Rows | 1,000 | 950 |
| Format | `messy_clinic_appointments.csv` | `clinic_appointments_cleaned.csv` |

## What Was Fixed

| Issue | Raw example | Cleaned result |
------------------------------------------
| Inconsistent gender encoding | `'F'`, `'1'`, `'female'`, `'Female'`, `'0'`, `'male'` | Standardized to `Male` / `Female` / `Unknown` |
| Currency symbols embedded in amount field | `'£425.80'`, `'Rs85.76'`, `'€203.34'`, `'$84.44'` | Split into a clean numeric billing amount + separate `Currency` column (EUR/USD/GBP/INR) |
| Whitespace / casing inconsistencies | mixed casing in name & department fields | Consistent casing and no leading/trailing whitespace across text columns |
| Duplicate rows | — | Checked, none found |

## Known Limitations (Not Yet Fixed)

Being upfront about these matters more than pretending the file is perfect —
these are genuine gaps worth calling out in an interview or write-up:

- **Name titles only partially removed.** Some patient and doctor names still
  carry prefixes/suffixes like `"Dr."`, `"Mr."`, `"MD"`, `"DDS"` (e.g. `"Dr. Karen
  Miller DDS"`), while others were cleaned. The stripping logic wasn't applied
  consistently across all rows.
- **One missing `Currency` value** was not resolved or flagged.
- **Dates are stored as text, not true date values**, and use a 2-digit year
  format (e.g. `26`, `27`, `28`) that's ambiguous without assuming the century.
- **`appointment_date` and `booking_date` are identical across all 950 rows.**
  This looks like a processing artifact rather than a real pattern — most
  likely one column got copied over the other during cleaning — and it
  removes any ability to analyze booking lead time.
- **Column naming is inconsistent**: `Currency` is capitalized while every
  other column is lowercase (e.g. `patient_name`, `billing_amount`).
- **No currency conversion** — amounts remain in 4 different currencies
  side by side, so aggregate stats (e.g. average billing) aren't meaningful
  without grouping by currency first.

## Repo Structure

```
data/
  raw/messy_clinic_appointments.csv        # original Kaggle source, untouched
  processed/clinic_appointments_cleaned.csv   # cleaned output
README.md
```

## Skills Demonstrated

- Identifying and standardizing inconsistent categorical values (gender)
- Parsing mixed currency-symbol-and-number text into structured numeric data
- Auditing a dataset for residual inconsistencies (titles, date formats,
  column naming) rather than assuming a single cleaning pass is complete
- Documenting known data quality limitations transparently instead of
  hiding them
