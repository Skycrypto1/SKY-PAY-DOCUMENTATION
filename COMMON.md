<h1 align="center">COMMON API</h1>
 
[Получение актуального баланса](#balance)

[Получение актуальных курсов](#rates)

[Получение списка банков](#brokers)

[Получение актуального биржевого курса](#exchange)
 
 <a name="balance"></a>
## Получение актуального баланса

```http
  GET rest/v2/balance?symbol=btc 
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `symbol` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md)

#### Response example

```javascript
{
  "balance": 1000,
  "balance_rub": 72000,
  "symbol": "btc",
  "updated_at": "2020-03-25T14:38:06.515058Z"
}
```
 <a name="rates"></a>
## Получение актуальных курсов

```http
  GET rest/v2/rates/btc?currency=rub&lot_type
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
  GET rest/v1/brokers?currency=rub&sky_pay=true
```
#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `currency` | **Required**. (rub, usd, kzt, uah, byn, tjs, azn, uzs)
| `sky_pay` | Если флаг **true**, то в response придут только те брокеры, которые поддерживают SKY PAY

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
## Получение актуального биржевого курса

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
