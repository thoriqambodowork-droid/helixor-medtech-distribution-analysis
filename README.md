# HELIXOR MEDTECH — European Medical Device Distribution Analysis

**Python · Pandas · Data Quality · Delivery KPI Analysis · Operations Reporting**

> **Portfolio case study:** This project analyzes a simulated medical-device distribution dataset. HELIXOR MEDTECH is a fictional business scenario, not a live client engagement. Calculated KPIs are provisional until the documented data-quality and eligibility questions are resolved.

## Business problem

A European medical-device distributor needs to assess shipment data quality and understand delivery reliability across warehouses, operational routes, and order months.

This project addresses four questions:

1. Which records require cleaning, investigation, or operational confirmation?
2. What proportion of eligible completed shipments arrived on time?
3. How much of the eligible ordered quantity is recorded as delivered?
4. Which warehouses and routes show the lowest fulfillment rates or highest recorded damage, and where do timeliness gaps appear?

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
| Lowest named-warehouse Fill Rate | **Lyon: 95.35%** | 15,254 / 15,998 units |
| Lowest route Fill Rate | **FRA-SE-03: 95.78%** | 13,705 / 14,309 units |
| Recorded damaged units | **1,001** | 487 quantity-eligible records; 108,864 delivered units |
| Recorded Damage Rate | **0.92%** | 1,001 damaged / 108,864 delivered units |
| Highest named-warehouse Damage Rate | **Lyon: 1.00%** | 153 / 15,254 delivered units |
| Highest route Damage Rate | **HAM-DE-03: 1.26%** | 132 / 10,488 delivered units |
| Monthly pivot coverage | **474 records** | 476 OTD records less 2 ambiguous order months |

**Important:** OTD and Quantity Fill Rate use **different eligibility rules and denominators**. The 2,815-unit difference does not establish physical losses or inventory shrinkage. Damaged units were aggregated only on the 487 quantity-eligible records, **not all 1,000 source rows**. Damage Rate means recorded damaged units divided by recorded delivered units.

## Main findings

- All six named warehouses recorded provisional OTD rates below 30%.
- Madrid had the lowest named-warehouse OTD (9.09%), while Milan had the largest **count** of late shipments (68).
- Route `HAM-DK-02` showed the lowest route-level OTD (12.24%). Route codes should not be interpreted as verified physical origin/destination pairs.
- In Madrid, the April and August **order-month cohorts** had 0/7 and 0/9 on-time deliveries, respectively. These figures do **not** mean that no shipments occurred.
- Lyon had the lowest named-warehouse Quantity Fill Rate (95.35%), while `FRA-SE-03` had the lowest route-level rate (95.78%).
- Milan recorded the largest absolute damaged-unit count by warehouse (197); Lyon had the highest named-warehouse damage proportion (1.00%). At route level, `HAM-DE-03` had both the most damaged units (132) and the highest Damage Rate (1.26%).
- A route identifier can appear with multiple warehouses in this dataset. It does not prove which warehouse caused damage, and damaged-unit totals do not establish physical loss or root cause.
- Shipment timing and unit fulfillment should be investigated separately; neither metric establishes a root cause.

## Data quality and reporting limitations

Issues requiring confirmation include 10 exact duplicate pairs, invalid/ambiguous dates, missing or non-numeric quantities, unexpected status labels, ambiguous warehouse names, and business-rule exceptions.

The audit identified 10 exact duplicate pairs (20 source rows involved), while 10 duplicate-flagged rows were excluded in the provisional OTD candidate population. This is not evidence that all source duplicates were included in the eligible population. Provisional Fill Rate applies separate quantity eligibility filters. These choices are **not** final approved company rules.

**Reproducibility status:** The downloaded notebook was inspected: it had no saved error outputs and contained the expected provisional KPI values. The GitHub copy removes the superseded 23.00% OTD calculation and cached outputs, and adds assertions for the training dataset. The user reports a successful top-to-bottom execution of the cleaned copy in Google Colab without errors. This execution has not been independently witnessed or reproduced by this repository's CI. Google authentication and access to the source Sheet are required.

**Work still pending:** Review publication rights and sensitive fields, test the notebook with the intended access model, and complete a final public-portfolio review before changing repository visibility. Grouped Fill Rate and damage comparisons have been calculated but remain provisional.

## Tools and analytical methods

- **Python / Pandas:** data profiling, safe type conversion, cleaning, derived features, filtering, `groupby`, `pivot_table`
- **Google Colab / Jupyter:** reproducible notebook workflow
- **Google Sheets / Google Docs:** source data review, technical audit, and business communication

## Supporting work

- [Portfolio notebook (GitHub)](analysis/HELIXOR_MEDTECH_Analysis.ipynb) — cleaned source, without cached outputs
- [Original working notebook (Google Colab)](https://colab.research.google.com/drive/1MDC0FdMTQ02K-_hl6eN-u_fJPI2TlXV6)
- [Technical Report (PDF)](reports/HELIXOR%20MEDTECH.pdf)
- [Full technical report (editable Google Docs)](https://docs.google.com/document/d/1qdxnN2AF81fq0EMg8DhNVdsCub70UntLqm5gTTjE4y0/edit)
- [Client-Ready Operations Report (PDF)](reports/HELIXOR%20MEDTECH%20%E2%80%94%20Client-Ready%20Operations%20Performance%20Report.pdf)
- [Client-ready management report (editable Google Docs)](https://docs.google.com/document/d/1OLO-gvVqANnnAbInU6x6Hpj2X5kCxnUwjwy6gwGVqtk/edit)

> Portable notebook and both report PDF exports are now stored in this repository. Editable Google Docs may require separate sharing permissions.

## Project completion checklist

- [x] Initial data-quality audit and proposed cleaning rules
- [x] Safe cleaning and validation
- [x] Derived quantity shortfall and delivery delay fields
- [x] Provisional OTD and Quantity Fill Rate calculations
- [x] Warehouse and route OTD analysis
- [x] Order-month OTD and shipment-count pivots
- [x] Technical report and updated client-ready management report
- [x] Grouped Fill Rate and damaged-unit analyses by warehouse/route (provisional)
- [x] Top-to-bottom clean notebook run — user-reported successful in Google Colab, without errors
- [x] Upload cleaned notebook (`analysis/HELIXOR_MEDTECH_Analysis.ipynb`)
- [x] Upload Technical and Client-Ready PDF reports
- [ ] Confirm publication rights and finalize public portfolio version

## Author

**Thoriq Satrio Ambodo**  
Industrial Engineering student · Data & Operations Analytics portfolio

*This is an independent analytical exercise based on a simulated dataset. It should not be presented as audited operational performance for a real company.*
