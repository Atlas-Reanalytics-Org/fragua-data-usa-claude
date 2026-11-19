# Fragua Data USA

![Fragua Data USA](assets/logo.png)

Ask Claude about U.S. real estate: market snapshots, price and supply trends, absorption, rental yield,
days on market, affordability, investment ratings, comparable listings and census demographics for
states, counties, cities, ZIP codes and neighbourhoods. Data comes from Fragua by Atlas Real Estate Analytics and is
read-only.

This plugin bundles the Fragua Data USA connector (`https://apiv2.atlas-reanalytics.com/public-usa-mcp/mcp`) with a skill that teaches Claude
how to resolve U.S. place names, pick the right data, and present the results.

## Requirements

A Fragua USA account (username and password). No account yet? Write to welcome@atlas-reanalytics.com.

## Use it

1. Add the plugin, then connect **Fragua Data USA** from the plugin's **Connectors** tab and sign in with
   your Fragua username and password.
2. Ask, for example:
   - "What does the housing market look like in Miami-Dade County, Florida?"
   - "Find 3-bedroom homes for sale in ZIP code 33139 under $1.5 million."
   - "How have median asking prices changed over the last year in Palm Beach County?"
   - "What is the population and median age of Broward County, Florida?"

### Claude Code

```bash
claude plugin marketplace add Atlas-Reanalytics-Org/fragua-data-usa-claude
claude plugin install fragua-data-usa@atlas-reanalytics
```

Then run `/mcp`, select **fragua-data-usa** and sign in. Port `4322` must be free on your computer while
you sign in.

## Data and privacy

When Claude calls a tool, the plugin sends the place names and filters of your question (for example a
county name, bedroom counts or a price limit) to the Fragua Data USA server at `https://apiv2.atlas-reanalytics.com/public-usa-mcp/mcp`, together
with your sign-in token. Fragua records each call (your user, the tool, the request, the status and the
time) to count it against your account's monthly allowance. Sign-in is handled by Auth0 for
Atlas Real Estate Analytics. The plugin itself stores nothing, runs no local code and sends no data anywhere else.

Documentation and troubleshooting: https://us.fragua-ai-plugins.atlas-reanalytics.com/claude

Privacy policy: https://atlas-reanalytics.com/fragua/en/privacy-policy/
Terms of service: https://atlas-reanalytics.com/fragua/en/terms-and-conditions/

## Support

welcome@atlas-reanalytics.com - https://us.fragua-ai-plugins.atlas-reanalytics.com/support
