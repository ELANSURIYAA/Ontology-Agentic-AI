---
type: Business Entity
title: Booking
description: Represents a booked order line transaction in the booking system.
tags:
  - Booking
  - Fact
---

# Booking

## Business Definition
Stores measurable business transactions where each record corresponds to a booked order line.

## Technical Mapping
- Table: `fact_bookings`
- Primary Key: `booking_id`

## Attributes
- booking_id
- order_number
- order_line_number
- date_key
- customer_key
- product_key
- partner_key
- geography_key
- sales_rep_key
- contract_key
- booking_type
- is_renewal
- quantity
- unit_list_price_usd
- discount_pct
- booking_amount_usd
- acv_usd
- tcv_usd

## Keys
- Primary Key: `booking_id`
- Foreign Keys: `date_key`, `customer_key`, `product_key`, `partner_key`, `geography_key`, `sales_rep_key`, `contract_key`

## Measures
- [quantity](../measures/quantity.md)
- [unit_list_price_usd](../measures/unit_list_price_usd.md)
- [discount_pct](../measures/discount_pct.md)
- [booking_amount_usd](../measures/booking_amount_usd.md)
- [acv_usd](../measures/acv_usd.md)
- [tcv_usd](../measures/tcv_usd.md)

## Relationships
- [Booking occurs on Date](../relationships/booking_occurs_on_date.md)
- [Booking is for Customer](../relationships/booking_is_for_customer.md)
- [Booking includes Product](../relationships/booking_includes_product.md)
- [Booking involves Partner](../relationships/booking_involves_partner.md)
- [Booking is associated with Geography](../relationships/booking_is_associated_with_geography.md)
- [Booking is owned by Sales Representative](../relationships/booking_is_owned_by_sales_representative.md)
- [Booking is governed by Contract](../relationships/booking_is_governed_by_contract.md)

## Business Notes
Contains additive and non-additive commercial measures.

## Confidence Score
1.00
