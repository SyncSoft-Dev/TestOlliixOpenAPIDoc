.. Olliix Open API documentation master file, created by
   sphinx-quickstart on Thu Mar 11 09:19:25 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Authentication
==============

Generate Token
--------------

Before you can start using the Shippo API, you’ll need to register for a free Shippo account and get your API live token from the API page of the dashboard.

To create production shipping labels and make live requests, you must authenticate your requests using the live token. All code samples in these tutorials use your test token.


Getting started
---------------
**Request URL** ::

	https://api.olliix.com/Open/Token/Create

**Request Method** ::

	POST

**Request Parameter**

+------------------------+------------+----------+------------+
|Parameter name          | required   | type     | description|
+========================+============+==========+============+
|username                | true       |string    | user name  |
+------------------------+------------+----------+------------+
|password                | true       |string    | password   |
+------------------------+------------+----------+------------+


**Response JSON** ::

	{
		"Result": {
			"access_token": "",
			"token_type": "",
			"expires_in": 0
		},
		"MsgCode": null,
		"IsSuccess": true
	}
	
**Response Parameter**

+--------------------+----------+------------------------------+
|Parameter name      | type     | description                  |
+====================+==========+==============================+
|MsgCode             | string   | error message.               |
+--------------------+----------+------------------------------+
|IsSuccess           | boolean  | whether the request was      |
|                    |          | successful.                  |
+--------------------+----------+------------------------------+
|Result.access_token | string   | token string.                |
+--------------------+----------+------------------------------+
|Result.token_type   | string   | token type.                  |
+--------------------+----------+------------------------------+
|Result.expires_in   | int      | expire date.                 |
+--------------------+----------+------------------------------+


**cURL** ::

   curl --location --request POST 'https://api.olliix.com/Open/Token/Create' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --data-urlencode 'username=yourusername' \
   --data-urlencode 'password=yourpassword'

**Golang** ::

	package main
	import (
	  "fmt"
	  "strings"
	  "net/http"
	  "io/ioutil"
	)
	func main() {
	  url := "https://api.olliix.com/Open/Token/Create"
	  method := "POST"
	  payload := strings.NewReader("username=yourusername&password=yourpassword")
	  client := &http.Client {
	  }
	  req, err := http.NewRequest(method, url, payload)
	  if err != nil {
		fmt.Println(err)
		return
	  }
	  req.Header.Add("Content-Type", "application/x-www-form-urlencoded")
	  res, err := client.Do(req)
	  if err != nil {
		fmt.Println(err)
		return
	  }
	  defer res.Body.Close()
	  body, err := ioutil.ReadAll(res.Body)
	  if err != nil {
		fmt.Println(err)
		return
	  }
	  fmt.Println(string(body))
	}

**Python - requests** ::

	import requests
	url = "https://api.olliix.com/Open/Token/Create"
	payload='username=yourusername&password=yourpassword'
	headers = {
	  'Content-Type': 'application/x-www-form-urlencoded'
	}
	response = requests.request("POST", url, headers=headers, data=payload)
	print(response.text)

**Python - http.client** ::

	import http.client
	conn = http.client.HTTPSConnection("api.olliix.com", 443)
	payload = 'username=yourusername&password=yourpassword&='
	headers = {
	  'Content-Type': 'application/x-www-form-urlencoded'
	}
	conn.request("POST", "/Open/Token/Create", payload, headers)
	res = conn.getresponse()
	data = res.read()
	print(data.decode("utf-8"))

**Java - OkHttp** ::

	OkHttpClient client = new OkHttpClient().newBuilder()
	  .build();
	MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
	RequestBody body = RequestBody.create(mediaType, "username=username&password=password");
	Request request = new Request.Builder()
	  .url("https://api.olliix.com/Open/Token/Create")
	  .method("POST", body)
	  .addHeader("Content-Type", "application/x-www-form-urlencoded")
	  .build();
	Response response = client.newCall(request).execute();


**Java - Unirest** ::

	Unirest.setTimeouts(0, 0);
	HttpResponse<String> response = Unirest.post("https://api.olliix.com/Open/Token/Create")
	  .header("Content-Type", "application/x-www-form-urlencoded")
	  .field("username", "username")
	  .field("password", "password")
	  .asString();



