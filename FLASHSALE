<h1 align="center">FLASH SALE API</h1>
 

[Создание FLASH SALE](#flashsale)

[Получение информации по выполнению SKY SALE V2](#flashsaleinfo)

[Статусы платежей FLASH SALE](#paymentStatuses)

 <a name="flashsale"></a>
## Создание FLASH SALE

```http
  POST /rest/v2/sale_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `is_flash` | `boolean` | **Required**. Поле должно быть со значением **true**. 
 `symbol` | `string` | **Required**. [Список криптовалют](FLASHPAY_CRYPTOCURRENCIES.md)
| `amount` | `number` | **Required**. Сумма продажи RUB.
| `broker_id` | `string` | **Required**. [Список банков](FLASHPAY_BROKERS.md)
| `requisites` | `string` | **Required**.
| `client_order_id` | `number` | Данное поле предназначено для реализации идемпотентности.
| `valid_minutes` | `number` | Время в минутах, через которое у платежа будет 3 статус. По дефолту - 360. [Статусы платежей](#paymentStatuses)

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
  "broker_id": "f79a6e4d-0f87-45d6-bbf8-5ee3d95cc3af",
  "requisites": "test flash sale requisite”
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
  "deal": null,
  "id": "41f1acd0-db1c-456b-9b1d-c7bc2148e134",
  "merchant_id": 186714,
  "processed_at": null,
  "requisites": "test v2 requisite",
  "sent_crypto": 0.0,
  "status": 0,
  "symbol": "usdt",
  "is_flash": true,
  "valid_minutes": 360
}
```
 <a name="flashsaleinfo"></a>
## Получение информации по выполнению FLASH SALE

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
  "deal": "FdvgWIDl0Q",
  "id": "41f1acd0-db1c-456b-9b1d-c7bc2148e134",
  "merchant_id": 186714,
  "processed_at": "2023-08-16T11:12:39.206570+00:00",
  "requisites": "test v2 requisite",
  "sent_crypto": 21.00665569,
  "status": 2,
  "symbol": "usdt",
  "is_flash": true,
  "valid_minutes": 360
}
```

## Статусы платежей FLASH SALE
 <a name="paymentStatuses"></a>
| Sale status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданная продажа |
| `1` | Продажа в статусе оплаты |
| `2` | Успешная продажа |
| `3` | Не успешная продажа |

