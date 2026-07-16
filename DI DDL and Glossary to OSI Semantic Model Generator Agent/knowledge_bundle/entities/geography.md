---
type: Business Entity
title: Geography
description: Represents geographic reporting structures used in booking analysis.
tags:
  - Geography
  - Dimension
---

# Geography

## Business Definition
Provides hierarchical geographic information for analyzing bookings across global regions.

## Technical Mapping
- Table: `dim_geography`
- Primary Key: `geography_key`
- Glossary Alias: `geo_key`

## Attributes
- geography_key
- region
- theater
- country

## Keys
- Primary Key: `geography_key`

## Measures
- None

## Relationships
- [Booking is associated with Geography](../relationships/booking_is_associated_with_geography.md)

## Business Notes
Key naming differs between glossary and DDL.

## Confidence Score
0.82
