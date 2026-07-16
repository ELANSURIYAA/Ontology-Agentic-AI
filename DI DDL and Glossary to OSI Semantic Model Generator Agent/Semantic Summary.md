# Semantic Summary

## Semantic Overview

### Business Subject Area
Cisco bookings analytics for booked order lines across customers, products, partners, geographies, sales representatives, contracts, and time.

### Data Domain Description
This schema is a dimensional star model centered on **fact_bookings** at the grain of one row per booked order line. It supports sales and revenue-oriented analysis using conformed dimensions for date, customer, product, partner, geography, sales representative, and contract context.

### Business Value Proposition
The model enables trusted analysis of booking performance, customer demand, product mix, channel effectiveness, regional performance, contract value, and renewal behavior. It provides a business-centric foundation for semantic modeling, reporting, KPI calculation, ontology generation, and downstream AI-driven metadata experiences.

### Business Capabilities Enabled
- Analyze bookings by fiscal and calendar periods
- Evaluate customer, segment, industry, and account tier performance
- Measure product and technology domain contribution
- Assess partner channel and route-to-market effectiveness
- Compare geographic performance by region, theater, and country
- Track sales representative performance and coverage
- Analyze contract mix, term, renewal behavior, ACV, and TCV

### Three Business Questions
1. What is total booking amount by fiscal quarter, region, and product family?
2. How do renewal bookings and ACV vary by contract type and customer segment?
3. Which partners and sales teams generate the highest TCV across technology domains?

---

## Semantic Metrics Report

### Overall Metrics
| Metric | Value |
|---|---:|
| Total Tables | 8 |
| Total Columns | 53 |
| Total Relationships | 7 |
| Total Domains | 8 |
| Total Measures | 6 |
| Total Glossary Terms | 55 |
| Mapped Terms | 53 |
| Glossary Coverage Percentage | 96.36% |

### Schema Statistics
| Category | Count |
|---|---:|
| Fact Tables | 1 |
| Dimension Tables | 7 |
| Lookup Tables | 0 |
| Bridge Tables | 0 |
| Composite Keys | 0 |
| Primary Keys | 8 |
| Foreign Keys | 7 |

### Per-Domain Metrics
| Domain Name | Entity Count | Attribute Count | Measure Count | Glossary Coverage % | Domain Status |
|---|---:|---:|---:|---:|---|
| Bookings | 1 | 18 | 6 | 100.00% | Healthy |
| Date | 1 | 7 | 0 | 70.00% | Thin |
| Customer | 1 | 8 | 0 | 100.00% | Thin |
| Product | 1 | 7 | 0 | 100.00% | Thin |
| Partner | 1 | 6 | 0 | 100.00% | Thin |
| Geography | 1 | 4 | 0 | 75.00% | Thin |
| Sales | 1 | 6 | 0 | 100.00% | Thin |
| Contract | 1 | 5 | 0 | 100.00% | Thin |

### Glossary Coverage Statistics
- Total glossary attributes identified: 55
- DDL columns directly present: 53
- Glossary-only terms not found in DDL: 2
  - `day_of_week`
  - `month_number`
- Name mismatch warnings:
  - Glossary uses `geo_key` while DDL uses `geography_key`
  - Glossary uses `geo_key` in `fact_bookings` while DDL uses `geography_key`
- Ambiguous mappings: 0
- Duplicate glossary terms: 0 detected in source text
- Duplicate table definitions: 0

---

## Semantic Quality & Reasoning Report

### Validation Warnings
- No duplicate table definitions detected.
- No duplicate glossary terms detected in the supplied glossary text.
- No invalid column definitions detected in the DDL.
- No missing primary keys detected.
- No broken foreign keys detected; all 7 foreign keys point to existing primary keys.
- Glossary-to-DDL naming inconsistency detected for geography foreign key naming (`geo_key` vs `geography_key`).
- Two glossary attributes are not implemented in the supplied DDL: `day_of_week`, `month_number`.

### Design Observations
| Observation | Result |
|---|---|
| Deepest Relationship Chain | 2 levels (`fact_bookings` -> any dimension) |
| Orphan Tables | 0 |
| Many-to-Many Relationships | 0 explicit |
| Nullable Column Percentage | 40 / 53 = 75.47% |
| Degenerate Dimensions | `order_number`, `order_line_number`, `booking_type` |
| Star Schema Pattern | Confirmed |

### Glossary Health
| Metric | Result |
|---|---|
| Unmapped Glossary Terms | 2 |
| Ambiguous Mappings | 0 |
| Domain Coverage | Strong across all physical tables |
| Coverage Gaps | Date detail attributes and geography key naming alignment |

### Strong Semantic Domains
- **Bookings**: Strong central fact with explicit measures and complete dimensional context.
- **Customer**: Well-described business entity with segment and industry analysis attributes.
- **Product**: Strong descriptive support for portfolio and offer analysis.

### Weak Semantic Domains
- **Date**: Semantically useful but under-modeled compared with glossary; missing `day_of_week` and `month_number`.
- **Geography**: Small but valid domain; naming inconsistency reduces semantic clarity.

### Sparse Modeling
- No severe sparsity in the fact model.
- Several dimensions are intentionally thin and serve descriptive roles only.

### Broken Lineage
- No broken referential lineage in the DDL.
- Potential metadata lineage issue due to geography key naming inconsistency between glossary and DDL.

### Suggested Join Paths
- Bookings to Customer: `fact_bookings.customer_key = dim_customer.customer_key`
- Bookings to Product: `fact_bookings.product_key = dim_product.product_key`
- Bookings to Date: `fact_bookings.date_key = dim_date.date_key`
- Bookings to Partner: `fact_bookings.partner_key = dim_partner.partner_key`
- Bookings to Geography: `fact_bookings.geography_key = dim_geography.geography_key`
- Bookings to Sales Representative: `fact_bookings.sales_rep_key = dim_sales_rep.sales_rep_key`
- Bookings to Contract: `fact_bookings.contract_key = dim_contract.contract_key`

### Data Quality Watch-Outs
- `is_renewal` is modeled as integer rather than explicit boolean/flag domain.
- `discount_pct` should be validated for acceptable percentage ranges.
- `unit_list_price_usd` is a rate and should not be summed without business rules.
- `booking_amount_usd`, `acv_usd`, and `tcv_usd` may require reconciliation rules.
- Surrogate keys are primary identifiers in joins; natural keys should be governed for uniqueness externally.
- High nullable percentage suggests optional descriptive attributes that may affect downstream completeness.

### Recommendations
1. Align glossary and DDL naming for geography key to eliminate mapping ambiguity.
2. Extend `dim_date` to include `day_of_week` and `month_number` if required by reporting.
3. Define semantic aggregation rules explicitly for non-additive measures like `unit_list_price_usd` and semi-analytic metrics like `discount_pct`.
4. Add business rule documentation for `is_renewal`, `booking_type`, ACV, and TCV reconciliation.
5. Consider domain stewardship ownership for each dimension to strengthen metadata governance.
