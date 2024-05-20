<h1 align="center">WITHDRAWAL V2 API</h1>
 
[Создание WITHDRAWAL V2](#withdrawal)

[Получение информации по выполнению WITHDRAWAL V2](#withdrawalinfo)

[Комиссии](#commissions)

## Активация WITHDRAWAL V2

Перед выполнением следующих действий необходимо обратиться к администратору SKY PAY для того, чтобы он активировал Вывод v2 для интернет-площадки, предоставив ему Название.

<a name="withdrawal"></a>
## Создание WITHDRAWAL V2

```http
  POST /rest/v2/withdrawals 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbol` | `string` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md)
| `amount` | `number` | **Required**. Сумма покупки не должна быть более 6 знаков после запятой. [Лимиты по выводу криптовалют](WITHDRAWALLIMITS.md)
| `address` | `string` | **Required**. Адрес кошелька.
| `client_order_id` | `string` | Данное поле предназначено для реализации идемпотентности.

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | minimum: **0.0001**; maximum: **100000000**

#### Body example

```javascript
{
  "symbol": "usdt",
  "amount": 15,
  "address": "TYjXWvB2CVm6Nzmg3i8BVcxs5797o1cSm8"
}
```

#### Response example

```javascript
{
  "address": "TYjXWvB2CVm6Nzmg3i8BVcxs5797o1cSm8",
  "amount": 15.0,
  "client_order_id": null,
  "created_at": "2024-05-20T10:33:43.855177+00:00",
  "id": "585d6072-d70c-45ab-8c03-13c2f047d222",
  "merchant_id": 186714,
  "processed_at": null,
  "status": 1,
  "symbol": "usdt",
  "tx_hash": null
}
```
 <a name="withdrawalinfo"></a>
## Получение информации по выполнению WITHDRAWAL V2

```http
  GET rest/v2/withdrawals/<ID> 
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `ID` | **Required**.

#### Response example

```javascript
{
  "address": "TYjXWvB2CVm6Nzmg3i8BVcxs5797o1cSn7",
  "amount": 15.0,
  "client_order_id": null,
  "created_at": "2024-05-20T10:33:43.855177+00:00",
  "id": "585d6072-d70c-45ab-8c03-13c2f047d222",
  "merchant_id": 186714,
  "processed_at": null,
  "status": 2,
  "symbol": "usdt",
  "tx_hash": null
}
```

| Withdrawal status (status) | Description                |
| :-------- |  :------------------------- |
| `1` | Cозданный вывод |
| `2` | Успешный вывод  |
| `3` | Не успешный вывод |

 <a name="commissions"></a>
## Комиссии

| cryptocurrency | commision                |
| :-------- |  :------------------------- |
| `btc` | 0.0001 |
| `eth` | 0.001  |
| `usdt` | 1 |

