<h1 align="center">SKY PAY V2 API</h1>
 
[Создание SKY PAY V2](#skypay)

[Получение информации по выполнению SKY PAY V2](#skypayinfo)

[Подтверждение отправки фиата](#confirmation)

[Статусы платежей SKY PAY V2](#paymentStatuses)

[Отмена платежа SKY PAY V2](#paymentCancel)

<a name="skypay"></a>
## Создание SKY PAY V2

```http
  POST /rest/v2/payments_v2 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `amount` | `number` | **Required**. Сумма покупки. [Посмотреть информацию по лимитам валют](CURRENCIES.md)
| `label` | `string` | Hash который заедается мерчантом
| `symbol` | `string` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [Список валют](CURRENCIES.md)
| `is_currency_amount` | `boolean` | **Required**. для суммы в фиате – true, для суммы в крипте – false |
| `broker_id` | `string` |  **Required**. Используется для создания платежа на определенный банк
| `valid_minutes` | `number` | Время в минутах, через которое у платежа будет 3 статус. Максимальное значение - 120. По дефолту - 120. [Статусы платежей](#paymentStatuses)
| `client_name` | `string` | ФИО клиента.
| `client_email` | `string` | E-mail клиента.
| `lang` | `string` | Используется для установки языка интерфейса SKY PAY V2. По дефолту - 'ru'. [Список языков SKY PAY V2](SKYPAYLANGUAGES.md)

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
  "symbol": "btc",
  "currency": "rub",
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
  "merchant_id": 120222,
  "processed_at": null,
  "received_crypto": 0.0,
  "requisites": null,
  "status": 0,
  "symbol": "btc",
  "valid_minutes": 360,
  "client_name": "Stan Smith",
  "client_email": "test@mail.co",
  "lang": "ru",
  "rate": 3850026.30
}
```
 <a name="skypayinfo"></a>
## Получение информации по выполнению SKY PAY V2

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
  "symbol": "btc",
  "valid_minutes": 360,
  "client_name": "Stan Smith",
  "client_email": "test@mail.co",
  "rate": 3850026.30
}
```

 <a name="paymentStatuses"></a>
## Статусы платежей SKY PAY V2
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
  "fiat_sent": true
}
```

#### Response example

```javascript
{
  "success": "\"fiat_sent\" updated"
}
```

 <a name="paymentCancel"></a>
## Отмена платежа SKY PAY V2

```http
  PATCH /rest/v2/payments_v2/<ID>/cancel
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `ID` | **Required**.

#### Response example

```javascript
{
  "success": true
}
```
