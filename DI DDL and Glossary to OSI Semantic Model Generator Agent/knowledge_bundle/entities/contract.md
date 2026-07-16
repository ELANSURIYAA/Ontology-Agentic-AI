---
type: Business Entity
title: Contract
description: Represents customer contract context associated with bookings.
tags:
  - Contract
  - Dimension
---

# Contract

## Business Definition
Stores information describing customer contracts associated with bookings.

## Technical Mapping
- Table: `dim_contract`
- Primary Key: `contract_key`

## Attributes
- contract_key
- contract_type
- term_months
- auto_renew_flag
- coverage_level

## Keys
- Primary Key: `contract_key`

## Measures
- None

## Relationships
- [Booking is governed by Contract](../relationships/booking_is_governed_by_contract.md)

## Business Notes
Supports renewal and contract-value analysis.

## Confidence Score
1.00
