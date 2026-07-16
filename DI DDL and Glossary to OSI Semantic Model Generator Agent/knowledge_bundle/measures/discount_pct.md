---
type: Measure
title: discount_pct
description: Percentage discount applied to the standard list price.
tags:
  - Measure
  - Discount
---

# discount_pct

## Business Definition
Percentage discount applied to the standard list price.

## Aggregation Type
Non-additive / average with business rule

## Associated Entities
- [Booking](../entities/booking.md)

## Technical Mapping
`fact_bookings.discount_pct`

## Business Notes
Requires defined averaging or weighting rules.

## Confidence Score
1.00
