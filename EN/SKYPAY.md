<h1 align="center">SKY PAY API</h1>
 
[Creation of SKY PAY](#skypay)

[Obtaining information on performing SKY PAY](#skypayinfo)

[SKY PAY payment statuses](#paymentStatuses)
 
<a name="skypay"></a>
## Creation of Fiat purchase redirect SKY PAY

```http
  POST /rest/v2/purchases 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `amount` | `number` | **Required**. Purchase amount. [View information on currency limits](CURRENCIES.md)
| `label` | `string` | Hash that is set by the merchant
| `symbol` | `string` | **Required**. [List of cryptocurrencies](CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [List of currencies](CURRENCIES.md)
| `is_currency_amount` | `boolean` | **Required**. for the amount in fiat – true, for the amount in crypto – false |
| `back_url` | `string` | Link to the page where the user will be redirected after a payment
| `email` | `string` | Email of the user who will make payments in SkyPay
| `broker_id` | `string` | Used to create a payment to a specific bank
| `mask` | `string` | Used to transmit the sender's card details
| `lang` | `string` | Used to set the SKY PAY interface language. By default - 'ru'. [List of SKY PAY languages](SKYPAYLANGUAGES.md)
| `valid_minutes` | `number` | Time in minutes after which the payment will have status 3. Max value - 120. By default - 120. [Payment Statuses](#paymentStatuses)


#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | minimum: **0.0001**; maximum: **100000000**
| `label` | maxLength: **256**
| `back_url` | maxLength: **256**
| `email` | maxLength: **50**

#### Body example

```javascript
{
  "amount": 1500,
  "label": "100311",
  "symbol": "btc",
  "currency": "rub",
  "is_currency_amount": true,
  "back_url": "https://myservice.com/payment/100311",
  "email": "testuser@mail.co",
  "broker_id": "ad70be25-5bb0-401f-a7a2-1f71c403cabf",
  "mask": "4728367903430821"
}
```

#### Response example

```javascript
{
  "address": "",
  "amount": 1500.0,
  "back_url": "https://myservice.com/payment/100311",
  "bot_link": "",
  "broker_id": "ad70be25-5bb0-401f-a7a2-1f71c403cabf",
  "confirmed_at": null,
  "created_at": "2023-02-23T12:23:36.989693+00:00",
  "currency": "rub",
  "email": "testuser@mail.co",
  "is_currency_amount": true,
  "label": "100311",
  "mask": "4728367903430821",
  "merchant_id": 186024,
  "payment_id": "52d27f05-0a62-40c0-8ecc-d28c9fdbb829",
  "processed_at": null,
  "received_crypto": 0.0,
  "secondary_link": "",
  "status": 0,
  "symbol": "btc",
  "token": null,
  "tx_hash": null,
  "valid_minutes": 360,
  "web_link": "https://skypay365.pro/payment/52d27f05-0a62-40c0-8ecc-d28c9fdbb829?ca=1500.0&s=btc&m=186024&l=100311",
  "lang": "ru"
}
```
 <a name="skypayinfo"></a>
## Obtaining information on performing SKY PAY

```http
  GET rest/v2/purchases/<PAYMENT_ID> 
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `PAYMENT_ID` | **Required**.

#### Response example

```javascript
{
    "address": "",
    "amount": 1000.0,
    "back_url": null,
    "bot_link": "",
    "broker_id": null,
    "confirmed_at": "2023-05-18T09:11:17.875286+00:00",
    "created_at": "2023-05-18T09:10:56.675509+00:00",
    "currency": "rub",
    "email": null,
    "is_currency_amount": true,
    "label": "",
    "lang": "ru",
    "mask": "4807-0702-9739-8133",
    "merchant_id": 186715,
    "payment_id": "0fab873b-c035-4910-ad58-2adc80515945",
    "processed_at": "2023-05-18T09:11:42.293384+00:00",
    "rate": 1654497.0,
    "received_crypto": 0.0005864,
    "secondary_link": "",
    "status": 2,
    "symbol": "btc",
    "token": null,
    "tx_hash": null,
    "valid_minutes": 360,
    "web_link": "https://skypay365.pro/payment/0fab873b-c035-4910-ad58-2adc80515945?ca=1000.0&s=btc&m=186715&l="
}
```

## SKY PAY payment statuses
<a name="paymentStatuses"></a>
| Payment status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Created payment |
| `1` | Payment in payment status |
| `2` | Successful payment |
| `3` | Failed payment |
