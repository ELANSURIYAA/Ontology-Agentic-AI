---
type: Relationship
title: Booking includes Product
description: Relates booking transactions to the product dimension.
tags:
  - Relationship
  - Product
---

# Booking includes Product

## Source Entity
- [Booking](../entities/booking.md)

## Target Entity
- [Product](../entities/product.md)

## Relationship Type
Foreign Key

## Cardinality
Many Bookings to One Product

## Technical Mapping
`fact_bookings.product_key -> dim_product.product_key`

## Confidence Score
1.00
