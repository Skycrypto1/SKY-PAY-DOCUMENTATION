<h1 align="center">FLASH PAY API</h1>
 
[Создание FLASH PAY](#flashpay)

[Получение информации по выполнению FLASH PAY](#flashpayinfo)

[Подтверждение отправки фиата](#confirmation)

[Статусы платежей FLASH PAY](#paymentStatuses)

<a name="flashpay"></a>
## Создание FLASH PAY

```http
  POST /rest/v2/payments_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `is_flash` | `number` | **Required**. Для создания FLASH PAY данное поле должно быть **true**. [Посмотреть информацию по лимитам валют](CURRENCIES.md)
| `amount` | `number` | **Required**. Сумма покупки. [Посмотреть информацию по лимитам валют](CURRENCIES.md)
| `label` | `string` | **Required**. Hash который заедается мерчантом
| `symbol` | `string` | **Required**. [Список криптовалют](FLASHPAY_CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [Список валют](CURRENCIES.md)
| `is_currency_amount` | `boolean` | **Required**. для суммы в рублях – true, для суммы в крипте – false |
| `broker_id` | `string` | Используется для создания платежа на определенный банк
| `valid_minutes` | `number` | Время в минутах, через которое у платежа будет 3 статус. По дефолту - 360. [Статусы платежей](#paymentStatuses)

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | minimum: **0.0001**; maximum: **100000000**
| `label` | maxLength: **256**

#### Body example

```javascript
{
  "amount": 1500,
  "label": "100311",
  "symbol": "usdt",
  "currency": "rub",
  "is_flash": true,
  "is_currency_amount": true,
  "broker_id": "ad70be25-5bb0-401f-a7a2-1f71c403cabf"
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
  "merchant_id": 120222,
  "processed_at": null,
  "received_crypto": 0.0,
  "requisites": null,
  "status": 0,
  "symbol": "usdt",
  "valid_minutes": 360
}
```
 <a name="flashpayinfo"></a>
## Получение информации по выполнению FLASH PAY

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
  "is_flash": true,
  "label": "642002",
  "merchant_id": 120222,
  "processed_at": null,
  "received_crypto": 0.0,
  "requisites": 4452773861241948,
  "status": 1,
  "symbol": "usdt",
  "valid_minutes": 360
}
```

 <a name="paymentStatuses"></a>
## Статусы платежей FLASH PAY
| Payment status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданный платеж |
| `1` | Платеж в статусе оплаты |
| `2` | Успешный платеж |
| `3` | Не успешный платеж |

 <a name="сonfirmation"></a>
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

