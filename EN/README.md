<h1 align="center"><a href="https://skycrypto.me/" target="_blank">SKY CRYPTO</a> 

## To activate the features from the documentation, the user must perform the following steps:
 - Register at https://skycrypto.me/ **(test environment - https://trcrfortest.co/)**.

 - On the page https://skycrypto.me/merchant **(test environment - https://trcrfortest.co/merchant)** 
fill in the parameters of the online platform in the SKY API: Name, Website, Logo, which will be displayed in the SKY PAY order. Click on the "Regenerate token" button and get your unique TOKEN. The resulting TOKEN is used in all requests specified in this documentation in the following format: **Authorization: Token < TOKEN >**.
 - If you specify callback_url, then after a successful/unsuccessful payment or receipt of transfer details within Sky Pay v2 and Flash Pay (Acceptance), a POST request with payment data will be sent to the callback_url address. If the request to callback_url is not successful, it will be sent once per minute until it receives an HTTP Status Code 200 in response. The Purchase callback URL sends a callback to Sky Pay, the Sale callback URL sends a callback to Sky Sale, and the Payment callback URL sends a callback to Cpayment. The callback format is selected in the merchant’s personal account from the following two options: application/x-www-form-urlencoded or JSON. Description of the parameters that will be sent to the callback:
  - Purchase callback URL:
     - For Sky Pay - [Information from response Sky Pay](SKYPAY.md#Receiving-information-on-execution-SKY-PAY)
     - For Sky Pay v2 - [Information from response Sky Pay v2](SKYPAYV2.md#Receiving-information-on-execution-SKY-PAY-V2)
     - For Flash Pay (Reception) - [Information from response Flash Pay (Reception)](FLASHPAY.md#Reception)
  - Sale callback URL:
     - For Sky Sale - [Information from response Sky Sale](SKYSALE.md#Receiving-information-on-execution-SKY-SALE)
     - For Sky Sale v2 - [Information from response Sky Sale v2](SKYSALEV2.md#Receiving-information-on-execution-SKY-SALE-V2)
     - For Flash Pay (Payment) - [Information from response Flash Pay (Payment)](FLASHPAY.md#Payment)
  - Cpayment callback URL - [Information from response Cpayment](CPAYMENT.md#Receiving-information-on-CPAYMENT)

On the page https://skycrypto.me/merchant **(test environment - https://trcrfortest.co/merchant)** It is possible to encrypt callback by activating the corresponding switch and clicking on the "Regenerate encryption keys" button. You can read more about callback encryption on the page [Callback Encryption](CALLBACK_ENCRYPTION.md)
- Contact the SKY PAY administrator so that he can activate the necessary functionality for the online platform by providing him with a Name.
  
**API PROD** - https://papi.skycrypto.net or https://papi.skycrypto.me
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

