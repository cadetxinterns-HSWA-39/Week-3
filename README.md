# CadetX — Heavy Supplier, Inventory & Warehouse Analytics

## Week 3 submission: Data Validation & Consistency Checks, Data Dictionary & Documentation, KPI Framework

## Team

- Odetunde Olumide Temitope — Data Scientist
- Kukoyi Zainab Omotola — Data Analyst
- Nyong Asuabiat — Data Analyst

## What's in this folder

```
week-03/
├── Data_Dictionary_Phase1.docx
├── Heavy_Suppliers_KPI_Framework.pdf
├── Data_Validation_And_Consistency_Checks_Log.pdf
├── product_features.csv
├── README.md
└── SPRINT_NOTES_WEEK3.md
```

## 1. Data Validation & Consistency Checks

Full detail in `Data_Validation_And_Consistency_Checks_Log.pdf`. Every GST, grand-total, and payment-vs-invoice reconciliation check passed cleanly across every sales order, purchase order, invoice, and payment row.

`stock_ledger` ADJUSTMENT rows had an unreliable quantity sign — 1,222 of 2,454 rows didn't reconcile against the running balance. Fixed by deriving `implied_signed_quantity` from the running-balance delta for every row, and flagging all 2,454 ADJUSTMENT rows with `adjustment_sign_ambiguous_flag`.

Product P002's margin (37.3% stored vs. 60.0% implied by cost and price) was corrected during Week 1 cleaning, and that fix carries through both the cleaned `products.csv` and the Merged folder's copy. `product_features.csv` still holds `calculated_margin_percentage` and `margin_mismatch_flag` alongside it for traceability.

## 2. Data Dictionary & Documentation

Full field-level reference for all 12 original files, plus the fact and dimension tables in the Merged datasets folder, in `Data_Dictionary_Phase1.docx`. Scope covers Data Profiling, Data Cleaning, and Data Integration — Feature Engineering outputs (row-level features, `customer_features.csv`, `product_features.csv`) are documented separately in the Feature Engineering log.

`sales_transactions.csv` and `purchase_transactions.csv` are in the Week 2 folder, available for review alongside their documentation.

## 3. KPI Framework

15 business KPIs defined, prioritised, and mapped to business questions in `Heavy_Suppliers_KPI_Framework.pdf`, covering Inventory, Product Movement, Suppliers, Procurement, Warehouse Efficiency, Sales, and Finance. Three KPIs are tied directly to known data-quality findings from validation — the 417 payments unmatched to a single invoice, the `inventory_master.current_stock` scale mismatch, and the `branches.avg_monthly_revenue` mismatch against actual transactions — rather than hiding them inside a formula.

## 4. Data Architecture

Two integration structures came out of Week 2 — a lean fact/dimension split and a fully denormalized set of joined views. Both are kept, each with a defined role:

- Fact/dimension tables (`sales_fact.csv`, `purchasing_fact.csv`, and the dimension tables) are canonical — the source of truth for KPI calculations, feature engineering, and modelling work in Phase 3.
- Denormalized views are a BI convenience layer, regenerated from the canonical tables for dashboarding and exploratory analysis in Phase 
