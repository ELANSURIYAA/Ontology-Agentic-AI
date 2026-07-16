# OSI Semantic Model

## Domains

### 1. Bookings Domain
**Description:** Central transactional domain representing booked order lines and associated commercial measures.

### 2. Date Domain
**Description:** Calendar and fiscal time analysis domain used to slice booking performance across reporting periods.

### 3. Customer Domain
**Description:** Customer master analysis domain for understanding who is purchasing and how customers are classified.

### 4. Product Domain
**Description:** Product and offer analysis domain describing the items and services included in bookings.

### 5. Partner Domain
**Description:** Channel and route-to-market domain describing partners involved in sales motions.

### 6. Geography Domain
**Description:** Geographic reporting domain for analyzing bookings by region, theater, and country.

### 7. Sales Domain
**Description:** Sales organization domain representing sales representatives, roles, teams, and coverage.

### 8. Contract Domain
**Description:** Contract context domain describing agreement structure, duration, renewal behavior, and service coverage.

---

## Entities

### Booking
- **Technical Table:** `fact_bookings`
- **Description:** Stores measurable business transactions where each row represents one booked order line.
- **Attributes:**
  - `booking_id`: unique identifier for a booking transaction
  - `order_number`: sales order number
  - `order_line_number`: line number within the order
  - `date_key`: reference to booking date
  - `customer_key`: reference to customer
  - `product_key`: reference to product
  - `partner_key`: reference to partner
  - `geography_key`: reference to geography
  - `sales_rep_key`: reference to sales representative
  - `contract_key`: reference to contract
  - `booking_type`: transaction type such as New, Renewal, Upsell
  - `is_renewal`: renewal indicator
  - `quantity`: number of units booked
  - `unit_list_price_usd`: list price per unit in USD
  - `discount_pct`: percentage discount
  - `booking_amount_usd`: net booking amount in USD
  - `acv_usd`: annual contract value in USD
  - `tcv_usd`: total contract value in USD
- **Measures:**
  - `quantity`
  - `unit_list_price_usd`
  - `discount_pct`
  - `booking_amount_usd`
  - `acv_usd`
  - `tcv_usd`
- **Keys:**
  - Primary Key: `booking_id`
  - Foreign Keys: `date_key`, `customer_key`, `product_key`, `partner_key`, `geography_key`, `sales_rep_key`, `contract_key`
- **Relationships:**
  - belongs to Date
  - belongs to Customer
  - belongs to Product
  - belongs to Partner
  - belongs to Geography
  - belongs to Sales Representative
  - belongs to Contract

### Date
- **Technical Table:** `dim_date`
- **Description:** Stores calendar and fiscal date information used for period-based booking analysis.
- **Attributes:**
  - `date_key`: surrogate date key
  - `full_date`: full calendar date
  - `month_name`: calendar month name
  - `calendar_year`: calendar year
  - `fiscal_year`: fiscal year
  - `fiscal_quarter`: fiscal quarter
  - `fiscal_period_seq`: sequential fiscal period
- **Measures:** None
- **Keys:**
  - Primary Key: `date_key`
- **Relationships:**
  - referenced by Booking

### Customer
- **Technical Table:** `dim_customer`
- **Description:** Contains descriptive information about customers purchasing products or services.
- **Attributes:**
  - `customer_key`: surrogate customer key
  - `customer_id`: business customer identifier
  - `customer_name`: customer organization name
  - `segment`: business segment
  - `industry`: industry classification
  - `account_tier`: strategic account classification
  - `hq_country`: headquarters country
  - `hq_region`: headquarters region
- **Measures:** None
- **Keys:**
  - Primary Key: `customer_key`
  - Business Key: `customer_id` inferred, confidence 0.97
- **Relationships:**
  - referenced by Booking

### Product
- **Technical Table:** `dim_product`
- **Description:** Contains descriptive information about products and services included in bookings.
- **Attributes:**
  - `product_key`: surrogate product key
  - `product_id`: business product identifier
  - `product_name`: commercial product name
  - `product_family`: related product grouping
  - `technology_domain`: technology category
  - `offer_type`: offer classification
  - `business_entity`: responsible business unit
- **Measures:** None
- **Keys:**
  - Primary Key: `product_key`
  - Business Key: `product_id` inferred, confidence 0.97
- **Relationships:**
  - referenced by Booking

### Partner
- **Technical Table:** `dim_partner`
- **Description:** Stores information about channel partners involved in selling products.
- **Attributes:**
  - `partner_key`: surrogate partner key
  - `partner_id`: business partner identifier
  - `partner_name`: partner organization name
  - `partner_type`: partner classification
  - `partner_tier`: partner program tier
  - `route_to_market`: channel route model
- **Measures:** None
- **Keys:**
  - Primary Key: `partner_key`
  - Business Key: `partner_id` inferred, confidence 0.97
- **Relationships:**
  - referenced by Booking

### Geography
- **Technical Table:** `dim_geography`
- **Description:** Provides geographic hierarchy for reporting bookings across global areas.
- **Attributes:**
  - `geography_key`: surrogate geography key
  - `region`: top reporting region
  - `theater`: sales theater
  - `country`: country
- **Measures:** None
- **Keys:**
  - Primary Key: `geography_key`
- **Relationships:**
  - referenced by Booking

### Sales Representative
- **Technical Table:** `dim_sales_rep`
- **Description:** Contains information about sales representatives responsible for bookings.
- **Attributes:**
  - `sales_rep_key`: surrogate sales representative key
  - `rep_id`: business identifier for sales rep
  - `rep_name`: representative name
  - `sales_role`: functional role
  - `sales_team`: team or organization
  - `segment_covered`: customer segment covered
- **Measures:** None
- **Keys:**
  - Primary Key: `sales_rep_key`
  - Business Key: `rep_id` inferred, confidence 0.96
- **Relationships:**
  - referenced by Booking

### Contract
- **Technical Table:** `dim_contract`
- **Description:** Stores information describing customer contracts associated with bookings.
- **Attributes:**
  - `contract_key`: surrogate contract key
  - `contract_type`: contract category
  - `term_months`: duration in months
  - `auto_renew_flag`: auto-renew indicator
  - `coverage_level`: service/support coverage
- **Measures:** None
- **Keys:**
  - Primary Key: `contract_key`
- **Relationships:**
  - referenced by Booking

---

## Relationships

| Relationship Name | Parent Entity | Child Entity | Relationship Type | Cardinality | Confidence Score |
|---|---|---|---|---|---:|
| Booking occurs on Date | Date | Booking | Foreign Key | 1-to-many | 1.00 |
| Booking is for Customer | Customer | Booking | Foreign Key | 1-to-many | 1.00 |
| Booking includes Product | Product | Booking | Foreign Key | 1-to-many | 1.00 |
| Booking involves Partner | Partner | Booking | Foreign Key | 1-to-many | 1.00 |
| Booking is associated with Geography | Geography | Booking | Foreign Key | 1-to-many | 1.00 |
| Booking is owned by Sales Representative | Sales Representative | Booking | Foreign Key | 1-to-many | 1.00 |
| Booking is governed by Contract | Contract | Booking | Foreign Key | 1-to-many | 1.00 |

---

## Measures

| Measure Name | Business Definition | Aggregation Type | Source Entity |
|---|---|---|---|
| quantity | Number of product units included in the booking. | Additive | Booking |
| unit_list_price_usd | Standard list price per product unit before discounts. | Non-additive / average or point-in-time rate | Booking |
| discount_pct | Percentage discount applied to the standard list price. | Non-additive / average with business rule | Booking |
| booking_amount_usd | Net booking revenue after applying discounts. | Additive | Booking |
| acv_usd | Annual Contract Value associated with the booking. | Additive | Booking |
| tcv_usd | Total Contract Value over the full duration of the contract. | Additive | Booking |

---

## Glossary Mapping

| Business Term | Technical Mapping | Confidence Score |
|---|---|---:|
| date_key | `dim_date.date_key`, `fact_bookings.date_key` | 1.00 |
| full_date | `dim_date.full_date` | 1.00 |
| month_name | `dim_date.month_name` | 1.00 |
| calendar_year | `dim_date.calendar_year` | 1.00 |
| fiscal_period_seq | `dim_date.fiscal_period_seq` | 1.00 |
| fiscal_quarter | `dim_date.fiscal_quarter` | 1.00 |
| fiscal_year | `dim_date.fiscal_year` | 1.00 |
| day_of_week | Not present in DDL; glossary-only term | 0.00 |
| month_number | Not present in DDL; glossary-only term | 0.00 |
| customer_key | `dim_customer.customer_key`, `fact_bookings.customer_key` | 1.00 |
| customer_id | `dim_customer.customer_id` | 1.00 |
| customer_name | `dim_customer.customer_name` | 1.00 |
| segment | `dim_customer.segment`, `dim_sales_rep.segment_covered` semantic partial for covered segment | 0.92 |
| industry | `dim_customer.industry` | 1.00 |
| account_tier | `dim_customer.account_tier` | 1.00 |
| hq_country | `dim_customer.hq_country` | 1.00 |
| hq_region | `dim_customer.hq_region` | 1.00 |
| product_key | `dim_product.product_key`, `fact_bookings.product_key` | 1.00 |
| product_id | `dim_product.product_id` | 1.00 |
| product_name | `dim_product.product_name` | 1.00 |
| product_family | `dim_product.product_family` | 1.00 |
| technology_domain | `dim_product.technology_domain` | 1.00 |
| offer_type | `dim_product.offer_type` | 1.00 |
| business_entity | `dim_product.business_entity` | 1.00 |
| partner_key | `dim_partner.partner_key`, `fact_bookings.partner_key` | 1.00 |
| partner_id | `dim_partner.partner_id` | 1.00 |
| partner_name | `dim_partner.partner_name` | 1.00 |
| partner_type | `dim_partner.partner_type` | 1.00 |
| partner_tier | `dim_partner.partner_tier` | 1.00 |
| route_to_market | `dim_partner.route_to_market` | 1.00 |
| geo_key | `dim_geography.geography_key`, `fact_bookings.geography_key` name-aligned by semantic inference | 0.82 |
| region | `dim_geography.region`, `dim_customer.hq_region` partial contextual usage | 0.88 |
| theater | `dim_geography.theater` | 1.00 |
| country | `dim_geography.country`, `dim_customer.hq_country` partial contextual usage | 0.88 |
| sales_rep_key | `dim_sales_rep.sales_rep_key`, `fact_bookings.sales_rep_key` | 1.00 |
| rep_id | `dim_sales_rep.rep_id` | 1.00 |
| rep_name | `dim_sales_rep.rep_name` | 1.00 |
| sales_role | `dim_sales_rep.sales_role` | 1.00 |
| sales_team | `dim_sales_rep.sales_team` | 1.00 |
| segment_covered | `dim_sales_rep.segment_covered` | 1.00 |
| contract_key | `dim_contract.contract_key`, `fact_bookings.contract_key` | 1.00 |
| contract_type | `dim_contract.contract_type` | 1.00 |
| term_months | `dim_contract.term_months` | 1.00 |
| auto_renew_flag | `dim_contract.auto_renew_flag` | 1.00 |
| coverage_level | `dim_contract.coverage_level` | 1.00 |
| booking_id | `fact_bookings.booking_id` | 1.00 |
| order_number | `fact_bookings.order_number` | 1.00 |
| order_line_number | `fact_bookings.order_line_number` | 1.00 |
| booking_type | `fact_bookings.booking_type` | 1.00 |
| is_renewal | `fact_bookings.is_renewal` | 1.00 |
| quantity | `fact_bookings.quantity` | 1.00 |
| unit_list_price_usd | `fact_bookings.unit_list_price_usd` | 1.00 |
| discount_pct | `fact_bookings.discount_pct` | 1.00 |
| booking_amount_usd | `fact_bookings.booking_amount_usd` | 1.00 |
| acv_usd | `fact_bookings.acv_usd` | 1.00 |
| tcv_usd | `fact_bookings.tcv_usd` | 1.00 |

---

## Validation
- Missing glossary mappings: `day_of_week`, `month_number`
- Duplicate entities: none detected
- Duplicate measures: none detected
- Circular relationships: none detected
- Missing keys: none detected
- Invalid semantic domains: none detected
- Orphan entities: none detected
