<h1 align="center">COMMON API</h1>
 
[Получение актуального баланса](#balance)

[Получение лучших курсов по заявкам трейдеров](#rates)

[Получение списка банков](#brokers)

[Получение биржевого курса криптовалют относительно валют](#exchange)

[Получение истории платежей](#paymentHistory)
 
 <a name="balance"></a>
## Получение актуального баланса

```http
  GET rest/v2/balance?symbol=btc&currencies=rub,usd
```

#### Query parameters

| Parameter | Description                | Default       |
| :-------- | :------------------------- | ------------- |
| `symbol` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md) | 
| `currencies` | **Required**. [Список валют](CURRENCIES.md) | rub

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
## Получение лучших курсов по заявкам трейдеров

```http
  GET rest/v2/rates/btc?currency=rub&lot_type=sell
```

#### Query parameters
 
| Parameter | Description                | Default       |
| :-------- | :------------------------- | ------------- | 
| `currency` | Филтрация по валюте. (rub, usd, kzt, uah, byn, tjs, azn, uzs) | rub
| `lot_type` | Фильтрация по типу операции. (buy, sell) | sell

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
## Получение списка банков

```http
  GET rest/v2/brokers?currency=rub
```
#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `currency` | **Required**. (rub, usd, kzt, uah, byn, tjs, azn, uzs)
| `sky_pay` | Если флаг **true**, то в response придут те брокеры, которые поддерживают SKY PAY
| `sale_v2` | Если флаг **true**, то в response придут те брокеры, которые поддерживают SALE V2

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
## Получение биржевого курса криптовалют относительно валют

```http
  GET rest/v2/actual-rates/{symbol}
```
#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `symbol` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md)

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

 <a name="paymentHistory"></a>
## Получение истории платежей

```http
  GET rest/v2/merchant-payment-statistics?action=sky-pay
```
#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `action` | **Required**. Варианты: ["sky-pay", "sky-pay-v2", "sky-sale", "sky-sale-v2", "cpayment", "withdrawals"].

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
