<h1 align="center">SkySale v2 API</h1>
 

[Создание SkySale v2](#skysale)

[Получение информации по выполнению SkySale v2](#skysaleinfo)

 <a name="skysale"></a>
## Создание SkySale v2

```http
  POST /rest/v2/sale_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbol` | `string` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md)
| `amount` | `number` | **Required**. Сумма покупки. [Посмотреть информацию по лимитам валют](CURRENCIES_SALES.md)
| `broker_id` | `number` | **Required**.
| `requisites` | `string` | **Required**.

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
## Получение информации по выполнению SkySale v2

```http
  GET rest/v2/sale_v2/<SALE_ID> 
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `SALE_ID` | **Required**.

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

| Sale status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданная продажа |
| `1` | Продажа в статусе оплаты |
| `2` | Успешная продажа |
| `3` | Не успешная продажа |

