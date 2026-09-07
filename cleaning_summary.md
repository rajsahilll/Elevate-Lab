# Task 1 — Data Cleaning & Preprocessing Summary

**Dataset:** Customer Personality Analysis (`marketing_campaign.csv`, Kaggle)
**Original size:** 2,240 rows × 29 columns
**Cleaned size:** 2,236 rows × 31 columns

## Changes made

| # | Step | Detail |
|---|------|--------|
| 1 | **Column headers standardized** | All headers converted to lowercase (`Year_Birth` → `year_birth`), consistent with "clean, uniform" naming. |
| 2 | **Missing values handled** | `income` had 24 missing values (~1%). Filled with the **median income (51,381.5)** rather than dropping rows, since missingness was small and unrelated to other columns. |
| 3 | **Duplicates removed** | Checked for full-row duplicates and duplicate `id`s — **0 found**, so no rows were removed on this basis. (Note: 182 rows matched on all columns *except* `id`; these were kept since a shared `id` is what identifies a true duplicate customer record — different customers can share purchase/demographic values by coincidence.) |
| 4 | **Text values standardized** | `marital_status`: merged non-standard/joke entries — `"Alone"`, `"YOLO"`, `"Absurd"` — into `"Single"` (5 rows affected). `education`: merged `"2n Cycle"` (EU equivalent) into `"Master"` (rows affected: all `2n Cycle` entries). |
| 5 | **Date format standardized** | `dt_customer` parsed from mixed string input into proper datetime, then written back out in a consistent **dd-mm-yyyy** format. |
| 6 | **Data types fixed** | `income` → float; `year_birth` → integer; `dt_customer` → datetime (then formatted string on export). |
| 7 | **Invalid / outlier records removed** | 3 rows had `year_birth` before 1940 (1893, 1899, 1900) — implausible ages (85+) for the 2012–2014 survey period — removed. 1 row had `income` = 666,666 (~13× the median) — treated as a data-entry error — removed. |
| 8 | **New derived columns added** | `age` (2014 − year_birth) and `customer_for_years` (tenure as of end-2014, based on `dt_customer`) — added for easier downstream analysis. |

## Net effect
- Rows: 2,240 → 2,236 (4 rows dropped: 3 implausible birth years + 1 income outlier)
- Columns: 29 → 31 (added `age`, `customer_for_years`)
- 0 missing values remain
- All categorical fields now have clean, consistent categories
- All dates in one consistent format; all numeric fields properly typed
