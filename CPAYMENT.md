
<h1 align="center">Cpayment API</h1>
 
[Создание Cpayment](#cpayment)

[Получение информации по Оплате криптовалютой Cpayment](#cpaymentinfo)

<a name="cpayment"></a>
## Создание ссылки на Оплату криптовалютой (Cpayment)

```http
  POST /rest/v2/cpayment 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `currency` | `string` | **Required**. [Список валют](CURRENCIESCPAYMENT.md)
| `amount_currency` | `number` | **Required**. Сумма оплаты. [Посмотреть информацию по лимитам валют](CURRENCIESCPAYMENT.md)

#### Body example

```javascript
{
  "address": null,
  "amount": null,
  "amount_currency": 1000.0,
  "created_at": "2022-10-21T07:22:16.094674+00:00",
  "currency": "rub",
  "ended_at": null,
  "id": "2a5cba7d-daav-4563-aac4-f0d967bd6856",
  "merchant_id": 18078,
  "rate": null,
  "received_crypto": 0.0,
  "status": 0,
  "symbol": null,
  "web_link": "http://qpay.sky-crypto.com/cpayment/2a5cba7d-daav-4563-aac4-f0d967bd6856"
}
```

#### Response example

```javascript
{
  "address": "0x1579c0B749fAEa82A0A6FF54078F5749a8060a49",
  "amount": 0.03,
  "created_at": "2022-08-31T18:44:11.465405+00:00",
  "id": "7123e6af-f01b-49bf-8d95-0ce067de37fb",
  "merchant_id": 18078,
  "processed_at": null,
  "status": 1,
  "symbol": "eth"
}
```
 <a name="cpaymentinfo"></a>
## Получение информации по Оплате криптовалютой (Cpayment)

```http
  GET rest/v2/cpeyments/<ID> 
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
  "created_at": "2022-10-21T07:22:16.094674+00:00",
  "currency": "rub",
  "ended_at": null,
  "id": "2a5cba7d-daav-4563-aac4-f0d967bd6856",
  "merchant_id": 18078,
  "rate": null,
  "received_crypto": 0.0,
  "status": 0,
  "symbol": null,
  "web_link": "http://qpay.sky-crypto.com/cpayment/2a5cba7d-daav-4563-aac4-f0d967bd6856"
}
```

| Cpayment status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданный платеж |
| `1` | Начатый платеж |
| `2` | Успешный платеж  |
| `3` | истекший (просроченный) платеж |
