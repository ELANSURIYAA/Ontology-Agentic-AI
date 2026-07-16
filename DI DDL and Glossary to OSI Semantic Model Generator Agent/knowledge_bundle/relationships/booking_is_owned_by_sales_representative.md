---
type: Relationship
title: Booking is owned by Sales Representative
description: Relates booking transactions to the responsible sales representative.
tags:
  - Relationship
  - Sales Representative
---

# Booking is owned by Sales Representative

## Source Entity
- [Booking](../entities/booking.md)

## Target Entity
- [Sales Representative](../entities/sales_representative.md)

## Relationship Type
Foreign Key

## Cardinality
Many Bookings to One Sales Representative

## Technical Mapping
`fact_bookings.sales_rep_key -> dim_sales_rep.sales_rep_key`

## Confidence Score
1.00
