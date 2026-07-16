---
type: Relationship
title: Booking is governed by Contract
description: Relates booking transactions to the contract dimension.
tags:
  - Relationship
  - Contract
---

# Booking is governed by Contract

## Source Entity
- [Booking](../entities/booking.md)

## Target Entity
- [Contract](../entities/contract.md)

## Relationship Type
Foreign Key

## Cardinality
Many Bookings to One Contract

## Technical Mapping
`fact_bookings.contract_key -> dim_contract.contract_key`

## Confidence Score
1.00
