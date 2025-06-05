<h1 align="center">COMMON API</h1>
 
[Получение актуального баланса](#balance)

[Получение лучших курсов по заявкам трейдеров](#rates)

[Получение списка банков](#brokers)

[Получение биржевого курса криптовалют относительно валют](#exchange)

[Получение истории платежей](#paymentHistory)

[Статистика платежей по банкам](#brokerStatistics)

[Поиск платежей по label](#searchByLabel)

[Поиск платежей за период](#searchByPeriod)
 
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
| `currency` | Фильтрация по валюте. (rub, usd, kzt, uah, byn, tjs, azn, uzs) | rub
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
```

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
```

 <a name="brokerStatistics"></a>
## Статистика платежей по банкам

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
## Поиск платежей по label

```http
  GET rest/v2/label-search/<instance>/<label>
```

<b>Примечание: максимально возможное количество полученных записей с одинаковым label - 100.</b>

#### Parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `instance` | **Required**. Варианты: ["pay_v2", "sale_v2", "sale", "pay"].
| `label` | **Required**. Label для поиска.

 <a name="searchByPeriod"></a>
## Поиск платежей за период

```http
  GET rest/v2/merchant-report?operation_type=<op_type>&date_from=<date_from>&date_to=<date_to>
```

<b>Примечание:</b>
<b>Максимальный период - 2 месяца.</b>
<b>Формат даты - YYYY-MM-DD</b>

#### Parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `op_type` | **Required**. Варианты: [ "pay", "sale", "sale_v2", "pay_v2" ].
| `date_from` | **Required**. Дата "от" в формате YYYY-MM-DD.
| `date_to` | **Required**. Дата "до" в формате YYYY-MM-DD.

#### Response example

```javascript
[
    {
        "amount": 5000.0,
        "created_at": "2025-03-06T08:58:57.306707+00:00",
        "currency": "rub",
        "id": "ea613ef3-841e-40ab-8c4e-d73bb0c8614f",
        "processed_at": "2025-03-06T09:00:20.870920+00:00",
        "status": 2,
        "symbol": "btc"
    }
]
```
