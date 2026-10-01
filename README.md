# Data Cleaning & Preparation: NYC Airbnb 2019

**Author:** Mohd Aayan

## Dataset
AB_NYC_2019 — 48,895 Airbnb listings in New York City, 16 columns.
Source: Kaggle (New York City Airbnb Open Data)

## Tools
Python, pandas, Jupyter Lab

## Issues found and how they were fixed

| Issue | Found | Action | Reason |
|---|---|---|---|
| Missing `reviews_per_month` | 10,052 | Filled with 0 | Listings with 0 reviews genuinely have 0 reviews/month, not unknown data |
| Missing `last_review` | 10,052 | Left blank | No valid date exists for listings with no reviews |
| Missing `name` | 16 | Filled with "Unknown" | Too few rows to drop; preserves the listing |
| Missing `host_name` | 21 | Filled with "Unknown" | Same reasoning |
| Exact duplicate rows | 0 | None needed | Verified with `.duplicated()` |
| Rows sharing host_id + name | 243 | Investigated, kept | Confirmed these are distinct units (different id, coordinates, reviews) — not duplicates |
| `last_review` stored as text | all | Converted to datetime | Enables date-based analysis |
| Category columns stored as text | all | Converted to category dtype | More memory-efficient, standard practice |
| Extra spaces in `name` | 238 | Stripped | Data consistency |
| `price == 0` | 11 | Removed | Invalid — Airbnb listings can't be free |
| `minimum_nights` > 365 | 14 | Removed | Unrealistic booking requirement |

## Before / After

| Metric | Before | After |
|---|---|---|
| Rows | 48,895 | 48,870 |
| Missing values | 20,141 | 10,043 (last_review only, left intentionally) |
| Duplicates | 0 | 0 |

## Files
- `data/AB_NYC_2019.csv` — original raw dataset
- `data/AB_NYC_2019_cleaned.csv` — cleaned dataset
- `data_cleaning.ipynb` — full cleaning notebook with explanations
