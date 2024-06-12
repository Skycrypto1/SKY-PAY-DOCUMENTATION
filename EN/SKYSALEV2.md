<h1 align="center">SKY SALE V2 API</h1>
 

[Creation of SKY SALE V2](#skysale)

[Obtaining information on performing SKY SALE V2](#skysaleinfo)

[SKY SALE V2 payment statuses](#paymentStatuses)

 <a name="skysale"></a>
## Creation of SKY SALE V2

```http
  POST /rest/v2/sale_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
`symbol` | `string` | **Required**. [List of cryptocurrencies](CRYPTOCURRENCIES.md)
| `amount` | `number` | **Required**. Sale amount RUB.
| `label` | `string` | Hash which is set by the merchant
| `broker_id` | `string` | **Required**.
| `requisites` | `string` | **Required**.
| `is_currency_amount` | `boolean` | **Required**. for the amount in fiat – true, for the amount in crypto – false
| `currency` | `string` | By default - 'rub'. [List of currencies](CURRENCIES_SALES.md)
| `client_order_id` | `string` | This field is intended to implement idempotency.
| `lang` | `string` | Used to set the SKY SALE V2 interface language. By default - 'ru'. [List of languages ​​SKY SALE V2](SKYPAYLANGUAGES.md)
| `valid_minutes` | `number` | Time in minutes after which the payment will have status 3. Max value - 120. By default - 120. [Payment Statuses](#paymentStatuses)

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | minimum: **2000**; maximum: **50000**
| `label` | maxLength: **256**

#### Body example

```javascript
{
  "symbol": "btc",
  "amount": 10000,
  "is_currency_amount": true,
  "broker_id": "f79a6e4d-0f87-45d6-bbf8-5ee3d95cc3af",
  "requisites": "test v2 requisite",
  "currency": "rub"
}
```

#### Response example

```javascript
{
  "amount": 2000,
  "broker_id": "fd70be25-5bb0-401f-a7a2-1f71c403caba",
  "cancel_reason": null,
  "client_order_id": null,
  "created_at": "2023-08-16T11:11:55.772941+00:00",
  "currency": "rub",
  "deal": null,
  "id": "41f1acd0-db1c-456b-9b1d-c7bc2148e134",
  "merchant_id": 186714,
  "is_currency_amount": true,
  "processed_at": null,
  "requisites": "test v2 requisite",
  "sent_crypto": 0.0,
  "status": 0,
  "label": null,
  "symbol": "usdt",
  "valid_minutes": 360,
  "lang": "ru"
}
```
 <a name="skysaleinfo"></a>
## Obtaining information on performing SKY SALE V2

```http
  GET rest/v2/sale_v2/<ID> 
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `ID` | **Required**.

#### Response example

```javascript
{
  "amount": 2000,
  "broker_id": "fd70be25-5bb0-401f-a7a2-1f71c403caba",
  "cancel_reason": null,
  "client_order_id": null,
  "created_at": "2023-08-16T11:11:55.772941+00:00",
  "currency": "rub",
  "lang": "ru"
  "deal": "FdvgWIDl0Q",
  "id": "41f1acd0-db1c-456b-9b1d-c7bc2148e134",
  "merchant_id": 186714,
  "is_currency_amount": true,
  "processed_at": "2023-08-16T11:12:39.206570+00:00",
  "requisites": "test v2 requisite",
  "sent_crypto": 21.00665569,
  "label": null,
  "status": 2,
  "symbol": "usdt",
  "valid_minutes": 360
}
```

## Статусы платежей SKY SALE V2
 <a name="paymentStatuses"></a>
| Sale status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Created sale |
| `1` | Sale in payment status |
| `2` | Successful sale |
| `3` | Not a successful sale |

