---
type: Relationship
title: Booking is associated with Geography
description: Relates booking transactions to the geography dimension.
tags:
  - Relationship
  - Geography
---

# Booking is associated with Geography

## Source Entity
- [Booking](../entities/booking.md)

## Target Entity
- [Geography](../entities/geography.md)

## Relationship Type
Foreign Key

## Cardinality
Many Bookings to One Geography

## Technical Mapping
`fact_bookings.geography_key -> dim_geography.geography_key`

## Confidence Score
1.00
