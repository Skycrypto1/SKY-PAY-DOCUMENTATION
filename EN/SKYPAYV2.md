<h1 align="center">SKY PAY V2 API</h1>
 
[Creation of SKY PAY V2](#skypay)

[Obtaining information on the implementation of SKY PAY V2](#skypayinfo)

[Confirmation of sending fiat](#confirmation)

[SKY PAY V2 payment statuses](#paymentStatuses)

[SKY PAY V2 payment cancel](#paymentCancel)

<a name="skypay"></a>
## Creation of SKY PAY V2

```http
  POST /rest/v2/payments_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `amount` | `number` | **Required**. Purchase amount. [View information on currency limits](CURRENCIES.md)
| `label` | `string` | **Required**. Hash that is set by the merchant
| `symbol` | `string` | **Required**. [List of cryptocurrencies](CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [List of currencies](CURRENCIES.md)
| `is_currency_amount` | `boolean` | **Required**. for the amount in fiat – true, for the amount in crypto – false |
| `broker_id` | `string` | **Required**. Used to create a payment to a specific bank
| `valid_minutes` | `number` | Time in minutes after which the payment will have status 3. By default - 360. [Payment Statuses](#paymentStatuses)
| `client_name` | `string` | Client's full name.
| `client_email` | `string` | Client's email.
| `lang` | `string` | Used to set the SKY PAY V2 interface language. By default - 'ru'. [List of languages ​​SKY PAY V2](SKYPAYLANGUAGES.md)

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
  "symbol": "btc",
  "currency": "rub",
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
  "merchant_id": 120222,
  "processed_at": null,
  "received_crypto": 0.0,
  "requisites": null,
  "status": 0,
  "symbol": "btc",
  "valid_minutes": 360,
  "client_name": "Stan Smith",
  "client_email": "test@mail.co",
  "lang": "ru",
  "rate": 3850026.30
}
```
 <a name="skypayinfo"></a>
## Obtaining information on the implementation of SKY PAY V2

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
  "symbol": "btc",
  "valid_minutes": 360,
  "client_name": "Stan Smith",
  "client_email": "test@mail.co",
  "rate": 3850026.30
}
```

 <a name="paymentStatuses"></a>
## SKY PAY V2 payment statuses
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

 <a name="paymentCancel"></a>
## Payment Cancel SKY PAY V2

```http
  PATCH /rest/v2/payments_v2/<ID>/cancel
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `ID` | **Required**.

#### Response example

```javascript
{
  "success": true
}
```
