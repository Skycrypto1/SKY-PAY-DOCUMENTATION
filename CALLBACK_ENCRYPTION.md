<h1 align="center">Шифрование Callback</h1>

 При шифровании callback пользуемся этой библиотекой для шифрования https://pypi.org/project/requests-http-signature/.

 Пример кода на **Python**:

 ```python
import hmac
import hashlib
import base64
 
def get_signature(data: dict, secret_key: str) -> str:
    sig_base = "\n".join(f'"{k}": {v}' for k, v in data.items())
    signature = hmac.new(
        secret_key.encode(),
        msg=sig_base.encode(),
        digestmod=hashlib.sha256
    ).digest()
    base64_signature = base64.b64encode(signature).decode()
    return base64_signature
 
sig_elements = {
    "@method": "POST",
    "@authority": "webhook.site",
    "@target-uri": "https://webhook.site/58e17407-e67a-4154-b669-88f1ec61f491",
    "content-digest": "sha-256=:GUi7pi//QbqRKLSDrRl8M1WDazFIw6Lhucx+V79ZgLQ=:",
    "date": "Mon, 23 Oct 2023 17:06:14 GMT",
    "@signature-params": '("@method" "@authority" "@target-uri" "content-digest" "date");created=1698080774;keyid="16335dd55d344700acbdd83de436e90c";alg="hmac-sha256"'
}
secret = "your_secret_key"
result_signature = get_signature(sig_elements, secret)
# Дальше эта подпись сравнивается с той, которая пришла в запросе, тем самым проверяется подлинность
```

Пример кода на **Javascript**:

```javascript
const crypto = require('crypto');
 
function getSignature(data, secretKey) {
  const sigBase = Object.entries(data)
    .map(([key, value]) => `"${key}": ${value}`)
    .join('\n');
  
  const hmac = crypto.createHmac('sha256', secretKey);
  hmac.update(sigBase);
  const signature = hmac.digest('base64');
  
  return signature;
}
 
const sigElements = {
  "@method": "POST",
  "@authority": "webhook.site",
  "@target-uri": "https://webhook.site/58e17407-e67a-4154-b669-88f1ec61f491",
  "content-digest": "sha-256=:GUi7pi//QbqRKLSDrRl8M1WDazFIw6Lhucx+V79ZgLQ=:",
  "date": "Mon, 23 Oct 2023 17:06:14 GMT",
  "@signature-params": '("@method" "@authority" "@target-uri" "content-digest" "date");created=1698080774;keyid="16335dd55d344700acbdd83de436e90c";alg="hmac-sha256"'
};
 
const secretKey = '29fad1cbcf574a0f9cddf2504fe8f73c';  // Замените на ваш фактический секретный ключ
 
result_signature = getSignature(sigElements, secretKey);
```
