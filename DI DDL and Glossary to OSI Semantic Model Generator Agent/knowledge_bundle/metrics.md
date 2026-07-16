---
type: Metrics Report
title: Cisco Bookings Semantic Metrics
description: Overall and domain-level semantic metrics for the Cisco bookings model.
tags:
  - Metrics
  - Coverage
  - Quality
---

# Semantic Metrics

## Overall
- Total Tables: 8
- Total Columns: 53
- Total Relationships: 7
- Total Domains: 8
- Total Measures: 6
- Total Glossary Terms: 55
- Mapped Terms: 53
- Coverage: 96.36%

## Domain Metrics
- Bookings: 1 entity, 18 attributes, 6 measures, 100% coverage, Healthy
- Date: 1 entity, 7 attributes, 0 measures, 70% coverage, Thin
- Customer: 1 entity, 8 attributes, 0 measures, 100% coverage, Thin
- Product: 1 entity, 7 attributes, 0 measures, 100% coverage, Thin
- Partner: 1 entity, 6 attributes, 0 measures, 100% coverage, Thin
- Geography: 1 entity, 4 attributes, 0 measures, 75% coverage, Thin
- Sales: 1 entity, 6 attributes, 0 measures, 100% coverage, Thin
- Contract: 1 entity, 5 attributes, 0 measures, 100% coverage, Thin

## Validation Warnings
- Missing glossary implementation for `day_of_week` and `month_number`
- Naming mismatch between glossary `geo_key` and DDL `geography_key`
