---
type: Business Entity
title: Product
description: Represents products and services sold through bookings.
tags:
  - Product
  - Dimension
---

# Product

## Business Definition
Contains descriptive information about products and services sold through bookings.

## Technical Mapping
- Table: `dim_product`
- Primary Key: `product_key`
- Business Key: `product_id`

## Attributes
- product_key
- product_id
- product_name
- product_family
- technology_domain
- offer_type
- business_entity

## Keys
- Primary Key: `product_key`
- Business Key: `product_id`

## Measures
- None

## Relationships
- [Booking includes Product](../relationships/booking_includes_product.md)

## Business Notes
Supports portfolio and offer analysis.

## Confidence Score
1.00
