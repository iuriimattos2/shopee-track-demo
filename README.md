# Data Collector Demo

This repo aims to demonstrate how a simple data collection project uses Github Workflows to periodically pull data.

Data is collected and stored changes to the `data` folder every hour.

# How it works?

Github Workflows, every hour will run the `main.py` script.

The script will:

1. Read the configuration from `config.yaml`

```yaml
urls:
  - https://shopee.vn/Apple-MacBook-Air-(2020)-M1-Chip-13.3-inch-8GB-256GB-SSD-i.88201679.5873954476
```

2. For each url in `urls`, it will try to parse url to get `itemid` and `shopid`

3. Call the Shopee API to get the JSON data: https://shopee.vn/api/v4/item/get?itemid=5873954476&shopid=88201679

```json
{
  "data": {
    "itemid": 5873954476,
    "shopid": 88201679,
    "userid": 0,
    "price_max_before_discount": 2899000000000,
    "has_lowest_price_guarantee": true,
    "price_before_discount": 2899000000000,
    "price_min_before_discount": 2899000000000,
    "exclusive_price_info": null,
    "hidden_price_display": null,
    "price_min": 2659000000000,
    "price_max": 2659000000000,
    "price": 2659000000000,
    "stock": 26,
    "discount": "8%",
    ...
  }
}
```

4. Compare and update the historical data at `./data/info/{itemid}.yaml` and `./data/history/{itemid}.csv`
