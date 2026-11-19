---
name: fragua-data-usa
description: Answer questions about U.S. real estate markets and demographics with the Fragua Data USA connector. Use when the user asks about home prices, price per square foot, supply, listings or comparables, absorption, days on market, rental yield, affordability, investment ratings, or census demographics (population, age, income, poverty, occupancy) for a U.S. state, county, city, ZIP code or neighbourhood.
---

# U.S. real estate data with Fragua Data USA

The Fragua Data USA connector gives read-only market, listing and census data from Atlas Real
Estate Analytics. Every call counts against the user's own monthly Fragua allowance, so call only
the tools the question needs.

## How to answer

- Reply in the user's language. Lead with one headline insight, then the supporting numbers,
  comparisons and caveats.
- Do not paste raw JSON, internal field names or tool names, and do not narrate tool calls.
- Areas are square feet and prices are US dollars. Yield, absorption and ratings are percent
  values: 8.42 means 8.42%.
- For a time series, give the analysis first (direction, size, recent change), then a chart or a
  compact table.
- End with: Source: Fragua by Atlas Real Estate Analytics.

## Resolve the place first

Data tools take `zone_names` (a list) and `zone_type` (one of state, county, subcounty, city, town,
village, CDP, zip_code, neighbourhood). Names match exactly, with no fuzzy search.

1. A 5-digit number is a `zip_code`.
2. If a name is not found, call `lookup_regions` with the other plausible types: one name can
   exist at several levels (Palm Beach is a county and a town). If several match, ask the user.
3. Otherwise call `list_contained_regions` on the parent area (for example all neighbourhoods in a
   city) and pick the match. Compound names have spaces around hyphens ("Wynwood - Edgewater").
4. If the parent is unknown, ask the user before guessing.

## Pick the tool

| Question | Tool |
| --- | --- |
| Market snapshot (supply, median price, price per sq ft) | `get_market_overview` |
| Change over time | `get_price_trends`, `get_price_per_sqft_trends`, `get_supply_trends`, `get_absorption_trends`, `get_rental_yield_trends`, `get_days_on_market_trends`, `get_investment_ratings_trends` |
| Latest pace and value | `get_absorption_rate`, `get_days_on_market`, `get_affordability`, `get_investment_ratings` |
| Distribution | `get_supply_by_bedrooms`, `get_amenities_share`, `get_price_per_sqft_range`, `get_size_vs_price_regression` |
| Individual listings | `get_comparable_listings` (page with `limit` and `offset`; `total_count` is the full count) |
| What is on the market now | `get_active_listing_profile` (the active listing stock, not buyer demand or sales) |
| Census demographics | `get_total_population`, `get_population_pyramid`, `get_median_age`, `get_race_ethnicity`, `get_household_relationships`, `get_housing_occupancy`, `get_household_income`, `get_poverty_status` |
| Map coordinates of ZIP codes | `get_coordinates_from_zip_code` |

## Filters

- `bedrooms` and `bathrooms` are lists of integers 0-4, where 4 means 4 or more. Omit optional
  fields instead of sending null.
- `new_construction` (0 or 1) separates new builds from resale.
- Absorption and days-on-market tools are whole-zone metrics: omit `bedrooms` for all homes or give
  exactly one value; they take no bathroom or property-feature filters.
- Investment ratings and their trends cover whole zones only, with no bedroom, bathroom or feature
  filters.
- "No data" means nothing matched: broaden the filters or recheck the zone name and type.

## When something fails

- Validation error: drop the optional fields you added, fix the format and retry quietly. After two
  or three attempts, tell the user what to change.
- Sign-in expired: ask the user to reconnect Fragua Data USA (claude.ai: Settings > Connectors;
  Claude Code: `/mcp`).
- Monthly allowance reached or data not enabled for the account: do not retry. Say so plainly and
  pass on the contact or link from the message.
- There is no tool for usage counts or account settings; do not guess remaining calls.

## Out of scope

Fragua Data USA covers U.S. places only and cannot make offers, transactions or account changes.
Say so and offer a U.S. market question it can answer instead.
