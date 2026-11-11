# HELIXOR MEDTECH — European Medical Device Distribution Analysis

**Python · Pandas · Data Quality · Delivery KPI Analysis · Operations Reporting**

> **Portfolio case study:** This project analyzes a simulated medical-device distribution dataset. HELIXOR MEDTECH is a fictional business scenario, not a live client engagement. Calculated KPIs are provisional until the documented data-quality and eligibility questions are resolved.

## Business problem

A European medical-device distributor needs to assess shipment data quality and understand delivery reliability across warehouses, operational routes, and order months.

This project addresses four questions:

1. Which records require cleaning, investigation, or operational confirmation?
2. What proportion of eligible completed shipments arrived on time?
3. How much of the eligible ordered quantity is recorded as delivered?
4. Where and when are delivery performance gaps most apparent?

## Dataset and approach

- **Source size:** 1,000 shipment records, 21 original fields
- **Period:** April–September 2026
- **Unit of analysis:** Shipment record; repeated sales orders may be legitimate
- **Workflow:** Audit → preserve raw data → safe cleaning → validation → derived fields → KPI eligibility → warehouse/route analysis → order-month pivot → management reporting
- **Data handling:** Original input preserved as `df_raw`; safe transformations and analysis-ready fields held in `df_clean`. Unknown values are not silently replaced with zero.

## Preliminary KPI results

| Metric | Provisional result | Calculation base |
|---|---:|---|
| On-Time Delivery (OTD) | **23.11%** | 110 on time / 476 eligible shipment records |
| Late deliveries | **366** | 366 / 476 OTD-eligible records |
| Quantity Fill Rate | **97.48%** | 108,864 units delivered / 111,679 ordered |
| Quantity difference | **2,815 units (2.52%)** | Arithmetic difference on 487 eligible records |
| Lowest named-warehouse OTD | **Madrid: 9.09%** | 5 on time / 55 eligible records |
| Monthly pivot coverage | **474 records** | 476 OTD records less 2 ambiguous order months |

**Important:** OTD and Quantity Fill Rate use **different eligibility rules and denominators**. The 2,815-unit difference does not establish physical losses or inventory shrinkage.

## Main findings

- All six named warehouses recorded provisional OTD rates below 30%.
- Madrid had the lowest named-warehouse OTD (9.09%), while Milan had the largest **count** of late shipments (68).
- Route `HAM-DK-02` showed the lowest route-level OTD (12.24%). Route codes should not be interpreted as verified physical origin/destination pairs.
- In Madrid, the April and August **order-month cohorts** had 0/7 and 0/9 on-time deliveries, respectively. These figures do **not** mean that no shipments occurred.
- Shipment timing and unit fulfillment should be investigated separately; neither metric establishes a root cause.

## Data quality and reporting limitations

Issues requiring confirmation include 10 exact duplicate pairs, invalid/ambiguous dates, missing or non-numeric quantities, unexpected status labels, ambiguous warehouse names, and business-rule exceptions.

For provisional OTD, both copies of each exact-duplicate pair and delivery-before-dispatch anomalies were excluded from the eligible sample. Provisional Fill Rate also applies separate quantity eligibility filters. These choices are **not** final approved company rules.

**Work still pending:** Validate grouped Quantity Fill Rate and damaged-unit comparisons by warehouse/route; rerun the notebook from the original import through the final outputs; review the dataset for publication rights and sensitive fields before making this repository public.

## Tools and analytical methods

- **Python / Pandas:** data profiling, safe type conversion, cleaning, derived features, filtering, `groupby`, `pivot_table`
- **Google Colab / Jupyter:** reproducible notebook workflow
- **Google Sheets / Google Docs:** source data review, technical audit, and business communication

## Supporting work

- [Analysis notebook (Google Colab)](https://colab.research.google.com/drive/1MDC0FdMTQ02K-_hl6eN-u_fJPI2TlXV6)
- [Full technical report (Google Docs)](https://docs.google.com/document/d/1qdxnN2AF81fq0EMg8DhNVdsCub70UntLqm5gTTjE4y0/edit)
- [Client-ready management report (Google Docs)](https://docs.google.com/document/d/1OLO-gvVqANnnAbInU6x6Hpj2X5kCxnUwjwy6gwGVqtk/edit)

> External documents may require separate sharing permissions. Portable notebook and approved report exports will be organized in the repository after final review.

## Project completion checklist

- [x] Initial data-quality audit and proposed cleaning rules
- [x] Safe cleaning and validation
- [x] Derived quantity shortfall and delivery delay fields
- [x] Provisional OTD and Quantity Fill Rate calculations
- [x] Warehouse and route OTD analysis
- [x] Order-month OTD and shipment-count pivots
- [x] Technical report and draft client-ready management report
- [ ] Grouped Fill Rate and damaged-unit analyses by warehouse/route
- [ ] Top-to-bottom notebook reproducibility check
- [ ] Upload reviewed notebook and supporting artifacts
- [ ] Confirm publication rights and finalize public portfolio version

## Author

**Thoriq Satrio Ambodo**  
Industrial Engineering student · Data & Operations Analytics portfolio

*This is an independent analytical exercise based on a simulated dataset. It should not be presented as audited operational performance for a real company.*
