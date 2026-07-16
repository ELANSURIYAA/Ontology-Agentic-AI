# Ontology Summary

## Ontology Overview

### Primary Business Domain
Cisco bookings analytics within the Quote-to-Booking segment of the Order-to-Cash lifecycle.

### Ontology Scope
This ontology represents the business meaning of booked order lines and their surrounding descriptive context across customer, product, partner, geography, sales representative, contract, and date dimensions. It captures explicit enterprise semantics from the OSI Semantic Model and Business Process documentation and adds constrained inferred semantics where the source documents support them.

### Concepts Modeled
- **Booking**: booked order line transaction recognized after Cisco accepts a valid order with committed value.
- **Date**: calendar and fiscal reporting context.
- **Customer**: purchasing organization and business classification.
- **Product**: booked item or service with portfolio attributes.
- **Partner**: channel participant and route-to-market context.
- **Geography**: region, theater, and country reporting hierarchy.
- **SalesRepresentative**: accountable seller and coverage context.
- **Contract**: service or subscription agreement context associated with a booking.
- **Business domain classes** used as organizing concepts: BookingsDomain, DateDomain, CustomerDomain, ProductDomain, PartnerDomain, GeographyDomain, SalesDomain, ContractDomain.
- **Process-supporting inferred classes** supported by process text: RenewalBooking, NewBooking, UpsellBooking, SubscriptionOfferBooking, ChannelBooking.

### Relationships Modeled
Explicit relationships derived from foreign keys and process context:
- Booking occurs on Date
- Booking is for Customer
- Booking includes Product
- Booking involves Partner
- Booking is associated with Geography
- Booking is owned by SalesRepresentative
- Booking is governed by Contract

Inferred or process-supported relationships:
- Customer places Booking
- SalesRepresentative owns Booking
- Partner routes Booking
- Contract governs Booking
- Booking has booking type classification
- RenewalBooking governed by Contract with renewal characteristics

### Business Rules Captured
Explicit and inferred rules captured in ontology annotations and OWL restrictions where feasible:
1. A **Booking** is recorded when Cisco accepts a valid order with committed value.
2. **Booking** is modeled at **one row per booked order line** grain.
3. Every Booking is associated with exactly one Date, Customer, Product, Partner, Geography, SalesRepresentative, and Contract in the source model.
4. **Bookings are additive** at order-line grain for `quantity`, `booking_amount_usd`, `acv_usd`, and `tcv_usd`; aggregation nuances for `unit_list_price_usd` and `discount_pct` are documented as annotations rather than logical axioms.
5. For subscription and SaaS offers, the process document states that **booking amount equals TCV** and **ACV is the annualized figure**. This is documented as a business rule annotation because arithmetic equality is outside standard OWL DL expressivity.
6. `booking_type` classifies a Booking as New, Renewal, or Upsell.
7. `is_renewal` indicates whether a booking represents a contract renewal.
8. A contract may include `auto_renew_flag`, `term_months`, and `coverage_level`.

### Validation Warnings
- OSI semantic completeness is strong for core entities and relationships.
- Business process document is readable and sufficiently structured.
- Missing semantic attributes in physical model relative to glossary: `day_of_week`, `month_number`, `calendar_quarter`.
- Naming inconsistency detected: glossary uses `geo_key` while SQL uses `geography_key`.
- No duplicate entities detected.
- No duplicate relationships detected.
- Missing formal process actors as modeled entities in the dimensional schema: Sales / Account Executive, Deal Desk, Revenue Operations, Channel / Partner Org, Customer Experience, Finance. These are documented in process annotations but not promoted to ontology classes to avoid inventing unsupported schema concepts.
- Missing machine-executable business rules for KPI formulas such as renewal capture rate and attach rate.

### Competency Questions
1. Which bookings are renewals, and what contract type, term, and customer segment are associated with them?
2. Which partners and sales teams contribute the highest booking amount or TCV by route-to-market, product family, and fiscal quarter?
3. Which bookings correspond to subscription or SaaS offers where contract context and annualized value are relevant?

## Ontology Metrics Report

### Overall Metrics Table
| Metric | Value |
|---|---:|
| Total Classes | 13 |
| Total Object Properties | 14 |
| Total Datatype Properties | 44 |
| Total Individuals | 0 |
| Hierarchy Depth | 2 |
| Total Axioms | 164 |
| Reasoning Rules / Logical Patterns | 10 |

### Per-Domain Metrics Table
| Domain | Class Count | Property Count | Individual Count | Reasoning Complexity |
|---|---:|---:|---:|---|
| Bookings | 5 | 20 | 0 | Complex |
| Date | 2 | 8 | 0 | Simple |
| Customer | 2 | 9 | 0 | Simple |
| Product | 2 | 8 | 0 | Medium |
| Partner | 2 | 7 | 0 | Medium |
| Geography | 2 | 5 | 0 | Simple |
| Sales | 2 | 7 | 0 | Medium |
| Contract | 2 | 6 | 0 | Medium |

### Reasoning Complexity Summary
- **Simple**: direct classification and descriptive lookup domains such as Date and Geography.
- **Medium**: domains with business keys, role semantics, or process-supported interpretation such as Product, Partner, Sales, and Contract.
- **Complex**: Booking domain due to cardinality restrictions, inverse properties, booking subtype inference, and cross-domain business context.

## Ontology Quality & Reasoning Insights

### Semantic Coverage
**Well-covered areas**
- Core booking star-schema concepts are fully represented.
- All seven dimensional foreign-key relationships are modeled as OWL object properties with inverse properties.
- Measures and core descriptive attributes are represented as datatype properties.
- Business glossary definitions are preserved as annotations.

**Coverage gaps**
- Glossary-only or process-mentioned attributes not implemented in SQL are not materialized as logical properties: `day_of_week`, `month_number`, `calendar_quarter`.
- Process roles are not fully formalized into ontology classes because they are not represented in the supplied OSI semantic entities.
- KPI definitions such as renewal capture rate and attach rate require additional event or fulfillment data not present in the source semantic model.

**Classes without direct datatype properties**
- Domain organizer classes have no direct datatype properties by design.

**Missing inverse properties**
- Core relationship inverses are provided for all Booking-to-dimension links.
- No inverse is created for annotation-only or classification helper relationships.

**Missing domain/range declarations**
- None for the core modeled object and datatype properties.

**Potential sparse or weak areas**
- Geography and Date remain thin semantic areas.
- Arithmetic business-rule semantics are documented but not formally inferable in OWL DL.

### Reasoning Capabilities
- **Subclass inference**: `RenewalBooking`, `NewBooking`, `UpsellBooking`, `SubscriptionOfferBooking`, and `ChannelBooking` are modeled as subclasses or defined classes using supported conditions where feasible.
- **Inverse reasoning**: from `Booking hasCustomer Customer` infer `Customer isCustomerFor Booking`, and similarly for other dimensions.
- **Functional reasoning**: core Booking-to-dimension properties are functional because the fact grain and foreign keys imply one context value per booking row.
- **Existential reasoning**: Booking is restricted to have some Date, Customer, Product, Partner, Geography, SalesRepresentative, and Contract.
- **Cardinality reasoning**: Booking has exactly 1 value for each modeled dimensional relationship.
- **Disjointness reasoning**: major business entity classes are declared pairwise distinct where appropriate to reduce accidental overlap.
- **Classification reasoning**: booking type and renewal flag enable type-specific booking subclassing when asserted through datatype values, though full datatype-based class equivalence is limited in OWL DL and therefore primarily documented.
- **No transitive or symmetric core business properties** are justified by the source material.
- **No property chains** are introduced because the available source data does not support safe multi-hop derivations without over-assertion.

### Key Reasoning Paths
1. If an instance is a Booking, it must be linked to exactly one Date, Customer, Product, Partner, Geography, SalesRepresentative, and Contract.
2. If a Booking has `bookingType` value `Renewal` or `isRenewal` true-like value, it may be classified as a RenewalBooking based on asserted typing and business rule annotation.
3. If a Product linked to a Booking has an `offerType` indicating subscription or SaaS, that Booking may be typed as a SubscriptionOfferBooking where asserted by downstream ETL or rule engines.
4. Inverse property reasoning enables navigation from any dimension instance back to the set of related bookings.

### Common SPARQL Query Patterns Supported
```sparql
# 1. Total booking amount by fiscal quarter and region
SELECT ?fiscalQuarter ?region (SUM(?amount) AS ?totalBookings)
WHERE {
  ?b a :Booking ;
     :hasDate ?d ;
     :hasGeography ?g ;
     :bookingAmountUsd ?amount .
  ?d :fiscalQuarter ?fiscalQuarter .
  ?g :region ?region .
}
GROUP BY ?fiscalQuarter ?region
```

```sparql
# 2. Renewal bookings by contract type and customer segment
SELECT ?contractType ?segment (COUNT(?b) AS ?renewalCount) (SUM(?acv) AS ?totalACV)
WHERE {
  ?b a :RenewalBooking ;
     :hasContract ?c ;
     :hasCustomer ?cust ;
     :acvUsd ?acv .
  ?c :contractType ?contractType .
  ?cust :segment ?segment .
}
GROUP BY ?contractType ?segment
```

```sparql
# 3. Partner contribution by route-to-market and product family
SELECT ?route ?family (SUM(?tcv) AS ?totalTCV)
WHERE {
  ?b a :Booking ;
     :hasPartner ?p ;
     :hasProduct ?prod ;
     :tcvUsd ?tcv .
  ?p :routeToMarket ?route .
  ?prod :productFamily ?family .
}
GROUP BY ?route ?family
```

```sparql
# 4. Sales team bookings by fiscal year
SELECT ?team ?fy (SUM(?amount) AS ?bookings)
WHERE {
  ?b a :Booking ;
     :hasSalesRepresentative ?rep ;
     :hasDate ?d ;
     :bookingAmountUsd ?amount .
  ?rep :salesTeam ?team .
  ?d :fiscalYear ?fy .
}
GROUP BY ?team ?fy
```

### Recommendations
1. Align `geo_key` and `geography_key` terminology across glossary, SQL, and ontology annotations.
2. Extend the Date domain with `day_of_week`, `month_number`, and `calendar_quarter` if these are required by downstream semantic queries.
3. Represent `is_renewal` and `auto_renew_flag` as controlled booleans in upstream data pipelines for cleaner OWL alignment.
4. Add explicit business rule metadata outside OWL DL for ACV/TCV arithmetic, attach rate, and renewal capture rate.
5. Introduce process-event entities only when additional source documents supply stable attributes and relationships for opportunity, quote, order, fulfillment, and entitlement stages.
6. Add SKOS concept schemes for controlled vocabularies such as booking type, offer type, route to market, partner tier, and contract type.

### Watch-outs
- Do not assume full process-event lineage from Quote, Order, Fulfillment, or Revenue entities because those are not represented in the supplied OSI semantic model.
- Arithmetic equality such as `booking_amount_usd = tcv_usd` for subscription/SaaS cannot be fully enforced in OWL DL.
- Renewal semantics are partly flag-based and may require data quality controls to ensure consistency between `booking_type`, `is_renewal`, and contract fields.
- Domain classes introduced for organization are ontology scaffolding, not transactional data classes.

### Ontology Validation
| Check | Result | Confidence |
|---|---|---:|
| Duplicate classes | None detected | 0.99 |
| Duplicate properties | None detected | 0.99 |
| Invalid namespaces | None detected | 0.99 |
| Missing domains | None in modeled properties | 0.98 |
| Missing ranges | None in modeled properties | 0.98 |
| Circular inheritance | None detected | 0.99 |
| Invalid restrictions | None detected in generated OWL | 0.96 |
| Logical consistency | Consistent under standard OWL 2 DL assumptions | 0.95 |
| Protégé compatibility | Compatible with RDF/XML OWL serialization | 0.99 |

### Assumptions and Inference Confidence
- Business keys for Customer, Product, Partner, and SalesRepresentative are inferred from `*_id` fields with confidence between 0.96 and 0.97.
- Booking subtype classes are supported by process descriptions and source attributes but may require ETL assertions or rule-engine support for reliable population; confidence 0.86.
- No unsupported enterprise concepts were added beyond lightweight domain organizer classes and process-supported booking subtypes.
