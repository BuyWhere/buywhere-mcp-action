# BuyWhere MCP Server — GitHub Action

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-BuyWhere%20MCP%20Server-blue.svg)](https://github.com/marketplace/actions/buywhere-mcp-server)

Start the **BuyWhere MCP server** in your GitHub Actions workflow. Give your AI agents real-time access to **1.5M+ products** across **20+ e-commerce platforms** in Southeast Asia and the US.

## What is BuyWhere?

[BuyWhere](https://buywhere.ai) is an agent-native product catalog API that indexes products from Shopee, Lazada, Amazon SG/US, Walmart, Carousell, FairPrice, Harvey Norman, Courts, Challenger, and 50+ merchants into a single, normalized, real-time endpoint.

## Features

- **Product Search** — Full-text search across 1.5M+ products with price, category, merchant, region, and rating filters
- **Price Comparison** — Compare 2-10 products side-by-side across merchants
- **Deal Discovery** — Find products with active discounts sorted by savings percentage
- **Category Browsing** — Browse product categories and subcategories
- **Best Price** — Find the cheapest price for any product across all merchants
- **Multi-Region** — Singapore, United States, Vietnam, Thailand, Malaysia, Philippines, Indonesia
- **Multi-Currency** — SGD, USD, MYR, IDR, THB, PHP, VND

## Usage

```yaml
name: AI Shopping Agent

on:
  schedule:
    - cron: '0 9 * * *'  # Daily at 9 AM

jobs:
  check-deals:
    runs-on: ubuntu-latest
    steps:
      - uses: BuyWhere/buywhere-mcp-action@v1
        with:
          api-key: ${{ secrets.BUYWHERE_API_KEY }}

      - name: Search for deals
        run: |
          # MCP server is now running on port 8081
          curl -s http://localhost:8081/mcp \
            -H "Content-Type: application/json" \
            -d '{
              "jsonrpc": "2.0",
              "method": "tools/call",
              "params": {
                "name": "get_deals",
                "arguments": {
                  "min_discount": 30,
                  "country": "SG",
                  "limit": 10
                }
              },
              "id": 1
            }'
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `api-key` | Yes | — | BuyWhere API key |
| `api-url` | No | `https://api.buywhere.ai` | API base URL |
| `mcp-port` | No | `8081` | Port for the MCP server |

## Get a Free API Key

1. Go to [https://api.buywhere.ai/v1/auth/register](https://api.buywhere.ai/v1/auth/register)
2. Create your account (no credit card required)
3. Copy your API key
4. Add it as a repository secret: `BUYWHERE_API_KEY`

Free tier: **1,000 calls/month**. Pro: $19/mo. Enterprise: custom pricing.

## Tools Available via MCP

| Tool | Description |
|------|-------------|
| `search_products` | Full-text product search with filters |
| `get_product` | Get product details by BuyWhere product ID |
| `compare_products` | Compare 2-10 products side-by-side across merchants |
| `get_deals` | Get discounted products sorted by discount % |
| `list_categories` | Browse product categories with product counts |
| `find_best_price` | Find cheapest price across all merchants |

## Documentation

- [API Docs](https://api.buywhere.ai/docs/guides/mcp)
- [Website](https://buywhere.ai)
- [Pricing](https://buywhere.ai/pricing)
- [GitHub](https://github.com/BuyWhere/buywhere)

## License

MIT
