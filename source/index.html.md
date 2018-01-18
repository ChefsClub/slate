---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Session

## Create a Session

```shell
curl https://account.chefsclub.com.br/api/v3/sessions \
  -i -H "Content-Type: application/json" \
  -X POST \
  -d '{ 
        "account": { 
          "email" : "marolito@gmail.com",
          "password": "123456" 
         } 
      }'
```

> The above command returns JSON structured like this:

```json
{
  "account":
    {
      "access_token":"XG1x8CxbQsOYViQpmS8rAm6GEhyMxxCuv_DFzZ4AvA8ybhusdDioafMgSHa1d-WW_T7UEqH0_HdmiSgOVQ4xH8okSwGRN_UhJ7wh1O-GKo9VZ9FWOQu_lpYMXXZIJKHa-pmo7ULJ0TIOYHV83y-9HPYY2OlWpFEYyg3eih0OvecaMQGO9JH9hHp7Qfw5Vs3gn_ThLZnvzlIsvv6xJkzTXCaYnuLoYzRcNCeAbug96fs=",
      "first_name":"Leonardo",
      "last_name":"Ferreira",
      "email":"marolito@gmail.com",
      "uuid":"74e7c0ff-706e-4f88-a560-7bfcaa09356f",
      "client_id":229544,
      "referral_link":null
    }
}
```

Create user session based on the possible credentials.

### HTTP Request

`GET https://account.chefsclub.com.br/api/v3/sessions`

### Request Body

Parameter | Description
--------- | -----------
email | The email of the user
password | The password should be passed along the email
oauth_token | The oauth_token from the identity provider used to authenticate (Facebook, Google)
oauh_provider | The identity provider used to authenticate (Facebook, Google)

## Destroy a session

```shell
curl https://account.chefsclub.com.br/api/v3/sessions \
  -i -X DELETE \
  -H "Content-Type: application/json" \
  -H "X-Client-Access-Token: XG1x8CxbQsOYViQpmS8rAm6GEhyMxxCuv_DFzZ4AvA8ybhusdDioafMgSHa1d-WW_T7UEqH0_HdmiSgOVQ4xH8okSwGRN_UhJ7wh1O-GKo9VZ9FWOQu_lpYMXXZIJKHa-pmo7ULJ0TIOYHV83y-9HPYY2OlWpFEYyg3eih0OvecaMQGO9JH9hHp7Qfw5Vs3gn_ThLZnvzlIsvv6xJkzTXCaYnuLoYzRcNCeAbug96fs="
```

> The above command does't returns anything


Destroy a user session.


### HTTP Request

`POST https://account.chefsclub.com.br/api/v3/reservations`

# Reservation 

```shell
curl https://account.chefsclub.com.br/api/v3/reservations \
  -i -X POST \
  -H "Content-Type: application/json" \
  -H "X-Client-Access-Token: XG1x8CxbQsOYViQpmS8rAm6GEhyMxxCuv_DFzZ4AvA8ybhusdDioafMgSHa1d-WW_T7UEqH0_HdmiSgOVQ4xH8okSwGRN_UhJ7wh1O-GKo9VZ9FWOQu_lpYMXXZIJKHa-pmo7ULJ0TIOYHV83y-9HPYY2OlWpFEYyg3eih0OvecaMQGO9JH9hHp7Qfw5Vs3gn_ThLZnvzlIsvv6xJkzTXCaYnuLoYzRcNCeAbug96fs=" \
  -d '{ "checkin": { "restaurant_id" : 3004 } }'
```

> The above command returns JSON structured like this:

```json
{
  "reservation": {
    "id": 10,
    "starts_at": "2018-01-18T16:30:00-02:00",
    "expires_at": "2018-01-18T18:30:00-02:00",
    "created_at": "",
    "canceled_at": null,
    "savings": null,
    "rating": null,
    "type": "booking"
    "seats": 6,
    "client": {
      "first_name": "James"
      "last_name": "Taylor"
      "cpf": "99999999999"
    }
    "restaurant" : {
      "id": 10,
      "name": "Pobre Juan",
      "cuisines": ["Francesa"],
      "photo": "http://example.org/photo.jpg",
      "cover_photo": "http://example.org/photo.jpg",
      "address": "Rua da aurora",
      "city": "Recife",
      "state": "PE",
      "neighborhood": "Centro",
      "active": true,
      "latitude": "-23.45960",
      "longitude": "45.298743",
    }
    "offer": {
      "discount": "30"
      "description": "Desconto na conta toda"
      "restriction": "Não vale menu executivo"
      "period": "10:00 - 11:00"
    }
  }
}
```

Create a checkin or booking a restaurant.


### Request Body
Parameter | Description
--------- | -----------
restaurant_id | The restaurante for the reservation or checkin
reserve_at (datetime) | optional
savings (float) | optional
latitude (float) |optional
longitude (float) |optional
seats (interger) | optional


### Status Codes:
Code | Description
--------- | -----------
201 | Created
400 | Restaurante não existente
401 | Access Token Inválido
402 | Sem Assinatura
404/410 | Reserva não mais disponível

# Examples

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete


<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

