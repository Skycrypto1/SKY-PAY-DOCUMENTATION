Для интеграции FlashPay на сайте необходимо указать ссылку на FlashPay в iframe, к примеру:

**Приём**: <iframe src='https://skycrypto.shop/flashpay/payment/{id}' />

**Выплата**: <iframe src='https://skycrypto.shop/flashpay/sale/{id}' />


<h1 align="center">Приём</h1>
 
[Создание приёма](#flashpay)

[Получение информации по выполнению приёма](#flashpayinfo)

[Подтверждение отправки фиата](#confirmation)

[Статусы платежей приёма](#paymentStatuses)

<a name="flashpay"></a>
## Создание приёма

```http
  POST /rest/v2/payments_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `is_flash` | `boolean` | **Required**. Для создания приёма данное поле должно быть со значением **true**.
| `amount` | `number` | **Required**. Сумма покупки. [Посмотреть информацию по лимитам валют](CURRENCIES.md)
| `label` | `string` | Hash который задается мерчантом
| `symbol` | `string` | **Required**. [Список криптовалют](FLASHPAY_CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [Список валют](CURRENCIES.md)
| `is_currency_amount` | `boolean` | **Required**. Для Flash Pay значение должно быть true
| `lang` | `string` | Используется для установки языка интерфейса FlashPay. По дефолту - 'ru'. [Список языков FlashPay](SKYPAYLANGUAGES.md). Получить id можно по запросу на [эндпоинт списка банков](COMMON.md#brokers)
| `broker_id` | `string` | Используется для создания платежа на определенный банк. [Список банков](FLASHPAY_BROKERS.md)
| `valid_minutes` | `number` | Время в минутах, через которое у платежа будет 3 статус. Максимальное значение - 120. По дефолту - 120. [Статусы платежей](#paymentStatuses)
| `client_name` | `string` | ФИО клиента.
| `client_email` | `string` | E-mail клиента.

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
## Получение информации по выполнению приёма

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
## Статусы платежей приёма
| Payment status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданный платеж |
| `1` | Платеж в статусе оплаты |
| `2` | Успешный платеж |
| `3` | Не успешный платеж |

 <a name="confirmation"></a>
## Подтверждение отправки фиата

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

<h1 align="center">Выплата</h1>
 

[Создание выплаты](#flashsale)

[Получение информации по выполнению выплаты](#flashsaleinfo)

[Статусы платежей выплат](#paymentStatuses)

 <a name="flashsale"></a>
## Создание выплаты

```http
  POST /rest/v2/sale_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `is_flash` | `boolean` | **Required**. Для создания выплаты данное поле должно быть со значением **true**.
 `symbol` | `string` | **Required**. [Список криптовалют](FLASHPAY_CRYPTOCURRENCIES.md)
| `amount` | `number` | **Required**. Сумма продажи RUB.
| `broker_id` | `string` | **Required**. [Список банков](FLASHPAY_BROKERS.md). Получить id можно по запросу на [эндпоинт списка банков](COMMON.md#brokers)
| `label` | `string` | Hash который задается мерчантом
| `requisites` | `string` | **Required**.
| `is_currency_amount` | `boolean` | **Required**. для суммы в фиате – true, для суммы в крипте – false 
| `lang` | `string` | Используется для установки языка интерфейса FlashSale. По дефолту - 'ru'. [Список языков FlashSale](SKYPAYLANGUAGES.md)
 | `currency` | `string` | По дефолту - 'rub'. [Список валют](CURRENCIES_SALES.md)
| `client_order_id` | `number` | Данное поле предназначено для реализации идемпотентности.
| `valid_minutes` | `number` | Время в минутах, через которое у платежа будет 3 статус. Максимальное значение - 120. По дефолту - 120. [Статусы платежей](#paymentStatuses)

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
## Получение информации по выполнению выплаты

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

## Статусы платежей выплаты
 <a name="paymentStatuses"></a>
| Sale status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданная продажа |
| `1` | Продажа в статусе оплаты |
| `2` | Успешная продажа |
| `3` | Не успешная продажа |


