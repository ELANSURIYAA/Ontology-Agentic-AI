---
type: Business Entity
title: Date
description: Represents calendar and fiscal date context for bookings.
tags:
  - Date
  - Dimension
---

# Date

## Business Definition
Stores calendar and fiscal date information used for analyzing bookings across time periods.

## Technical Mapping
- Table: `dim_date`
- Primary Key: `date_key`

## Attributes
- date_key
- full_date
- month_name
- calendar_year
- fiscal_year
- fiscal_quarter
- fiscal_period_seq

## Keys
- Primary Key: `date_key`

## Measures
- None

## Relationships
- [Booking occurs on Date](../relationships/booking_occurs_on_date.md)

## Business Notes
Glossary includes additional desired date attributes not implemented in DDL.

## Confidence Score
1.00
