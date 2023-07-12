<h1 align="center">SKY SALE V2 API</h1>
 

[Создание SKY SALE V2](#skysale)

[Получение информации по выполнению SKY SALE V2](#skysaleinfo)

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
| `broker_id` | `number` | **Required**.
| `requisites` | `string` | **Required**.
| `client_order_id` | `number` | Данное поле предназначено для реализации идемпотентности.

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | minimum: **2000**; maximum: **50000**

#### Body example

```javascript
{
  "symbol": "btc",
  "amount": 10000,
  "broker_id": "f79a6e4d-0f87-45d6-bbf8-5ee3d95cc3af",
  "requisites": "test v2 requisite”
}
```

#### Response example

```javascript
{
  "amount": 10000,
  "broker_id": "f79a6e4d-0f87-45d6-bbf8-5ee3d95cc3af",
  "created_at": "2021-11-29T07:47:44.378517+00:00",
  "deal": null,
  "id": "11dcd487-9921-4c23-a19d-e00a9241a452",
  "merchant_id": 156334,
  "processed_at": null,
  "requisites": "test v2 requisite",
  "status": 0,
  "symbol": "btc"
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
  "amount": 3000,
  "broker_id": "f79a6e4d-0f87-45d6-bbf8-5ee3d95cc3af",
  "cancel_reason": null,
  "client_order_id": null,
  "created_at": "2023-06-05T12:56:22.671628+00:00",
  "deal": "hclUWgBtLS",
  "id": "3cb6d3cd-37f2-44b0-85cc-656b1a17f851",
  "merchant_id": 186715,
  "processed_at": "2023-06-05T12:57:01.956215+00:00",
  "requisites": "test v2 requisite",
  "status": 2,
  "symbol": "btc"
}
```

| Sale status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданная продажа |
| `1` | Продажа в статусе оплаты |
| `2` | Успешная продажа |
| `3` | Не успешная продажа |

