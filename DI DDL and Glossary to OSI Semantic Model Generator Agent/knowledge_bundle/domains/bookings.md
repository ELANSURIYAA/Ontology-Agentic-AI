---
type: Business Domain
title: Bookings
description: Central transactional domain representing booked order lines and commercial measures.
tags:
  - Bookings
  - Revenue
---

# Bookings Domain

## Business Purpose
Represents measurable booking transactions at booked order line grain.

## Related Entities
- [Booking](../entities/booking.md)

## Related Measures
- [quantity](../measures/quantity.md)
- [unit_list_price_usd](../measures/unit_list_price_usd.md)
- [discount_pct](../measures/discount_pct.md)
- [booking_amount_usd](../measures/booking_amount_usd.md)
- [acv_usd](../measures/acv_usd.md)
- [tcv_usd](../measures/tcv_usd.md)

## Notes
Explicitly supported by `fact_bookings`.
