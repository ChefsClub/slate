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
curl https://account.chefsclub.com.br/api/v3/accounts/search?cpf=12345678900 -i
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

```shell
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

## Show client details

```shell
curl http://account.chefsclub.com.br/api/v3/clients/8102d882-8ea2-4c28-84ac-38169097d1d7 \
  -i -X GET \
  -H "Accept: application/json; charset=utf-8" \
  -H "Content-Type: application/json; charset=utf-8" \
  -H "X-Client-Access-Token: 7zwdHSrzxqGHvFxEPuxAwZRFat3f4dxN-F6GxdHZocFER6ZYqUDcxjZrDxF_aYmU9_y8n5bMrV-yaiiyTBgGEDyGWsQMSojU44z-Cz8zCZftmCYbh5sh_j_mx11ht_VySkVZAkaQ6nxc63Sq2B1nVa9s9qdCbsMXKt9dxqsAghPxgNK2ubzt3AD2bcfwGViXwPw-G9aMTgG-NQSHa7gPq1ucsyHsDq9nyQ4pWuyiSAi"
  -d ''
```

> The above command returns JSON structured like this:

```json
{
  "created_at": "2018-03-02T12:40:30.583-03:00",
  "updated_at": "2019-11-07T16:58:37.503-03:00",
  "client": {
    "tasting": 30,
    "personal": {
      "full_name": "Marcos Serpa",
      "email": "marquito_cabrito@gmail.com",
      "gender": "M",
      "cpf": "13219951700",
      "mobile_number": "219191991919",
      "birthdate": "1986-12-29",
      "referral_link": "http://chefsclub.refr.cc/marcosserpa",
      "facebook_user_id": "818181818181",
      "profile_image_url": "https://graph.facebook.com/818181818181/picture?type=large"
    },
    "address": {
      "zipcode": "22041080",
      "street": "Rua Anita Garibaldi",
      "number": "90",
      "complement": "",
      "reference": "",
      "neighbourhood": "Copacabana",
      "neighborhood": "Copacabana",
      "city": "Rio de Janeiro",
      "state": "RJ"
    },
    "subscription": {
      "is_first": false,
      "status": "valid",
      "activation_date": "2019-05-17T00:00:00.000-03:00",
      "expiration_date": "2020-05-17T23:59:59.000-03:00",
      "serial": "375050244",
      "auto_renewal": false,
      "free_renewal": false,
      "free_renewal_description": "",
      "partner_image_url": null,
      "validity_period": "yearly",
      "channel": "Influenciadores",
      "store": {
        "type": "site"
      }
    }
  }
}
```

Show some client information like creation date, name, email...; also returns it's subscription details.

### URL Parameters

Parameter | Description
--------- | -----------
uuid | The uuid of the client


### HTTP Request

`GET http://account.chefsclub.com.br/api/v3/clients/:uuid`

# Partner Subscriptions Direct Creation

## Partner HAND create a client subscription

```shell
curl https://admin.chefsclub.com.br/parceria/hand/subscription/create \
  -i -X POST \
  -H "Accept: application/json; charset=utf-8" \
  -H "Content-Type: application/json; charset=utf-8" \
  -d '{
        "cpf": "10313931700",
        "coupon": "hand123"
      }'
```

> The above command returns a blank JSON with status 200.



Creates a partner subscription to the client using the coupon.

### Request Body

Parameter | Description
--------- | -----------
cpf | Client's CPF
coupon | Coupon code

### HTTP Request

`POST http://admin.chefsclub.com.br/parceria/hand/subscription/create`

# Session

## Create a Session

```shell
curl -i \
  -X POST \
  -H "Content-Type: application/json; charset=utf-8" \
  -H "Accept: application/json; charset=utf-8" \
  -d '{
        "account": {
          "email" : "marolito@gmail.com",
          "cpf" : "18005879881",
          "password": "e07a1d5f"
         }
      }' \
  'https://account.chefsclub.com.br/api/v3/sessions'
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
cpf | The CPF of the user
password | The password should be passed along the email
oauth_token | The oauth_token from the identity provider used to authenticate (Facebook, Google)
oauh_provider | The identity provider used to authenticate (Facebook, Google)

```email``` or ```cpf``` are needed, not both simultaneously

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

## Change password

```shell
curl https://account.chefsclub.com.br/api/v3/clients/passwords \
  -i -X PUT \
  -H "Content-Type: application/json" \
   -H "X-Client-Access-Token:
   XG1x8CxbQsOYViQpmS8rAm6GEhyMxxCuv_DFzZ4AvA8ybhusdDioafMgSHa1d-WW_T7UEqH0_HdmiSgOVQ4xH8okSwGRN_UhJ7wh1O-GKo9VZ9FWOQu_lpYMXXZIJKHa-pmo7ULJ0TIOYHV83y-9HPYY2OlWpFEYyg3eih0OvecaMQGO9JH9hHp7Qfw5Vs3gn_ThLZnvzlIsvv6xJkzTXCaYnuLoYzRcNCeAbug96fs=" \
  -d '{
        "account": {
            "password": "chefs123",
            "password_confirmation":"chefs123",
            "old_password": "so283dg2663"
          }
      }'
```

> The above command returns JSON structured like this:

```json
{
  "account":
    {
      "access_token":"XG1x8CxbQsOYViQpmS8rAm6GEhyMxxCuv_DFzZ4AvA8ybhusdDioafMgSHa1d-WW_T7UEqH0_HdmiSgOVQ4xH8okSwGRN_UhJ7wh1O-GKo9VZ9FWOQu_lpYMXXZIJKHa-pmo7ULJ0TIOYHV83y-9HPYY2OlWpFEYyg3eih0OvecaMQGO9JH9hHp7Qfw5Vs3gn_ThLZnvzlIsvv6xJkzTXCaYnuLoYzRcNCeAbug96fs=",
    }
}
```

This endpoint changes a password for an authenticated user, but the previous
password must be informed.


### HTTP Request

`PUT https://account.chefsclub.com.br/api/v3/clients/passwords`


## Send recovery email

```shell
curl https://account.chefsclub.com.br/api/v3/recover_passwords \
  -i -X POST \
  -H "Content-Type: application/json" \
  -d '{ "account": { "auth_key" : "12345678900" } }'
```

> The above command does't returns anything

This endpoint sends en email to the client with a password recovery token.

The `auth_key` is the client's cpf. So, the `auth_key` param must have as value
the client's CPF on the request.

### HTTP Request

`POST https://account.chefsclub.com.br/api/v3/recover_passwords`

## Recover password

```shell
curl https://account.chefsclub.com.br/api/v3/recover_passwords \
  -i -X PUT \
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

# Usage

## List all bookings and checkins

```shell
curl -i \
  -X GET \
  -H "Content-Type: application/json; charset=utf-8" \
  -H "Accept: application/json; charset=utf-8" \
  -H "X-Client-Access-Token: XG1x8CxbQsOYViQpmS8rAm6GEhyMxxCuv_DFzZ4AvA8ybhusdDioafMgSHa1d-WW_T7UEqH0_HdmiSgOVQ4xH8okSwGRN_UhJ7wh1O-GKo9VZ9FWOQu_lpYMXXZIJKHa-pmo7ULJ0TIOYHV83y-9HPYY2OlWpFEYyg3eih0OvecaMQGO9JH9hHp7Qfw5Vs3gn_ThLZnvzlIsvv6xJkzTXCaYnuLoYzRcNCeAbug96fs="
  -d '{}' \
  'http://stg-account.chefsclub.com.br/api/v3/usages'
```

> The above command returns JSON structured like this:

```json
{
  "metadata": {
    "results_found": 1737,
    "time_in_milliseconds": null,
    "pagination": {
      "current_page": 1,
      "total_pages": 70,
      "has_next_page": true,
      "has_previous_page": false,
      "next_page": 2,
      "previous_page": null
    }
  },
  "reservations" : [
    {
      "id": 10,
      "starts_at": "2018-01-18T16:30:00-02:00",
      "expires_at": "2018-01-18T18:30:00-02:00",
      "canceled_at": null,
      "savings": null,
      "rating": null,
      "type": "booking"
      "seats": 6,
      "restaurant" : {
        "uuid": "c55045f0-6e8b-471e-9556-c45af9d2861a",
        "name": "Pobre Juan",
        "main_cuisine": "Francesa",
        "photos" : [
          {
            type: 'profile',
            "photo": "http://example.org/photo.jpg",
            "cover_photo": "http://example.org/photo.jpg",
          }
        ],
        "address" {
          "city": "Recife",
          "neighborhood": "Centro",
          "latitude": "-23.45960",
          "longitude": "45.298743"
        },
        "active": true,
        "average_rating" : 4.7
      },
      "offer": {
        "discount": "30"
        "restriction": "Não vale menu executivo"
        "period": "10:00 - 11:00"
      }
    }
  ]
}
```

## Create a booking or checkin

```shell
curl -i \
  -X POST \
  -H "Content-Type: application/json; charset=utf-8" \
  -H "Accept: application/json; charset=utf-8" \
  -H "X-Client-Access-Token: NvrGWQJYVZvZmX0fZ-op3MWyR3hPqQ2rW-s6FCnfgqDPDjrjCTyjsncE1aq2u370C9sY2EsyobYeGlUaUFEeLJXHkjg4sTyMFg-frvqMOxQjVzPgbiyY30MUHi6In2CsYu5avjl4G16s-tcsWX1YIU9IdYFOrZb0HfMFKjZWZKSPzI9kpWZYWKHnxqAtm8iSwO2PeSUqzIQXqCd5Jujf8hTTh_LDlo0m0GRf-r9C3FU=" \
  -d '{
    "reservation" : {
      "restaurant_uuid" : "bb22cffe-41d7-44a7-a32c-a44c871dbc07"
    }
  }' \
  'https://account.chefsclub.com.br/api/v3/usages'
```

> The above command returns JSON structured like this:

```json
{
  "reservation": {
    "id": 10,
    "starts_at": "2018-01-18T16:30:00-02:00",
    "expires_at": "2018-01-18T18:30:00-02:00",
    "canceled_at": null,
    "savings": null,
    "rating": null,
    "type": "booking"
    "seats": 6,
    "restaurant" : {
      "uuid": "c55045f0-6e8b-471e-9556-c45af9d2861a",
      "name": "Pobre Juan",
      "main_cuisine": "Francesa",
      "photos" : [
        {
          type: 'profile',
          "photo": "http://example.org/photo.jpg",
          "cover_photo": "http://example.org/photo.jpg",
        }
      ],
      "address" {
        "city": "Recife",
        "neighborhood": "Centro",
        "latitude": "-23.45960",
        "longitude": "45.298743"
      },
      "active": true,
      "average_rating" : 4.7
    },
    "offer": {
      "discount": "30"
      "restriction": "Não vale menu executivo"
      "custom_restrictions": "Na conta toda"
      "period": "10:00 - 11:00"
    }
  }
}
```

Create a checkin or booking a restaurant.


### Request Body
Parameter | Description
--------- | -----------
restaurant_uuid | The restaurant UUID for the reservation or checkin
reserve_at (datetime) | optional for checkin, required for booking
seats (interger) |  optional for checkin, required for booking
savings (float) | optional
latitude (float) |optional
longitude (float) |optional

### Status Codes:
Code | Description
--------- | -----------
201 | Created
400 | Restaurante não existente
401 | Access Token Inválido
402 | Sem Assinatura
409 | Já tem Reserva para mesma data
420 | Já tem Checkin para o mesmo periodo
404/410 | Reserva não mais disponível

### HTTP Request

`POST https://account.chefsclub.com.br/api/v3/usages`


## Cancel a booking

```shell
curl https://account.chefsclub.com.br/api/v3/usages/<ID> \
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

### HTTP Request

`DELETE https://account.chefsclub.com.br/api/v3/usages/<ID>`


## Create a review to Usage

This endpoint permit you update info about a usage and create the review/feedback to it.


Example of request

```shell
curl -i "https://account.chefsclub.com.br/api/v3/usages/$usage_id"\
  -X PUT
  -H "Content-Type: application/json" \
  -H "X-Client-Access-Token: XG1x8CxbQsOYViQpmS8rAm6GEhyMxxCuv_DFzZ4AvA8ybhusdDioafMgSHa1d-WW_T7UEqH0_HdmiSgOVQ4xH8okSwGRN_UhJ7wh1O-GKo9VZ9FWOQu_lpYMXXZIJKHa-pmo7ULJ0TIOYHV83y-9HPYY2OlWpFEYyg3eih0OvecaMQGO9JH9hHp7Qfw5Vs3gn_ThLZnvzlIsvv6xJkzTXCaYnuLoYzRcNCeAbug96fs=" \
  -d '{
    "reservation": {
      "review_rating": 4,
      "review_comment": "Mussum Ipsum, cacilds vidis litro abertis. Atirei o pau no gatis, per gatis num morreus."
    }
  }'
```

The response should be like document below

```json
{
  "reservation": {
    "id": 5,
    "starts_at": "2018-08-14T00:00:00-03:00",
    "expires_at": null,
    "canceled_at": null,
    "savings": null,
    "rating": 4,
    "comment": "Mussum Ipsum, cacilds vidis litro abertis. Atirei o pau no gatis, per gatis num morreus.",
    "type": null,
    "seats": null,
    "offer": {
      "restriction": "",
      "custom_restrictions": ""
    },
    "restaurant": {
      "uuid": "ca9fb3a8-96ed-4dd5-9a58-f374b8240aa1",
      "name": "La Mole",
      "main_cuisine": null,
      "price_range": null,
      "address": {
        "neighbourhood": null,
        "city": "Rio de Janeiro",
        "latitude": -22.19386272,
        "longitude": -44.38198463
      },
      "photos": [
        {
          "type": "profile",
          "url": null,
          "thumb": null
        }
      ],
      "average_rating": null,
      "active": true
    },
    "client": {
      "full_name": "Paulo Patto",
      "cpf": "19151234500"
    }
  }
}
```

### URL Parameters

Parameter | Description
--------- | -----------
USAGE_ID | The ID of the  booking reservation to review

### HTTP Request

`PUT|PATCH https://account.chefsclub.com.br/api/v3/usages/:usage_id`

### Request Body

Parameter | Description
--------- | -----------
rating | The rating of review (integer)
comment | The comment about you experience (string)

### HEADERS

Header | Description
------ | -----------
X-Client-Access-Token | Client Access token

---


# API de Busca de Restaurantes

Essa API tem um outro endpoint.

# Areas

## Retrieve Areas

```shell
curl https://search.chefsclub.com.br/api/v6/areas \
  -i -X GET \
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{ "current_area":   {
      "id": "12"
      "name": "Rio de Janeio"
      "slug": "rio-de-janeio"
    },
  "areas":
  [
    {
      "id": "12"
      "name": "Rio de Janeio"
      "slug": "rio-de-janeio"
    },
     {
      "id": "13"
      "name": "São Paulo"
      "slug": "sao-paulo"
    },
    {
      "id": "14"
      "name": "Recife e Região"
      "slug": "recife-e-região"
    }
  ]
}
```

Areas is a short for Interest Areas, at our api we both have the concept of city and interest areas. An interest areas can be composed by some neighboorhoods, cities or city areas.
Example: Baixada Fluminense (Duque de Caxias, Nova iguaçu, Nilopolis)

### URL Parameters

Parameter | Description
--------- | -----------
latitude |
longitude |

### HTTP Request

`GET https://search.chefsclub.com.br/api/v6/areas`

# Restaurants

## Retrieve restaurants

```shell
curl https://search.chefsclub.com.br/api/v6/restaurants \
  -i -X GET \
  -H "Content-Type: application/json"
  -d 'latitude=-23.0984' \
  -d 'longitide=-23.0984'
```

> The above command returns JSON structured like this:

```json
{
  "metadata": {
    "results_found": 1737,
    "time_in_milliseconds": 4,
    "pagination": {
      "current_page": 1,
      "total_pages": 70,
      "has_next_page": true,
      "has_previous_page": false,
      "next_page": 2,
      "previous_page": null
    }
  },
  "restaurants": [
    {
      "uuid": "4885-ssdfsdfdsf-fdsf-34534",
      "name": "Lá no Escondidinho",
      "main_cuisine": "Brasileira",
      "address": {
        "neighbourhood": "Brooklin",
        "latitude": 32425658679070,
        "longitude": 4353474574577
      },
      "photos": [
        {
          "type": "profile",
          "url": "https://dqwr636hdjha6.cloudfront.net/uploads/restaurant_picture/picture/29861/3509458878559132905_o.jpg",
          "thumb": "https://dqwr636hdjha6.cloudfront.net/uploads/restaurant_picture/picture/29861/3509458878559132905_o.jpg"
        }
      ],
      "available_offers": [
        "checkin",
        "book",
        "delivery"
      ],
      "offers": [
        {
          "highlights": ["Ganhe uma cortesia"],
          "discount": 20,
          "benefit": "ganhe uma sobremesa"
        }
      ],
      "average_rating": 4.6
    }
  ]
}
```

###  URL Parameters

Parameter | Description
--------- | -----------
latitude |
longititude |
area | The area slug to retrieve the highlights
neighbourhood_id | Filtra por bairro. É possível filtrar por múltiplos bairros.
cuisine_id[] |  Filtra por categoria. É possível filtrar por múltiplas categorias
price_range[] |  Filtra por faixa de preço Valores possíveis:  2 , 3 , 4 , 5
offers[] | Filtra por tipo de disponibilidade. É possível especificar múltiplos sources. Possible values: checkin, booking, delivery. Ex.: offers[]=checkin,booking
seats | Filtra por disponibilidade de número de pessoas
date |  Filtra por data hora, formato ISO8601(yyyy-mm-dd)
time | Filtra por hora, Possible values:  search_next , lunch , dinner , all , HH:MM.
datetime | Filtra por data e hora
discount | Filtra por percentual de desconto. Example: 30.
page | Número da página de resultados Default: 1.
per_page | Número de resultados (restaurantes) por página
order | Define a ordenação dos resultados A ordenação padrão muda para name (relevância do nome pesquisado) se a busca for por nome de restaurante. E se a busca for geolocalizada a ordenação padrão muda para nearest (mais próximos). Default: ranking. Possible values:  name, nearest, ranking, recommended.


### HTTP Request

`GET https://search.chefsclub.com.br/api/v6/restaurants`

## Get a restaurant

```shell
curl https://account.chefsclub.com.br/api/v6/restaurants/12344-1dks923-2938d` \
  -i -X GET \
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
  "name": "restaurant.name",
  "uiuid": "restaurant.id",
  "active": "restaurant.active",
  "slug": "restaurant.name.parameterize",
  "price_range": "restaurant.price_range",
  "available_offers": [
    "checkin",
    "book",
    "delivery"
  ],
  "current_offer": {
    "discount": 20,
    "details": ["Desconto na conta toda!", "Cortesia"],
    "benefits": "1 taça de vinho",
    "restrictions": "Não é válido para menu executivo",
    "seats": 4, //quantidade de assentos disponíveis
    "formatted_availability": "Hoje até às 15:00",
    "availability": [
      "checkin",
      "book",
      "delivery"
    ]
  },
  "later_offers": [
    {
      "discount": 20,
      "details": ["Desconto na conta toda!", "Cortesia"],
      "benefits": "1 taça de vinho",
      "restrictions": "Não é válido para menu executivo",
      "seats": 4, //quantidade de assentos disponíveis
      "formatted_availability": "Quarta-feira das 10:00 as 15:00",
      "availability": [
        "checkin",
        "book",
        "delivery"
      ]
    }
  ],
  "offers": [
    {
      "discount": 20,
      "benefit": "nil",
      "restrictions": [
        "executivo",
        "rodizio"
      ],
      "custom_restriction": "restaurant.usage_restrictions.to_s",
      "formatted_availability": "Segunda a Sexta das 10:00 as 15:00",
      "starts_at": "I18n.localize",
      "ends_in": "I18n.localize()",
      "availability": [
        "checkin",
        "book",
        "delivery"
      ]
    },
    {
      "discount": 20,
      "benefit": "Ganhe um sorvete de chocolate por pessoa",
      "restrictions": [
        "executivo",
        "rodizio"
      ],
      "custom_restriction": "restaurant.usage_restrictions.to_s",
      "formatted_availability": "Segunda a Sexta das 10:00 as 15:00",
      "starts_at": "I18n.localize",
      "ends_in": "I18n.localize()",
      "availability": [
        "checkin",
        "book"
      ]
    }
  ],
  "website": "restaurant.site",
  "descriptions": [
    {
      "language": "pt-br",
      "text": "restaurant.description",
      "restrictions": "restaurant.usage_restrictions.to_s"
    }
  ],
  "formatted_phone_number": "979879798798",
  "review_count": 10,
  "average_rating": 5,
  "address": {
    "street": "restaurant",
    "number": "",
    "complement": "",
    "neighborhood": "neigh",
    "location": {
      "latitude": 23.99999999,
      "longitude": 47.999999999
    },
    "city": "rio de janeiro",
    "state": "rj"
  },
  "photos": [
    {
      "type": "profile",
      "url": "https://dqwr636hdjha6.cloudfront.net/uploads/restaurant_picture/picture/29861/width704_13443154_1087046398029389_3509458878559132905_o.jpg"
    },
    {
      "type": "cover",
      "url": "https://dqwr636hdjha6.cloudfront.net/uploads/restaurant_picture/picture/29861/width704_13443154_1087046398029389_3509458878559132905_o.jpg"
    },
    {
      "type": "gallery",
      "url": "https://dqwr636hdjha6.cloudfront.net/uploads/restaurant_picture/picture/29861/width704_13443154_1087046398029389_3509458878559132905_o.jpg"
    }
  ],
  "main_cuisine ": "Brasileira",
  "cuisines": [
    "brasileira",
    "contemporanea"
  ]
}
```

### URL Parameters

Parameter | Description
--------- | -----------
uuid | the restaurant uuid

### HTTP Request


`GET https://search.chefsclub.com.br/api/v6/restaurants/<UUID>`


## Highlighted Restaurants

```shell
curl https://search.chefsclub.com.br/api/v6/restaurants/highlights \
  -i -X GET \
  -H "Content-Type: application/json"
  -d 'area=sao-paulo'
```

> The above command returns JSON structured like this:

```json
{
  "metadata": {
    "results_found": 3,
    "time_in_milliseconds": 4,
    "pagination": {
      "current_page": 1,
      "total_pages": 70,
      "per_page": 2,
      "next_page": 2,
      "previous_page": null
    }
  },
  "highlights" : [
    "type": "restaurant_grid",
    "title": "Disponiveis por perto",
    "call_to_action": "Ver todos proximos",
    "selected_filters": {
        "seats":1,
        "order":"nearest"
    },
    "restaurants": [
      {
        "uuid": "4885-ssdfsdfdsf-fdsf-34534",
        "name": "Lá no Escondidinho",
        "main_cuisine": "Brasileira",
        "address": {
          "neighbourhood": "Brooklin",
          "latitude": 32425658679070,
          "longitude": 4353474574577
        },
        "photos": [
          {
            "type": "profile",
            "url": "https://dqwr636hdjha6.cloudfront.net/uploads/restaurant_picture/picture/29861/width704_13443154_1087046398029389_3509458878559132905_o.jpg"
          }
        ],
        "available_offers": [
          "checkin",
          "book",
          "delivery"
        ],
        "offers": [
          {
            "discount": 20,
            "benefit": "ganhe uma sobremesa"
          }
        ],
        "average_rating": 4.6
      }
    ]
  ]
}
```

###  URL Parameters

Parameter | Description
--------- | -----------
latitude |
longititude |
area | The area slug to retrieve the highlights

### HTTP Request

`GET https://search.chefsclub.com.br/api/v6/restaurants/highlights`



## Search by Name (Autocomplete)

```shell
curl https://search.chefsclub.com.br/api/v6/restaurants/autocomplete \
  -i -X GET \
  -H "Content-Type: application/json"
  -d 'q=Buda'
```

> The above command returns JSON structured like this:

```json
{
  "metadata": {
    "results_found": 1737,
    "time_in_milliseconds": 4,
    "pagination": {
      "current_page": 1,
      "total_pages": 70,
      "has_next_page": true,
      "has_previous_page": false,
      "next_page": 2,
      "previous_page": null
    }
  },
  "restaurants": [
    {
      "uuid": "4885-ssdfsdfdsf-fdsf-34534",
      "name": "Lá no Escondidinho",
      "main_cuisine": "Brasileira",
      "address": {
        "neighbourhood": "Brooklin",
        "latitude": 32425658679070,
        "longitude": 4353474574577
      },
      "photos": [
        {
          "type": "profile",
          "url": "https://dqwr636hdjha6.cloudfront.net/uploads/restaurant_picture/picture/29861/width704_13443154_1087046398029389_3509458878559132905_o.jpg"
        }
      ],
      "available_offers": [
        "checkin",
        "book",
        "delivery"
      ],
     "offers": [
        {
          "discount": 20,
          "benefit": "ganhe uma sobremesa"
        }
      ],
      "average_rating": 4.6
    }
  ]
}
```

###  URL Parameters

Parameter | Description
--------- | -----------
q | The search term

### HTTP Request

`GET https://search.chefsclub.com.br/api/v6/restaurants/autocomplete`




## Reservation availability

```shell
curl https://search.chefsclub.com.br/api/v6/restaurants/12344-1dks923-2938d/availability \
  -i -X GET \
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{ "availabilities":
  [
    {
      "maximium_seats": 20,
      "available_dates": [
        "2017-01-20",
        "2017-01-21",
        "2017-01-22",
        "2017-01-23",
        "2017-01-24",
        "2017-01-25"
      ],
      "available_hours":{
        "2017-01-20": [
          "12:00",
          "12:30",
          "13:00",
          "13:30",
          "14:00",
          "14:30"
        ]
      }
    }
  ]
}
```

###  URL Parameters

Parameter | Description
--------- | -----------
seats | Number of seats(people) to reserver
date | The date to retreave the times

### HTTP Request

`GET https://search.chefsclub.com.br/api/v6/restaurants/<UUID>/availability`


# Reviews

## Retrieve Reviews (V2)
```shell
curl https://account.chefsclub.com.br/api/v2/restaurants/{restaurantId}/reviews \
  -i -X GET \
  -H "Content-Type: application/json" \
  -H "X-Client-Access-Token: access_token" \
```

> The above command returns JSON structured like this:

```json
{
  "average_rating":5.0,
  "reviews_count":2,
  "rating_distribution":{"1":1,"4":2,"5":5},
  "reviews":[
    {
      "rating":4,
      "comment": "Muito bom!",
      "aspects":[{"type" : "Desconto obtido"},{"type" : "Qualidade da comida"}],
      "created_at":"2017-04-16T21:37:11-03:00",
      "author_name":"Claudio Augusto"
    },
    {
      "rating":5,
      "comment":null,
      "aspects":[{"type" : "Variedade do cardápio"},{"type" : "Atendimento"},{"type" : "Desconto obtido"},{"type" : "Qualidade da comida"}],
      "created_at":"2017-02-13T00:24:35-02:00",
      "author_name":"Beatriz M."
    }
  ]
}

```
###  URL Parameters

Parameter | Description
--------- | -----------
restaurant_id | Id do restaurante.
page |  Página desejada



## Retrieve review (V3)

Given a customer made a validation (usage) can it write a review (see 'Create a review to Usage').
This endpoint, allows retrieving the list of reviews to Restaurant.

### Example of request

```shell
curl -X GET "//$troisgros_endpoint/api/v3/restaurants/:restaurant_uuid/reviews"
  -H "Content-Type: application/json" \
  -H "X-Client-Access-Token: $ACCESS_TOKEN" \
```

#### Example of response

```json
{
  "average_rating": 3.25,
  "reviews_count": 4,
  "rating_distribution": {
    "2": 1,
    "3": 2,
    "5": 1
  },
  "rating_histogram": {
    "2": 1,
    "3": 2,
    "5": 1
  },
  "reviews": [
    {
      "rating": 5,
      "comment": "Architecto soluta similique aut. Voluptatem magni tenetur dolorem qui. At accusamus laudantium dolorem fugiat et perferendis.",
      "aspects": [ { "type": "Desconto obtido" }, { "type": "Qualidade da comida" } ],
      "created_at": "2018-08-16T11:22:49.746-03:00",
      "author_name": "Murilo"
    },
    {
      "rating": 3,
      "comment": "Architecto soluta similique aut. Voluptatem magni tenetur dolorem qui. At accusamus laudantium dolorem fugiat et perferendis.",
      "aspects": [ { "type": "Desconto obtido" }, { "type": "Qualidade da comida" } ],
      "created_at": "2018-08-16T11:22:49.919-03:00",
      "author_name": "Rafael"
    },
    {
      "rating": 3,
      "comment": "Architecto soluta similique aut. Voluptatem magni tenetur dolorem qui. At accusamus laudantium dolorem fugiat et perferendis.",
      "aspects": [ { "type": "Atendimento" }, { "type": "Ambiente" } ],
      "created_at": "2018-08-16T11:22:49.820-03:00",
      "author_name": "Suélen"
    },
    {
      "rating": 2,
      "comment": "Architecto soluta similique aut. Voluptatem magni tenetur dolorem qui. At accusamus laudantium dolorem fugiat et perferendis.",
      "aspects": [ { "type": "Atendimento" }, { "type": "Ambiente" }, { "type": "Desconto obtido" } ],
      "created_at": "2018-08-16T11:22:50.011-03:00",
      "author_name": "Yago"
    }
  ],
  "metadata": {
    "pagination": {
      "current_page": 1,
      "per_page": 10,
      "total_results": 4
    }
  }
}
```

Can you paginate you results using metadata parameters, `:per_page` and `:page`

### HEADERS

Header | Description
------ | -----------
X-Client-Access-Token | Client Access token

### URL Parameters

Parameter | Description | Rule
--------- | ----------- | ----
restaurant_uuid | UUID of restaurant target | Required
page | The page number offset | Optional, Default 1
per_page | Amount of results per page | Optional, default 10


# Filters

## Retrieve filters

```shell
curl https://search.chefsclub.com.br/api/v6/filters \
  -i -X GET \
  -H "Content-Type: application/json" \
  -d 'area=sao-paulo'
```

> The above command returns JSON structured like this:


```json
{
  "filters": [
    {
      "type": "city",
      "load_more": false,
      "results": []
    },
    {
      "type": "order",
      "load_more": false,
      "results": [
        {
          "id": "recommended",
          "slug": "nome-do-slug",
          "name": "Recomendados"
        },
        {
          "id": "nearest",
          "slug": "nome-do-slug",
          "name": "Mais proximos"
        },
        {
          "id": "newest",
          "slug": "nome-do-slug",
          "name": "Novidades"
        },
        {
          "id": "ranking",
          "slug": "nome-do-slug",
          "name": "Destaques"
        }
      ]
    },
    {
      "type": "available_offer"
      "load_more": false,
      "results": []
    },
    {
      "type": "seats",
      "load_more": false,
      "results": []
    },
    {
      "type": "date",
      "load_more": false,
      "results": []
    },
    {
      "type": "hour",
      "load_more": false,
      "results": []
    },
    {
      "type": "cuisine",
      "load_more": true,
      "results": [
        {
          "id": 2,
          "slug": "nome-do-slug",
          "name": "Brasileira"
        },
        {
          "id": 8,
          "slug": "nome-do-slug",
          "name": "ContemporiÂ¢nea"
        },
        {
          "id": 5,
          "slug": "nome-do-slug",
          "name": "Italiana"
        },
        {
          "id": 13,
          "slug": "nome-do-slug",
          "name": "Japonesa"
        },
        {
          "id": 15,
          "slug": "nome-do-slug",
          "name": "Pizza"
        },
        {
          "id": 14,
          "slug": "nome-do-slug",
          "name": "Variada"
        }
      ]
    },
    {
      "type": "category",
      "load_more": false,
      "results": [
        {
          "id": 1,
          "slug": "nome-do-slug",
          "name": "a la carte"
        },
        {
          "id": 10,
          "slug": "nome-do-slug",
          "name": "Bar"
        },
        {
          "id": 8,
          "slug": "nome-do-slug",
          "name": "Buffet"
        },
        {
          "id": 7,
          "slug": "nome-do-slug",
          "name": "Cafeteria"
        },
        {
          "id": 4,
          "slug": "nome-do-slug",
          "name": "Comida rápida"
        },
        {
          "id": 6,
          "slug": "nome-do-slug",
          "name": "Executivo"
        },
        {
          "id": 5,
          "slug": "nome-do-slug",
          "name": "Food Truck"
        },
        {
          "id": 3,
          "slug": "nome-do-slug",
          "name": "Rodizio"
        },
        {
          "id": 11,
          "slug": "nome-do-slug",
          "name": "SaudiÂ¡vel"
        },
        {
          "id": 12,
          "slug": "nome-do-slug",
          "name": "Sobremesa"
        }
      ]
    },
    {
      "type": "price_range",
      "load_more": false,
      "results": [
        {
          "id": 1,
          "slug": "nome-do-slug",
          "name": "Até R$25 por pessoa"
        },
        {
          "id": 2,
          "slug": "nome-do-slug",
          "name": "De R$25 até R$50 por pessoa"
        },
        {
          "id": 3,
          "slug": "nome-do-slug",
          "name": "De R$50 até R$75 por pessoa"
        },
        {
          "id": 4,
          "slug": "nome-do-slug",
          "name": "De R$75 até R$100 por pessoa"
        },
        {
          "id": 5,
          "slug": "nome-do-slug",
          "name": "Acima de R$100 por pessoa"
        }
      ]
    },
    {
      "type": "neighbourhood",
      "load_more": true,
      "results": [
        {
          "id": 6,
          "slug": "nome-do-slug",
          "name": "Itaim Bibi"
        },
        {
          "id": 1,
          "slug": "nome-do-slug",
          "name": "Jardins"
        },
        {
          "id": 5,
          "slug": "nome-do-slug",
          "name": "Moema"
        },
        {
          "id": 13,
          "slug": "nome-do-slug",
          "name": "Perdizes"
        },
        {
          "id": 3,
          "slug": "nome-do-slug",
          "name": "Pinheiros"
        },
        {
          "id": 12,
          "slug": "nome-do-slug",
          "name": "Vila Olimpia"
        }
      ]
    }
  ]
}
```

### HTTP Request

`GET https://search.chefsclub.com.br/api/v6/filters`

###  URL Parameters

Parameter | Description
--------- | -----------
area | The area slug to retrieve the filters for that area

## Get filters

```shell
curl https://search.chefsclub.com.br/api/v6/filters/cuisine  \
  -i -X GET \
  -H "Content-Type: application/json" \
  -d 'area=sao-paulo' \
  -d 'neighbourhood_ids=1,2' \
```

> The above command returns JSON structured like this:

```json
{
  "filters": [
    {
      "type": "cuisine",
      "load_more": true,
      "results": [
        {
          "id": 2,
          "slug": "nome-do-slug",
          "name": "Brasileira"
        },
        {
          "id": 8,
          "slug": "nome-do-slug",
          "name": "Contemporienea"
        },
        {
          "id": 5,
          "slug": "nome-do-slug",
          "name": "Italiana"
        },
        {
          "id": 13,
          "slug": "nome-do-slug",
          "name": "Japonesa"
        },
        {
          "id": 15,
          "slug": "nome-do-slug",
          "name": "Pizza"
        },
        {
          "id": 14,
          "slug": "nome-do-slug",
          "name": "Variada"
        }
      ]
    }
  ]
}
```

###  URL Parameters

Parameter | Description
--------- | -----------
neighbourhood_ids | Filtra por bairro. É possível filtrar por múltiplos bairros separados por virgula
cuisine_ids |  Filtra por categoria. É possível iltrar por múltiplas categorias separados por virgula
price_range |  Filtra por faixa de preço Possible values:  2 , 3 , 4 , 5
offers | Filtra por tipo de disponibilidade. É possível especificar múltiplos sources. Possible values: checkin, booking, delivery.
seats | Filtra por disponibilidade de número de pessoas
date |  Filtra por data hora, formato ISO8601(yyyy-mm-dd)
time | Filtra por hora, Possible values:  search_next , lunch , dinner , all , HH:MM.

### HTTP Request

`GET https://search.chefsclub.com.br/api/v6/filters/<FILTER_TYPE>`


# Surveys (V3)

## Get surveys

To grab specific survey to the usage can you use:

`GET //:troisgros_endpoint/api/v3/surveys/:usage_id`

### Example of request

```shell
curl -X GET "$troisgros_endpoint/api/v3/surveys/$usage_id" \
  -H 'Content-Type: application/json'
  -H 'X-Client-Access-Token: $X_Client_Access_Token
```

### Example of response

```json
{
    "questions": [
        {
            "id": 1,
            "icon": "some-positive-icon",
            "title": "Do que você mais gostou?",
            "subtitle": "Você pode selecionar várias opções",
            "type": "multiple",
            "aspects": [
                { "id": 1, "type": "Custo x benefício" },
                { "id": 2, "type": "Qualidade da comida" },
                { "id": 3, "type": "Variedade do cardápio" },
                { "id": 4, "type": "Atendimento" },
                { "id": 5, "type": "Ambiente e decoração" }
            ]
        },
        {
            "id": 2,
            "icon": "some-positive-icon",
            "title": "Você recomendaria para?",
            "subtitle": "Você pode selecionar várias opções",
            "type": "multiple",
            "aspects": [
                { "id": 6, "type": "Jantar romântico" },
                { "id": 7, "type": "Ir com a família" },
                { "id": 8, "type": "Almoço de negócios" },
                { "id": 9, "type": "Ir com amigos" },
                { "id": 10, "type": "Happy Hour" },
                { "id": 11, "type": "Comer rápido" }
            ]
        }
    ]
}
```

## Write a Survey

`POST //:troisgros_endpoint/api/v3/surveys/`


##Example of request

```shell
curl -X POST "$troisgros_endpoint/api/v3/surveys/" \
  -H 'Contente-Type: application/json'
  -H "X-Client-Access-Token: $X_CLIENT_ACCESS_TOKEN"
  -d '
    {
      "usuario_id": "$X_CLIENT_ACCESS_TOKEN",
      "usage_id": "$usage_id",
      "questions": [
        { "id": 1, "answers": ["Qualidade da comida", "Ambiente e decoração", "Atendimento"] },
        { "id": 2, "answers": ["Happy Hour", "Comer rápido"] }
      ]
    }
  '
```

-----

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
