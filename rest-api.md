# Public Rest API for Metal X (2020-04-27)

## General API Information
* The base endpoint is: **https://api.metalx.com**
* All endpoints return either a JSON object

## HTTP Return Codes

* HTTP `4XX` return codes are used for malformed requests;
  the issue is on the sender's side.
* HTTP `429` return code is used when breaking a request rate limit.
* HTTP `5XX` return codes are used for internal errors; the issue is on
  Metal X's side.
  It is important to **NOT** treat this as a failure operation; the execution status is
  **UNKNOWN** and could have been a success.

## General endpoints

### Exchange information
```
GET /v1/exchange-info
```

**Parameters:**
NONE

**Response:**
```
{
  "timezone": "UTC",
  "serverTime": 1587998204719,
  "symbols": [
    {
      "symbol": "ETHBTC",
      "status": "running",
      "baseAsset": "ETH",
      "baseAssetPrecision": 8,
      "quoteAsset": "BTC",
      "quotePrecision": 8,
      "baseCommissionPrecision": 8,
      "quoteCommissionPrecision": 8,
      "orderTypes": [
        "LIMIT",
        "LIMIT_MAKER",
        "MARKET",
        "STOP_LOSS",
        "STOP_LOSS_LIMIT",
        "TAKE_PROFIT",
        "TAKE_PROFIT_LIMIT"
      ],
      "isSpotTradingAllowed": true,
      "isMarginTradingAllowed": false
    }
  ]
}
```

## Market Data endpoints

### Order book
```
GET /v1/depth
```

**Parameters:**

Name | Type | Mandatory | Description
------------ | ------------ | ------------ | ------------
symbol | STRING | YES | For example: MTLBTC
limit | INT | NO | Default 100; max 5000. Valid limits:[5, 10, 20, 50, 100, 500, 1000, 5000]

**Response:**
```
{
  "serverTime": 1587998357151,
  "bids": [
    {
      "quantity": "406.86",
      "price": "0.0003524"
    }
  ],
  "asks": [
    {
      "quantity": "26.94",
      "price": "0.0003526"
    }
  ]
}
```

### Recent trades list

```
GET /v1/trade-history
```

**Parameters:**

Name | Type | Mandatory | Description
------------ | ------------ | ------------ | ------------
symbol | STRING | YES |
limit | INT | NO | Default 100; max 1000.

**Response:**
```
[
  {
    "tradeId": 77725,
    "quantity": "1",
    "price": "0.00003866",
    "time": 1587999420135,
    "side": "buy"
  }
]
```
