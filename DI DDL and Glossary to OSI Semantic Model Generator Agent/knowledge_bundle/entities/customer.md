---
type: Business Entity
title: Customer
description: Represents customer organizations that purchase products or services.
tags:
  - Customer
  - Dimension
---

# Customer

## Business Definition
Contains descriptive information about customers who purchase products or services.

## Technical Mapping
- Table: `dim_customer`
- Primary Key: `customer_key`
- Business Key: `customer_id`

## Attributes
- customer_key
- customer_id
- customer_name
- segment
- industry
- account_tier
- hq_country
- hq_region

## Keys
- Primary Key: `customer_key`
- Business Key: `customer_id`

## Measures
- None

## Relationships
- [Booking is for Customer](../relationships/booking_is_for_customer.md)

## Business Notes
Used to analyze bookings by customer profile and classification.

## Confidence Score
1.00
