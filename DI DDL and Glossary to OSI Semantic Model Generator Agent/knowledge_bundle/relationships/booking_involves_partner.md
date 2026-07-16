---
type: Relationship
title: Booking involves Partner
description: Relates booking transactions to the partner dimension.
tags:
  - Relationship
  - Partner
---

# Booking involves Partner

## Source Entity
- [Booking](../entities/booking.md)

## Target Entity
- [Partner](../entities/partner.md)

## Relationship Type
Foreign Key

## Cardinality
Many Bookings to One Partner

## Technical Mapping
`fact_bookings.partner_key -> dim_partner.partner_key`

## Confidence Score
1.00
