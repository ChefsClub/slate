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

Seja bem vindo a documentação da API Mobile do ChefsClub

# Account

## Search an Account

```shell
curl https://account.chefsclub.com.br/api/v3/accounts/search?email=marolito@gmail.com -i
```

> If en error occur, the above command returns JSON structured like this:

```json
{
  "error":
    {
      "description":"Esse cliente é grubster",
      "raw_errors": "",
      "code": 409
    }
}
```

This endpoint checks if the email or cpf provided is an chefsclub account

### Request Body

Parameter | Description
--------- | -----------
email | The email of the user to search
cpf | The cpf of the user to search
oauth_user_id | The user id from the identity provider used to authenticate (Facebook, Google)

### Status Codes:
Code | Description
--------- | -----------
200 | Found
404 | Not Found
409 | Grubster Client


### HTTP Request

`GET https://account.chefsclub.com.br/api/v3/accounts/search`

# Clients

## Create a client

```shell
curl https://account.chefsclub.com.br/api/v3/clients \
  -i -H "Content-Type: application/json" \
  -X POST \
  -d '{
        "client": {
          "full_name":"Leonardo Ferreira",
          "email" : "marolito@gmail.com",
          "cpf:": "02103459603"
          "password": "123456",
          "password_confirmation": "123456"
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

Creates a client and a trial subscription

### Request Body

Parameter | Description
--------- | -----------
full_name | Client's full name
email | The email of the user to search
cpf | The cpf of the user to search
password | self-explaining
password_confirmation | self-explaining
**Optional Parameters** |
oauth_user_id | The user id from the identity provider used to authenticate (Facebook, Google)
oauth_token | Server side token to make requests to client information
oauth_provider | Facebook or Google
gender | self-explaining  (M of F)
birthdate | self-explaining
mobile_number | self-explaining
profile_image_url | User social media photo
fcm_token | Firebase token to send push notifications
device_platform | Android or iOS
promocode | A promocode from a caimpaing in order to increase months at user subscription

### HTTP Request

`POST https://account.chefsclub.com.br/api/v3/clients`

## Update a client

````shell
curl https://account.chefsclub.com.br/api/v3/clients/74e7c0ff-706e-4f88-a560-7bfcaa09356f \
  -i -H "Content-Type: application/json" \
  -X PUT \
  -d '{
        "client": {
          "full_name":"Leonardo Ferreira da Silva"
         }
      }'
```

> The above command returns JSON structured like this:

```json
{
  "client":
    {
      "first_name":"Leonardo",
      "last_name":"Ferreira",
      "email":"marolito@gmail.com",
      "uuid":"74e7c0ff-706e-4f88-a560-7bfcaa09356f",
      "client_id":229544,
      "referral_link":null
    }
}
```

Update client information.

### Request Body
Same as the client creations

### HTTP Request

`PATCH https://account.chefsclub.com.br/api/v3/clients/:id`

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

### Status Codes:
Code | Description
--------- | -----------
201 | Session created
206 | Session created, but there're required information missing, usually it's cpf
400 | Bad Request, usually when the email or cpf is duplicated
401 | Not authorized, creditials are wrong

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

# Passwords

## Send recovery email

```shell
curl https://account.chefsclub.com.br/api/v3/recover_passwords \
  -i -X POST \
  -H "Content-Type: application/json" \
  -d '{ "account": { "auth_key" : "email@example.org" } }'
```

> The above command does't returns anything

This endpoint sends en email to the client with a password recovery token

### HTTP Request

`POST https://account.chefsclub.com.br/api/v3/recover_passwords`

## Recover password

```shell
curl https://account.chefsclub.com.br/api/v3/recover_passwords \
  -i -X POST \
  -H "Content-Type: application/json" \
  -d '{
        "account": {
            "password": "chefs123",
            "password_confirmation":"chefs123",
            "token": "so283dg2663"
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

This endpoint updates the client password if the recovery token is correct and makes a new session to the user

### HTTP Request

`PUT https://account.chefsclub.com.br/api/v3/recover_passwords`

# Reservation

## Create a booking or checkin

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


## Cancel a booking

```shell
curl https://account.chefsclub.com.br/api/v3/reservations/<ID> \
  -i -X DELETE \
  -H "Content-Type: application/json" \
  -H "X-Client-Access-Token: XG1x8CxbQsOYViQpmS8rAm6GEhyMxxCuv_DFzZ4AvA8ybhusdDioafMgSHa1d-WW_T7UEqH0_HdmiSgOVQ4xH8okSwGRN_UhJ7wh1O-GKo9VZ9FWOQu_lpYMXXZIJKHa-pmo7ULJ0TIOYHV83y-9HPYY2OlWpFEYyg3eih0OvecaMQGO9JH9hHp7Qfw5Vs3gn_ThLZnvzlIsvv6xJkzTXCaYnuLoYzRcNCeAbug96fs=" \
```

> The above command returns JSON structured like this:

```json
{ "reservation":
  {
    "id": "10",
    "canceled_at": "2018-01-17T15:30:00-02:00"
  }
}
```

The endpoint cancels a booking reservation

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the  booking reservation to cancel


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

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>
