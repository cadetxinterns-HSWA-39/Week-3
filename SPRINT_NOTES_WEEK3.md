# Sprint Notes — Week 3

## Team

- Odetunde Olumide Temitope — Data Scientist
- Kukoyi Zainab Omotola — Data Analyst
- Nyong Asuabiat — Data Analyst

**Sprint scope:** Data Validation & Consistency Checks, Data Dictionary & Documentation, KPI Framework

## What was completed

- Ran full validation checks across GST calculations, grand-total reconciliation, and payment-to-invoice matching — all passed cleanly on the complete dataset.
- Resolved the `stock_ledger` ADJUSTMENT sign issue by deriving `implied_signed_quantity` from running-balance deltas, flagging all 2,454 affected rows with `adjustment_sign_ambiguous_flag`.
- Wrote the Phase 1 Data Dictionary covering all 12 original files plus the Merged folder's fact and dimension tables.
- Built the 15-KPI framework spanning Inventory, Suppliers, Procurement, Warehouse Efficiency, Sales, and Finance, tying three KPIs directly to known data-quality findings instead of masking them inside formulas.
- Confirmed `sales_transactions.csv` and `purchase_transactions.csv` are staged in the Week 2 folder.

## Decisions made

- Kept the stored and calculated margin values side by side in `product_features.csv` (`calculated_margin_percentage`, `margin_mismatch_flag`) rather than overwriting P002's stored margin — the correction from Week 1 cleaning is already reflected in `products.csv` itself.
- Documented, rather than altered, the `inventory_master.current_stock` scale mismatch and the `branches.avg_monthly_revenue` mismatch, since both trace back to the source systems.
- Standardised the data architecture: fact/dimension tables are canonical, denormalized views are regenerated from them for BI use.

## Closed out

Removed the leftover `ratio` column from the Week 1 cleaned `inventory_master_clean.csv`, bringing it in line with the Merged folder's copy.

## Next steps

Move into Phase 2 (Weeks 4–6): Core Product, Inventory & Warehouse Analytics.
