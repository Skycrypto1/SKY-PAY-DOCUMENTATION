<h1 align="center">WITHDRAWAL V2 API</h1>
 
[Creating WITHDRAWAL V2](#withdrawal)

[Getting information about running WITHDRAWAL V2](#withdrawalinfo)

[Commissions](#commissions)

## Activation WITHDRAWAL V2

Before performing the following steps, you must contact the SKY PAY administrator so that he can activate Withdrawal v2 for the online platform by providing him with a Name.

<a name="withdrawal"></a>
## Creating WITHDRAWAL V2

```http
  POST /rest/v2/withdrawals 
```
#### Body parameters

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbol` | `string` | **Required**. [List of cryptocurrencies](CRYPTOCURRENCIES.md)
| `amount` | `number` | **Required**. The purchase amount should not exceed 6 decimal places. [Cryptocurrency withdrawal limits](WITHDRAWALLIMITS.md)
| `address` | `string` | **Required**. Wallet address.
| `client_order_id` | `string` | This field is intended to implement idempotency.

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
## Getting information about running WITHDRAWAL V2

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
| `1` | Generated output |
| `2` | Successful withdrawal |
| `3` | Unsuccessful withdrawal |

 <a name="commissions"></a>
## Commissions

| cryptocurrency | commision                |
| :-------- |  :------------------------- |
| `btc` | 0.0001 |
| `eth` | 0.001  |
| `usdt` | 1 |

