<h1 align="center">SKY SALE API</h1>
 

[Creation of SKY SALE](#skysale)

[Obtaining information on performing SKY SALE](#skysaleinfo)

[SKY SALE payment statuses](#paymentStatuses)

 <a name="skysale"></a>
## Creation of SKY SALE

```http
  POST /rest/v2/sells 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `amount` | `number` | **Required**. Purchase amount. [View information on currency limits](CURRENCIES_SALES.md)
| `label` | `string` | Hash which is set by the merchant
| `symbol` | `string` | **Required**. [List of cryptocurrencies](CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [List of currencies](CURRENCIES_SALES.md)
| `is_currency_amount` | `boolean` | **Required**. for the amount in fiat – true, for the amount in crypto – false
| `back_url` | `string` | Link to the page where the user will be redirected after payment
| `lang` | `string` | Used to set the SKY PAY interface language. By default - 'ru'. [List of SKY PAY languages](SKYPAYLANGUAGES.md)
| `valid_minutes` | `number` | Time in minutes after which the payment will have status 3. Max value - 120. By default - 120. [Payment Statuses](#paymentStatuses)

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | minimum: **0.0001**; maximum: **100000000**
| `label` | maxLength: **256**
| `back_url` | maxLength: **256**

#### Body example

```javascript
{
  "amount": 10000,
  "label": "100311",
  "symbol": "btc",
  "is_currency_amount": true,
  "currency": "rub",
  "back_url": "https://myservice.com/payment/100311"
}
```

#### Response example

```javascript
{
  "amount": 10000,
  "created_at": "2023-02-23T13:39:02.144538+00:00",
  "currency": "rub",
  "email": null,
  "is_currency_amount": true,
  "id": "8392d915-668b-4ff3-9b02-45ead91c4d43",
  "is_approved": false,
  "label": "100311",
  "merchant_id": 186024,
  "processed_at": null,
  "status": 0,
  "symbol": "btc",
  "web_link": "https://skypay365.pro/sale/8392d915-668b-4ff3-9b02-45ead91c4d43?ca=10000&s=btc&m=186024&l=100311",
  "back_url": "https://myservice.com/payment/100311",
  "lang": "ru",
  "valid_minutes": 360,
  "requisite": null
}
```
Confirmation of withdrawal of funds is an operation on the internal SKY API. If there is a merchant balance, a temporary user is created to whom the funds are transferred. When clicking on the link, the client creates a transaction to sell cryptocurrency, which was debited from the merchant’s account. If after an hour there is no active sale transaction from this account, the funds are returned to the merchant’s balance.

 <a name="skysaleinfo"></a>
## Obtaining information on performing SKY SALE

```http
  GET rest/v2/sells/<ID> 
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `ID` | **Required**.

#### Response example

```javascript
{
  "amount": 10000,
  "created_at": "2023-02-23T13:41:45.024091+00:00",
  "currency": "rub",
  "email": "6f4c708755c445b@noemail.fkfl",
  "id": "d9a9312e-78fc-4d99-9baf-8b6c0a7493d6",
  "is_currency_amount": true,
  "is_approved": true,
  "label": "100311",
  "merchant_id": 186024,
  "processed_at": null,
  "status": 0,
  "symbol": "btc",
  "web_link": "https://skypay365.pro/sale/d9a9312e-78fc-4d99-9baf-8b6c0a7493d6?ca=10000&s=btc&m=186024&l=100311",
  "lang": "ru",
  "valid_minutes": 360,
  "requisite": "4382 6357 6372 8212"
}
```

## Статусы платежей SKY SALE
 <a name="paymentStatuses"></a>
| Sale status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Created sale |
| `1` | Sale in payment status |
| `2` | Successful sale |
| `3` | Not a successful sale |
