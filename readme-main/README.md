<h1 align="center"><a href="https://skycrypto.me/" target="_blank">SKY CRYPTO</a> 

## Для активизации возможностей из документации, пользователю необходимо выполнить следующие действия:
 - Зарегистрироваться на https://skycrypto.me/.

 - На странице https://skycrypto.me/merchant заполнить в SKY API параметры интернет-площадки: Название, Сайт, Логотип, которые будут отображаться в заказе SKY PAY. Нажать на кнопку "Перегенерировать токен" и получить свой уникальный TOKEN.  
 Если указать callback_url, то после успешного/не успешного платежа на адрес callback_url придет POST запрос с данными платежа.  Если запрос на callback_url не успешен, он будет отсылаться раз в минуту, пока не получит в ответ HTTP Status Code 200.
  
- Связаться с администратором SKY PAY для того, чтобы он активировал необходый функционал для интернет-площадки, предоставив ему Название.
  
## API
  
- [**SkyPay**](SKYPAY.md)
- [**SkySale**](SKYSALE.md)
- [**SkyPay v2**](SKYPAYV2.md)
- [**SkySale v2**](SKYSALEV2.md)
- [**Withdrawal v2**](WITHDRAWAL.md)
- [**Cpayment**](CPAYMENT.md)
- [**Common**](COMMON.md)

