<h1 align="center">SKY PAY API</h1>
 
[Создание SKY PAY](#skypay)

[Получение информации по выполнению SKY PAY](#skypayinfo)

[Статусы платежей SKY PAY](#paymentStatuses)
 
<a name="skypay"></a>
## Создание Fiat purchase redirect SKY PAY

```http
  POST /rest/v2/purchases 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `amount` | `number` | **Required**. Сумма покупки. [Посмотреть информацию по лимитам валют](CURRENCIES.md)
| `label` | `string` | Hash который задается мерчантом
| `symbol` | `string` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [Список валют](CURRENCIES.md)
| `is_currency_amount` | `boolean` | **Required**. для суммы в фиате – true, для суммы в крипте – false |
| `back_url` | `string` | Cсылка на страницу, куда будет перенаправлен пользователь после успешного платежа
| `email` | `string` | Email пользователя, который будет проводить оплату в SkyPay
| `broker_id` | `string` | Используется для создания платежа на определенный банк
| `mask` | `string` | Используется для передачи реквизитов карты отправителя
| `lang` | `string` | Используется для установки языка интерфейса SKY PAY. По дефолту - 'ru'. [Список языков SKY PAY](SKYPAYLANGUAGES.md)
| `valid_minutes` | `number` | Время в минутах, через которое у платежа будет 3 статус. По дефолту - 360. [Статусы платежей](#paymentStatuses)


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
    "web_link": "http://qpay.sky-crypto.com/payment/0fab873b-c035-4910-ad58-2adc80515945?ca=1000.0&s=btc&m=186715&l="
}
```

## Статусы платежей SKY PAY
<a name="paymentStatuses"></a>
| Payment status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданный платеж |
| `1` | Платеж в статусе оплаты |
| `2` | Успешный платеж |
| `3` | Не успешный платеж |
