---
type: Relationship
title: Booking is for Customer
description: Relates booking transactions to the customer dimension.
tags:
  - Relationship
  - Customer
---

# Booking is for Customer

## Source Entity
- [Booking](../entities/booking.md)

## Target Entity
- [Customer](../entities/customer.md)

## Relationship Type
Foreign Key

## Cardinality
Many Bookings to One Customer

## Technical Mapping
`fact_bookings.customer_key -> dim_customer.customer_key`

## Confidence Score
1.00
