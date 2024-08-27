To integrate FlashPay on the site, you must specify a link to FlashPay in the iframe, for example:

**Reception**: <iframe src='https://skycrypto.shop/flashpay/payment/{id}' />

**Payout**: <iframe src='https://skycrypto.shop/flashpay/sale/{id}' />


<h1 align="center">Reception</h1>
 
[Reception creating](#flashpay)

[Obtaining information on performing a reception](#flashpayinfo)

[Confirmation of sending fiat](#confirmation)

[Acceptance payment statuses](#paymentStatuses)

<a name="flashpay"></a>
## Reception creating

```http
  POST /rest/v2/payments_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `is_flash` | `number` | **Required**. To create a reception, this field must have the value **true**.
| `amount` | `number` | **Required**. Purchase amount. [View information on currency limits](CURRENCIES.md)
| `label` | `string` | Hash which is set by the merchant
| `symbol` | `string` | **Required**. [Cryptocurrencies list](FLASHPAY_CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [Currencies list](CURRENCIES.md)
| `is_currency_amount` | `boolean` | **Required**. For Flash Pay the value must be true
| `lang` | `string` | Used to set the FlashPay interface language. By default - 'ru'. [List of FlashPay languages](SKYPAYLANGUAGES.md)
| `broker_id` | `string` | Used to create a payment to a specific bank. [List of banks](FLASHPAY_BROKERS.md)
| `valid_minutes` | `number` | Time in minutes after which the payment will have status 3. Max value - 120. By default - 120. [Payment Statuses](#paymentStatuses)
| `client_name` | `string` | Client's full name.
| `client_email` | `string` | Client's email.

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | minimum: **0.0001**; maximum: **100000000**
| `label` | maxLength: **256**
| `client_name` | maxLength: **64**
| `client_email` | maxLength: **64**

#### Body example

```javascript
{
  "amount": 1500,
  "label": "100311",
  "symbol": "usdt",
  "currency": "rub",
  "is_flash": true,
  "is_currency_amount": true,
  "broker_id": "ad70be25-5bb0-401f-a7a2-1f71c403cabf",
  "client_name": "Stan Smith",
  "client_email": "test@mail.co"
}
```

#### Response example

```javascript
{
  "amount": 450.0,
  "broker_id": "efc65f1a-484a-4297-b192-3cf199e38e52",
  "confirmed_at": null,
  "created_at": "2023-01-23T09:40:25.147586+00:00",
  "currency": "rub",
  "deal": null,
  "fiat_sent": false,
  "id": "6e7e9421-9e08-4ecd-93c8-abc3559642bc",
  "is_currency_amount": true,
  "label": "642002",
  "lang": "ru",
  "merchant_id": 120222,
  "processed_at": null,
  "received_crypto": 0.0,
  "requisites": null,
  "status": 0,
  "symbol": "usdt",
  "valid_minutes": 360,
  "client_name": "Stan Smith",
  "client_email": "test@mail.co",
  "web_link": "https://skypay365.pro/flashpay/payment/b5a3f8be-f3e8-431d-bf15-9a632fcf8e14",
  "rate": 3850026.30
}
```
 <a name="flashpayinfo"></a>
## Obtaining information on performing a reception

```http
  GET rest/v2/payments_v2/<ID> 
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `ID` | **Required**.

#### Response example

```javascript
{
  "amount": 450.0,
  "broker_id": "efc65f1a-484a-4297-b192-3cf199e38e52",
  "confirmed_at": null,
  "created_at": "2023-01-23T09:40:25.147586+00:00",
  "currency": "rub",
  "deal": null,
  "fiat_sent": false,
  "id": "6e7e9421-9e08-4ecd-93c8-abc3559642bc",
  "is_currency_amount": true,
  "label": "642002",
  "merchant_id": 120222,
  "processed_at": null,
  "received_crypto": 0.0,
  "requisites": 4452773861241948,
  "status": 1,
  "lang": "ru",
  "symbol": "usdt",
  "valid_minutes": 360,
  "client_name": "Stan Smith",
  "client_email": "test@mail.co",
  "web_link": "https://skypay365.pro/flashpay/payment/b5a3f8be-f3e8-431d-bf15-9a632fcf8e14",
  "rate": 3850026.30
}
```

 <a name="paymentStatuses"></a>
## Acceptance payment statuses
| Payment status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Created payment |
| `1` | Payment in payment status |
| `2` | Successful payment |
| `3` | Failed payment |

 <a name="confirmation"></a>
## Confirmation of sending fiat

```http
  PATCH /rest/v2/payments_v2/<ID>/update
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `ID` | **Required**.

#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `fiat_sent` | `boolean` | **Required**. 

#### Body example

```javascript
{
  "fiat_sent": true,
}
```

#### Response example

```javascript
{
  "success": "\"fiat_sent\" updated"
}
```

<h1 align="center">Payout</h1>
 

[Payout creating](#flashsale)

[Receiving information on making a payment](#flashsaleinfo)

[Payment statuses](#paymentStatuses)

 <a name="flashsale"></a>
## Payout creating

```http
  POST /rest/v2/sale_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `is_flash` | `boolean` | **Required**. To create a payout, this field must have the value **true**.
 `symbol` | `string` | **Required**. [List of cryptocurrencies](FLASHPAY_CRYPTOCURRENCIES.md)
| `amount` | `number` | **Required**. Sale amount RUB.
| `broker_id` | `string` | **Required**. [List of banks](FLASHPAY_BROKERS.md)
| `requisites` | `string` | **Required**.
| `is_currency_amount` | `boolean` | **Required**. for the amount in fiat – true, for the amount in crypto – false
| `lang` | `string` | Used to set the FlashSale interface language. By default - 'ru'. [List of FlashSale languages](SKYPAYLANGUAGES.md)
 | `currency` | `string` | By default - 'rub'. [List of currencies](CURRENCIES_SALES.md)
| `client_order_id` | `number` | This field is intended to implement idempotency.
| `valid_minutes` | `number` | Time in minutes after which the payment will have status 3. Max value - 120. By default - 120. [Payment Statuses](#paymentStatuses)

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | minimum: **2000**; maximum: **50000**

#### Body example

```javascript
{
  "symbol": "usdt",
  "is_flash": true,
  "amount": 10000,
  "is_currency_amount": true,
  "broker_id": "f79a6e4d-0f87-45d6-bbf8-5ee3d95cc3af",
  "requisites": "test flash sale requisite”,
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
  "lang": "ru",
  "symbol": "usdt",
  "valid_minutes": 360,
  "web_link": "https://skypay365.pro/flashpay/sale/ce7c423e-1a38-449a-a80d-a24886e96153",
}
```
 <a name="flashsaleinfo"></a>
## Receiving information on making a payment

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
  "lang": "ru",
  "deal": "FdvgWIDl0Q",
  "id": "41f1acd0-db1c-456b-9b1d-c7bc2148e134",
  "merchant_id": 186714,
  "is_currency_amount": true,
  "processed_at": "2023-08-16T11:12:39.206570+00:00",
  "requisites": "test v2 requisite",
  "sent_crypto": 21.00665569,
  "status": 2,
  "symbol": "usdt",
  "valid_minutes": 360,
  "web_link": "https://skypay365.pro/flashpay/sale/ce7c423e-1a38-449a-a80d-a24886e96153",
}
```

## Payment statuses
 <a name="paymentStatuses"></a>
| Sale status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Created sale |
| `1` | Sale in payment status |
| `2` | Successful sale |
| `3` | Not a successful sale |


