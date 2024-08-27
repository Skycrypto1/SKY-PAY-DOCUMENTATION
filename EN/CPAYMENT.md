
<h1 align="center">CPAYMENT API</h1>
 
[CPAYMENT creation](#cpayment)

[Obtaining information on CPAYMENT](#cpaymentinfo)

[Commissions](#commissions)

<a name="cpayment"></a>
## Creating a CPAYMENT link

```http
  POST /rest/v2/cpayments
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `currency` | `string` | **Required**. [Currencies list](CURRENCIESCPAYMENT.md)
| `amount_currency` | `number` | **Required**. Payment amount. [View information on currency limits](CURRENCIESCPAYMENT.md)
| `label` | `string` | Hash which is set by the merchant
| `lang` | `string` | Used to set the SKY PAY interface language. By default - 'ru'. [List of SKY PAY languages](SKYPAYLANGUAGES.md)

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `label` | maxLength: **256**

#### Body example

```javascript
{
  "currency": "rub",
  "amount_currency": 1000
}
```

#### Response example

```javascript
{
  "address": null,
  "amount": null,
  "amount_currency": 1000.0,
  "amount_left": 0.0,
  "amount_received": 0.0,
  "created_at": "2023-06-06T07:25:34.801763+00:00",
  "currency": "rub",
  "ended_at": null,
  "id": "0f28aad2-94b2-4911-8a2b-eccdb797ffa3",
  "label": null,
  "lang": "ru",
  "merchant_id": 186715,
  "rate": null,
  "received_crypto": 0.0,
  "status": 0,
  "symbol": null,
  "web_link": "https://skypay365.pro/cpayment/0f28aad2-94b2-4911-8a2b-eccdb797ffa3"
}
```
 <a name="cpaymentinfo"></a>
## Obtaining information on CPAYMENT

```http
  GET rest/v2/cpayments/<ID> 
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `ID` | **Required**.

#### Response example

```javascript
{
  "address": null,
  "amount": null,
  "amount_currency": 1000.0,
  "amount_left": 0.0,
  "amount_received": 0.0,
  "created_at": "2022-10-21T07:22:16.094674+00:00",
  "currency": "rub",
  "ended_at": null,
  "id": "2a5cba7d-daav-4563-aac4-f0d967bd6856",
  "label": null,
  "lang": "ru",
  "merchant_id": 18078,
  "rate": null,
  "received_crypto": 0.0,
  "status": 0,
  "symbol": null,
  "web_link": "https://skypay365.pro/cpayment/2a5cba7d-daav-4563-aac4-f0d967bd6856",
}
```

| Cpayment status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Created payment |
| `1` | Started payment |
| `2` | Successful payment |
| `3` | Expired (overdue) payment |


 <a name="commissions"></a>
## Commissions

| cryptocurrency | commision                |
| :-------- |  :------------------------- |
| `btc` | 0.000004 |
| `eth` | 0.0007  |
| `usdt` | 1 |

#### Transaction time: 2 часа
