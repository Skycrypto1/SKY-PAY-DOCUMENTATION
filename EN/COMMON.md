<h1 align="center">COMMON API</h1>
 
[Getting the current balance](#balance)

[Obtaining the best rates based on traders' requests](#rates)

[Getting brokers list](#brokers)

[Getting the exchange rate of cryptocurrencies relative to currencies](#exchange)

[Getting payment history](#paymentHistory)

[Payment statistics by brokers](#brokerStatistics)

[Search by label](#searchByLabel)
 
 <a name="balance"></a>
## Getting the current balance

```http
  GET rest/v2/balance?symbol=btc&currencies=rub,usd
```

#### Query parameters

| Parameter | Description                | Default       |
| :-------- | :------------------------- | ------------- |
| `symbol` | **Required**. [Cryptocurrencies list](CRYPTOCURRENCIES.md) | 
| `currencies` | **Required**. [Currencies list](CURRENCIES.md) | rub

#### Response example

```javascript
{
  "balance": 1111.8080573,
  "balance_rub": 2299424746.9870005,
  "balance_usd": 29548922.989762727,
  "symbol": "btc",
  "updated_at": "2020-03-25T14:38:06.515058Z"
}
```
 <a name="rates"></a>
## Obtaining the best rates based on traders' requests

```http
  GET rest/v2/rates/btc?currency=rub&lot_type=sell
```

#### Query parameters
 
| Parameter | Description                | Default       |
| :-------- | :------------------------- | ------------- | 
| `currency` | Filter by currency. (rub, usd, kzt, uah, byn, tjs, azn, uzs) | rub
| `lot_type` | Filter by operation type. (buy, sell) | sell

#### Response example

```javascript
[
  {
  "broker": "Mastercard", 
  "currency": "rub",
  "lot_type": "sell",
  "rate": 72.16,
  "symbol": "btc"
  },
  ...
]
```
 <a name="brokers"></a>
## Getting a list of banks

```http
  GET rest/v2/brokers?currency=rub
```
#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `currency` | **Required**. (rub, usd, kzt, uah, byn, tjs, azn, uzs)
| `sky_pay` | If the flag is **true**, then the response will include those brokers that support SKY PAY
| `sale_v2` | If the flag is **true**, then the response will include those brokers that support SALE V2

#### Response example

```javascript
[
  {
  "id": "3d5f3052-2ca0-4d37-847a-d1ad841b36c5",
  "is_card": true,
  "name": "Райффайзен"
  },
  {
    "id": "f40b4b3a-3357-4c4d-b684-4ac3b9b2cd2c",
    "is_card": true,
    "name": "Росбанк"
  },
  ...
]
```
 <a name="exchange"></a>
## Getting the exchange rate of cryptocurrencies relative to currencies

```http
  GET rest/v2/actual-rates/{symbol}
```
#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `symbol` | **Required**. [Cryptocurrencies list](CRYPTOCURRENCIES.md)

#### Response example

```javascript

[
    {
        "currency": "rub",
        "rate": 2413785.0,
        "symbol": "btc"
    },
    {
        "currency": "usd",
        "rate": 29384.52,
        "symbol": "btc"
    },
    {
        "currency": "uah",
        "rate": 1105277.0,
        "symbol": "btc"
    },
    ...
]
```

 <a name="paymentHistory"></a>
## Getting payment history

```http
  GET rest/v2/merchant-payment-statistics?action=sky-pay
```
#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `action` | **Required**. Options: ["sky-pay", "sky-pay-v2", "sky-sale", "sky-sale-v2", "cpayment", "withdrawals"].

#### Response example

```javascript

[
    {
        "amount": 1500.0,
        "created_at": "2023-07-25T10:55:32.373747+00:00",
        "currency": "rub",
        "id": "6945d788-e857-4f79-835c-f807653fa828",
        "is_currency_amount": true,
        "label": "111111",
        "status": 3,
        "symbol": "btc"
    }
    ...
]
```

 <a name="brokerStatistics"></a>
## Payment statistics by banks

```http
  GET rest/v2/merchant-broker-statistics
```

#### Response example

```javascript
[
    {
        "id": "ad70be25-5bb0-401f-a7a2-1f71c403cabf",
        "is_card": true,
        "name": "Сбербанк",
        "payments_count": 1
    }
]
```

 <a name="searchByLabel"></a>
## Search by label

```http
  GET rest/v2/label-search/<instance>/<label>
```

<b>Note: the maximum possible number of received records with the same label is 100.</b>

#### Parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `instance` | **Required**. Veriants: ["pay_v2", "sale_v2", "sale", "pay"].
| `label` | **Required**. Label for search.
