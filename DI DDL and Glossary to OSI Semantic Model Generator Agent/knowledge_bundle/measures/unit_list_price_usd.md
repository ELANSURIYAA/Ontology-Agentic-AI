---
type: Measure
title: unit_list_price_usd
description: Standard list price per product unit before discounts.
tags:
  - Measure
  - Price
---

# unit_list_price_usd

## Business Definition
Standard list price per product unit before discounts.

## Aggregation Type
Non-additive / average or point-in-time rate

## Associated Entities
- [Booking](../entities/booking.md)

## Technical Mapping
`fact_bookings.unit_list_price_usd`

## Business Notes
Should not be blindly summed.

## Confidence Score
1.00
