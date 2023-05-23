<h1 align="center">SKY SALE API</h1>
 

[Создание SKY SALE](#skysale)

[Получение информации по выполнению SKY SALE](#skysaleinfo)

 <a name="skysale"></a>
## Создание SKY SALE

```http
  POST /rest/v2/sells 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `amount` | `number` | **Required**. Сумма покупки. [Посмотреть информацию по лимитам валют](CURRENCIES_SALES.md)
| `label` | `string` | **Required**. Hash который заедается мерчантом
| `symbol` | `string` | **Required**. [Список криптовалют](CRYPTOCURRENCIES.md)
| `currency` | `string` | **Required**. [Список валют](CURRENCIES_SALES.md)
| `back_url` | `string` | Cсылка на страницу, куда будет перенаправлен пользователь после успешной оплаты
| `lang` | `string` | Используется для установки языка интерфейса SKY PAY. По дефолту - 'ru'. [Список языков SKY PAY](SKYPAYLANGUAGES.md)

#### Limits

| Parameter | Rules     |
| :-------- | :-------  |
| `amount` | ``` {linenums="1"}
 minimum: **0.0001**
maximum: **100000000**
```
| `label` | maxLength: **256**
| `back_url` | maxLength: **255**

#### Body example

```javascript
{
  "amount": 10000,
  "label": "100311",
  "symbol": "btc",
  "currency": "rub",
  "back_url": "https://myservice.com/payment/100311",
}
```

#### Response example

```javascript
{
  "amount": 10000,
  "created_at": "2023-02-23T13:39:02.144538+00:00",
  "currency": "rub",
  "email": null,
  "id": "8392d915-668b-4ff3-9b02-45ead91c4d43",
  "is_approved": false,
  "label": "100311",
  "merchant_id": 186024,
  "processed_at": null,
  "status": 0,
  "symbol": "btc",
  "web_link": "http://qpay.sky-crypto.com/sale/8392d915-668b-4ff3-9b02-45ead91c4d43?ca=10000&s=btc&m=186024&l=100311",
  "back_url": "https://myservice.com/payment/100311",
  "lang": "ru"
}
```
Подтверждение вывода средств – это операция на внутреннем API SKY. При наличии баланса мерчанта, создается временный пользователь, которому переводятся средства. При переходе по ссылке, клиент создает сделку на продажу криптовалюты, которая была списана со счета мерчанта. Если спустя час нет активной сделки на продажу с данного аккаунта, средства возвращаются на баланс мерчанта. 

 <a name="skysaleinfo"></a>
## Получение информации по выполнению SKY SALE

```http
  GET rest/v2/sells/<SALE_ID> 
```

#### Query parameters

| Parameter | Description                |
| :-------- | :------------------------- |
| `SALE_ID` | **Required**.

#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `callback_url` | `string` |Если указан callback_url, то после успешного/не успешного платежа на адрес callback_url придет POST запрос с данными платежа. Если запрос на callback_url не успешен, он будет отсылаться раз в минуту, пока не получит в ответ HTTP Status Code 200.


#### Response example

```javascript
{
  "amount": 10000,
  "created_at": "2023-02-23T13:41:45.024091+00:00",
  "currency": "rub",
  "email": "6f4c708755c445b@noemail.fkfl",
  "id": "d9a9312e-78fc-4d99-9baf-8b6c0a7493d6",
  "is_approved": true,
  "label": "100311",
  "merchant_id": 186024,
  "processed_at": null,
  "status": 0,
  "symbol": "btc",
  "web_link": "http://qpay.sky-crypto.com/sale/d9a9312e-78fc-4d99-9baf-8b6c0a7493d6?ca=10000&s=btc&m=186024&l=100311",
  "lang": "ru"
}
```

| Sale status (status) | Description                |
| :-------- |  :------------------------- |
| `0` | Cозданная продажа |
| `1` | Продажа в статусе оплаты |
| `2` | Успешная продажа |
| `3` | Не успешная продажа |
