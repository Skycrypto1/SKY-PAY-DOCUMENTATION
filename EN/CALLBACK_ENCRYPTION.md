<h1 align="center">Callback encryption</h1>

 When encrypting callbacks, we use this library for encryption https://pypi.org/project/requests-http-signature/.

 Callback encryption is used only for JSON format. The format application/x-www-form-urlencoded can only be received unencrypted.

 **Python** code example:

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
    "date": "Mon, 23 Oct 2023 17:06:14 GMT",
    "content-digest": "sha-256=:GUi7pi//QbqRKLSDrRl8M1WDazFIw6Lhucx+V79ZgLQ=:",
    "@signature-params": '("@method" "@authority" "@target-uri" "content-digest" "date");created=1698080774;keyid="16335dd55d344700acbdd83de436e90c";alg="hmac-sha256"'
}

secret = "your_secret_key"
result_signature = get_signature(sig_elements, secret)
```

**Javascript** code example:

```javascript
const crypto = require('crypto');
const secret = "your_secret_key"; // Replace with your actual private key

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
  "date": "Mon, 23 Oct 2023 17:06:14 GMT",
  "content-digest": "sha-256=:GUi7pi//QbqRKLSDrRl8M1WDazFIw6Lhucx+V79ZgLQ=:",
  "@signature-params": '("@method" "@authority" "@target-uri" "content-digest" "date");created=1698080774;keyid="16335dd55d344700acbdd83de436e90c";alg="hmac-sha256"'
};

const resultSignature = getSignature(sigElements, secret)

```

**PHP** code example:

```PHP
<?php
function getSignature($data, $secretKey) {
    $sigBase = implode("\n", array_map(function($key, $value) {
        return "\"$key\": $value";
    }, array_keys($data), $data));
 
    $signature = hash_hmac('sha256', $sigBase, $secretKey, true);
    $base64Signature = base64_encode($signature);
 
    return $base64Signature;
}
 
$sigElements = [
    "@method" => "POST",
    "@authority" => "webhook.site",
    "@target-uri" => "https://webhook.site/58e17407-e67a-4154-b669-88f1ec61f491",
    "date" => "Mon, 23 Oct 2023 17:06:14 GMT",
    "content-digest" => "sha-256=:GUi7pi//QbqRKLSDrRl8M1WDazFIw6Lhucx+V79ZgLQ=:",
    "@signature-params" => '("@method" "@authority" "@target-uri" "content-digest" "date");created=1698080774;keyid="16335dd55d344700acbdd83de436e90c";alg="hmac-sha256"'
];
 
$secretKey = "your_secret_key"  // Replace with your actual private key
 
$resultSignature = getSignature($sigElements, $secretKey);
?>
```

Explanations for the code:

```python
sig_elements = {
"@method": "POST", # Callback method
"@authority": "webhook.site", # From header host
"@target-uri": "https://webhook.site/58e17407-e67a-4154-b669-88f1ec61f491", # Callback recieving address
"date": "Mon, 23 Oct 2023 17:06:14 GMT", # From header date
"content-digest": "sha-256=:GUi7pi//QbqRKLSDrRl8M1WDazFIw6Lhucx+V79ZgLQ=:", # From header content-digest
"@signature-params": '("@method" "@authority" "@target-uri" "content-digest" "date");created=1698080774;keyid="16335dd55d344700acbdd83de436e90c";alg="hmac-sha256"' # From header signature-input, full info after pyhms= param
```

Next, resultSignature must be compared with signature, which comes in header signature. If there is a match, it means that the information in the callback has not been changed.

