---
type: Business Entity
title: Sales Representative
description: Represents sales representatives responsible for bookings.
tags:
  - Sales Representative
  - Dimension
---

# Sales Representative

## Business Definition
Contains information about sales representatives responsible for customer bookings.

## Technical Mapping
- Table: `dim_sales_rep`
- Primary Key: `sales_rep_key`
- Business Key: `rep_id`

## Attributes
- sales_rep_key
- rep_id
- rep_name
- sales_role
- sales_team
- segment_covered

## Keys
- Primary Key: `sales_rep_key`
- Business Key: `rep_id`

## Measures
- None

## Relationships
- [Booking is owned by Sales Representative](../relationships/booking_is_owned_by_sales_representative.md)

## Business Notes
Supports seller and organizational performance analysis.

## Confidence Score
1.00
