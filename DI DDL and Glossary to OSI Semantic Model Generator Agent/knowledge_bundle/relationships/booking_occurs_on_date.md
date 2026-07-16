---
type: Relationship
title: Booking occurs on Date
description: Relates booking transactions to the date dimension.
tags:
  - Relationship
  - Date
---

# Booking occurs on Date

## Source Entity
- [Booking](../entities/booking.md)

## Target Entity
- [Date](../entities/date.md)

## Relationship Type
Foreign Key

## Cardinality
Many Bookings to One Date

## Technical Mapping
`fact_bookings.date_key -> dim_date.date_key`

## Confidence Score
1.00
