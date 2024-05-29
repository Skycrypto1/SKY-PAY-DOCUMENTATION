<h1 align="center">SKY SALE V2 API</h1>
 

[Создание SKY SALE V2](#skysale)

[Получение информации по выполнению SKY SALE V2](#skysaleinfo)

[Статусы платежей SKY SALE V2](#paymentStatuses)

 <a name="skysale"></a>
## Создание SKY SALE V2

```http
  POST /rest/v2/sale_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
 `symbol` | `string` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md)
| `amount` | `number` | **Required**. Сумма продажи RUB.
| `label` | `string` | Hash который задаётся мерчантом
| `broker_id` | `string` | **Required**.
| `requisites` | `string` | **Required**.
| `is_currency_amount` | `boolean` | **Required**. для суммы в фиате – true, для суммы в крипте – false 
| `currency` | `string` | По дефолту - 'rub'. [Список валют](CURRENCIES_SALES.md)
| `client_order_id` | `string` | Данное поле предназначено для реализации идемпотентности.
| `lang` | `string` | Используется для установки языка интерфейса SKY SALE V2. По дефолту - 'ru'. [Список языков SKY SALE V2](SKYPAYLANGUAGES.md)
| `valid_minutes` | `number` | Время в минутах, через которое у платежа будет 3 статус. По дефолту - 360. [Статусы платежей](#paymentStatuses)

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
  "requisites": "test v2 requisite”,
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
  "symbol": "usdt",
  "valid_minutes": 360,
  "lang": "ru"
}
```
 <a name="skysaleinfo"></a>
## Получение информации по выполнению SKY SALE V2

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
  "status": 2,
  "symbol": "usdt",
  "valid_minutes": 360
}
```

## Статусы платежей SKY SALE V2
 <a name="paymentStatuses"></a>
| Sale status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданная продажа |
| `1` | Продажа в статусе оплаты |
| `2` | Успешная продажа |
| `3` | Не успешная продажа |

