---
type: Business Entity
title: Partner
description: Represents partner organizations involved in selling products.
tags:
  - Partner
  - Dimension
---

# Partner

## Business Definition
Stores information about channel partners involved in selling products.

## Technical Mapping
- Table: `dim_partner`
- Primary Key: `partner_key`
- Business Key: `partner_id`

## Attributes
- partner_key
- partner_id
- partner_name
- partner_type
- partner_tier
- route_to_market

## Keys
- Primary Key: `partner_key`
- Business Key: `partner_id`

## Measures
- None

## Relationships
- [Booking involves Partner](../relationships/booking_involves_partner.md)

## Business Notes
Supports channel and route-to-market analysis.

## Confidence Score
1.00
