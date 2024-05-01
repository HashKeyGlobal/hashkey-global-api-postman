# HashKey Global API Postman

Hashkey Global now offers Postman collections and environments a popular plug and play API test environment that allows implementing and testing REST and API endpoints.

Postman provides the HTTP networking to connect to the REST API, allows the HTTP header and GET/POST data to be customised and allows for custom code to be executed using Javascript variant.

Pre-request Script
```
var timestamp = new Date().getTime().toString();
pm.environment.set("timestamp", timestamp);

var api_secret = pm.environment.get("secretKey");
var parameters = pm.request.url.query.toObject();

var paramsObject = {};

Object.keys(parameters).forEach((paramKey) => {
  var paramValue = parameters[paramKey];
  var disabled = false;

  if (paramKey !== 'signature' && paramValue && !disabled) {
    paramsObject[paramKey] = paramValue;
  }
});

paramsObject.timestamp = timestamp;

var requestString = Object.keys(paramsObject).map((key) => `${key}=${paramsObject[key]}`).join('&');

var signature = CryptoJS.HmacSHA256(requestString, api_secret).toString();
pm.environment.set("signature", signature);
```

## 1. Download Postman from Postman.com website

![](https://files.readme.io/b57bfa2-image.png)

## 2. Go to our HashKey Global API Postman repository and download the Postman Collection and Environment files

![](https://files.readme.io/9dcaa51-image.png)

## 3. Go to Collection and Environment to download the respective files

![](https://files.readme.io/8d6fdff-image.png)

![](https://files.readme.io/7cc8e7a-image.png)
## 4. Open Postman and navigate to "Import"

![](https://files.readme.io/5f2796b-Import_Postman.png)

## 5. Locate the 2 files to upload or simply drag and drop, you will also need to import the Environment file

![](https://files.readme.io/2b83d7b-image.png)

![](https://files.readme.io/5475132-image.png)
## 6. You will also need to import the Environment file

![](https://files.readme.io/cc45130-Global_Environment.png)

## 7. To ensure Access and Secret is configured properly. Please select environment on the top right corner

![](https://files.readme.io/cad3521-setupenvironment.png)

## 8. Select any endpoints and click "Send".

![](https://files.readme.io/0a3b919-finish.png)
