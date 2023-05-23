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
| `client_order_id` | `number` | Данное поле предназначено для реализации идемпотентности.

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | minimum: **0.0001**; maximum: **100000000**

#### Body example

```javascript
{
  "symbol": "btc",
  "amount": 1500,
  "address": "0x1579c0B749fAEa82A0A6FF54078F5749a8060a49"
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
  "address": "0x1579c0B749fAEa82A0A6FF54078F5749a8060a49",
  "amount": 0.03,
  "created_at": "2022-08-31T18:44:11.465405+00:00",
  "id": "7123e6af-f01b-49bf-8d95-0ce067de37fb",
  "merchant_id": 18078,
  "processed_at": null,
  "status": 2,
  "symbol": "eth"
}
```

| Withdrawal status (status) | Description                |
| :-------- |  :------------------------- |
| `1` | Cозданный вывод |
| `2` | Успешный вывод  |
| `3` | не успешный вывод |

 <a name="commissions"></a>
## Комиссии

| cryptocurrency | commision                |
| :-------- |  :------------------------- |
| `btc` | 0.0001 |
| `eth` | 0.001  |
| `usdt` | 1 |

