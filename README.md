<h1 align="center"><a href="https://skycrypto.me/" target="_blank">SKY CRYPTO</a> 

## Для активизации возможностей из документации, пользователю необходимо выполнить следующие действия:
 - Зарегистрироваться на https://skycrypto.me/ **(cсылка на тестовое окружение - по запросу к поддержке)**.

 - На странице https://skycrypto.me/merchant **(cсылка на тестовое окружение - по запросу к поддержке)** заполнить в SKY API параметры интернет-площадки: Название, Сайт, Логотип, которые будут отображаться в заказе SKY PAY. Нажать на кнопку "Перегенерировать токен" и получить свой уникальный TOKEN. Полученный таким образом TOKEN используется во всех запросах, указанных в настоящей документации, в следующем формате: **Authorization: Token < TOKEN >**.
 - Если указать callback_url, то после успешного/не успешного платежа на адрес callback_url придет POST запрос с данными платежа.  Если запрос на callback_url не успешен, он будет отсылаться раз в минуту, пока не получит в ответ HTTP Status Code 200. Описание параметров, которые придут на callback:
   - Purchase callback URL:
     - [Информация из response Sky Pay](SKYPAY.md#Получение-информации-по-выполнению-SKY-PAY)
     - [Информация из response Sky Pay](SKYPAY.md#Получение-информации-по-выполнению-SKY-PAY)  
   - Sale callback URL - [Информация из response Sky Sale](SKYSALE.md#Получение-информации-по-выполнению-SKY-SALE)
   - Cpayment callback URL - [Информация из response Cpayment](CPAYMENT.md#Получение-информации-по-CPAYMENT)

    На странице https://skycrypto.me/merchant **(cсылка на тестовое окружение - по запросу к поддержке)** существует возможность шифровать callback, активировав соответствующий переключатель и нажав на кнопку "Перегенерировать ключи шифрования". Подробнее о шифровании callback Вы можете прочитать на странице [Шифрование Callback](CALLBACK_ENCRYPTION.md)
- Связаться с администратором SKY PAY для того, чтобы он активировал необходый функционал для интернет-площадки, предоставив ему Название.
  
**API PROD** - https://papi.skycrypto.net или https://papi.skycrypto.me
 **API TEST** - https://papi.trcrfortest.co
 
 ## API DOCUMENTATION
- [**Sky Pay (Fiat purchase with redirect)**](SKYPAY.md)
- [**Sky Sale (Fiat sale with redirect)**](SKYSALE.md)
- [**Sky Pay v2 (Fiat purchase without redirect)**](SKYPAYV2.md)
- [**Sky Sale v2 (Fiat sale without redirect)**](SKYSALEV2.md)
- [**Widthdrawal v2 (Withdrawal without redirect)**](WITHDRAWAL.md)
- [**Cpayment (Crypto purchase with redirect)**](CPAYMENT.md)
- [**Flash Pay**](FLASHPAY.md)
- [**Callback encryption**](CALLBACK_ENCRYPTION.md)
- [**Common**](COMMON.md)

