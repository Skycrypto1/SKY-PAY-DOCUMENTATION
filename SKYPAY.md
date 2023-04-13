<h1 align="center">SKY PAY API</h1>
 
[Создание SKY PAY](#skypay)

[Получение информации по выполнению SKY PAY](#skypayinfo)
 
<a name="skypay"></a>
## Создание Fiat purchase redirect SKY PAY

```http
  POST /rest/v2/purchases 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `amount` | `number` | **Required**. Сумма покупки. [Посмотреть информацию по лимитам валют](CURRENCIES.md)
| `label` | `number` | **Required**. Hash который заедается мерчантом
| `symbol` | `string` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [Список валют](CURRENCIES.md)
| `is_currency_amount` | `boolean` | **Required**. для суммы в рублях – true, для суммы в крипте – false |
| `back_url` | `string` | Cсылка на страницу, куда будет перенаправлен пользователь после успешного платежа
| `email` | `string` | Email пользователя, который будет проводить оплату в SkyPay
| `broker_id` | `string` | Используется для создания платежа на определенный банк
| `mask` | `string` | Используется для передачи реквизитов карты отправителя
| `lang` | `string` | Используется для установки языка интерфейса SKY PAY. По дефолту - 'ru'. [Список языков SKY PAY](SKYPAYLANGUAGES.md)

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
  "broker_id": "ad70be25-5bb0-401f-a7a2-1f71c403cabf"
  "mask": "4728367903430821",
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
  "valid_minutes": 1440,
  "web_link": "http://qpay.sky-crypto.com/payment/52d27f05-0a62-40c0-8ecc-d28c9fdbb829?ca=1500.0&s=btc&m=186024&l=100311",
  "lang": "ru"
}
```
 <a name="skypayinfo"></a>
## Получение информации по выполнению SKY PAY

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
    "amount": 1500.0,
    "back_url": "https://myservice.com/payment/100311",
    "bot_link": "",
    "broker_id": "ad70be25-5bb0-401f-a7a2-1f71c403cabf",
    "confirmed_at": null,
    "created_at": "2023-02-23T12:39:59.084786+00:00",
    "currency": "rub",
    "email": "testuser@mail.co",
    "is_currency_amount": true,
    "label": "100311",
    "mask": null,
    "merchant_id": 186024,
    "payment_id": "4499c16d-13b6-43cc-bc24-af2cd4ac1563",
    "processed_at": null,
    "received_crypto": 0.0,
    "secondary_link": "",
    "status": 0,
    "symbol": "btc",
    "token": null,
    "tx_hash": null,
    "valid_minutes": 1440,
    "web_link": "http://qpay.sky-crypto.com/payment/4499c16d-13b6-43cc-bc24-af2cd4ac1563?ca=1500.0&s=btc&m=186024&l=100311",
    "lang": "ru"
}
```

| Payment status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданный платеж |
| `1` | Платеж в статусе оплаты |
| `2` | Успешный платеж |
| `3` | Не успешный платеж |
