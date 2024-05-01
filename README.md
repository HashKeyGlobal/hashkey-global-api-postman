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
