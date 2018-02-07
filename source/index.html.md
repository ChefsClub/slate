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


---


# API de Busca de Restaurantes

Essa API tem um outro endpoint.

# Areas

## Retrieve Areeas

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
          "type": "thumb",
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
latitude |
longititude |
area_id | The area ID to retrieve the highlights

### HTTP Request

`GET https://search.chefsclub.com.br/api/v6/restaurants`

## Get a restaurant

```shell
curl https://search.chefsclub.com.br/api/v6/restaurants/12344-1dks923-2938d` \
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
      "type": "thumb",
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
    "contemporÃ¢nea"
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
  -d 'area_id=14'
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
          "type": "thumb",
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
latitude |
longititude |
area_id | The area ID to retrieve the highlights

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
          "type": "thumb",
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

# Filters

## Retrieve filters

`GET https://search.chefsclub.com.br/api/v6/filters`

## Get filters

```shell
curl https://search.chefsclub.com.br/api/v6/filters \
  -i -X GET \
  -H "Content-Type: application/json" \
  -H "X-Client-Access-Token: XG1x8CxbQsOYViQpmS8rAm6GEhyMxxCuv_DFzZ4AvA8ybhusdDioafMgSHa1d-WW_T7UEqH0_HdmiSgOVQ4xH8okSwGRN_UhJ7wh1O-GKo9VZ9FWOQu_lpYMXXZIJKHa-pmo7ULJ0TIOYHV83y-9HPYY2OlWpFEYyg3eih0OvecaMQGO9JH9hHp7Qfw5Vs3gn_ThLZnvzlIsvv6xJkzTXCaYnuLoYzRcNCeAbug96fs=" \
  -d '{ ... }'
```

> The above command returns JSON structured like this:

```json
{
  "filters": [
    {
      "type": "city",
      "load_more": false,
      "results": [
        {
          "id": 27,
          "slug": "nome-do-slug",
          "name": "Belo Horizonte"
        },
        {
          "id": 11,
          "slug": "nome-do-slug",
          "name": "Brasilia"
        },
        {
          "id": 26,
          "slug": "nome-do-slug",
          "name": "Campinas e regiao"
        },
        {
          "id": 22,
          "slug": "nome-do-slug",
          "name": "Curitiba"
        },
        {
          "id": 30,
          "slug": "nome-do-slug",
          "name": "Porto Alegre"
        },
        {
          "id": 21,
          "slug": "nome-do-slug",
          "name": "Rio de Janeiro"
        },
        {
          "id": 1,
          "slug": "nome-do-slug",
          "name": "Sao Paulo"
        }
      ]
    },
    {
      "type": "people",
      "load_more": false,
      "results": []
    },
    {
      "type": "availability",
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
          "name": "Comida riÂ¡pida"
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
      "type": "ticket",
      "load_more": false,
      "results": [
        {
          "id": 1,
          "slug": "nome-do-slug",
          "name": "AtiÂ© R$25 por pessoa"
        },
        {
          "id": 2,
          "slug": "nome-do-slug",
          "name": "De R$25 atiÂ© R$50 por pessoa"
        },
        {
          "id": 3,
          "slug": "nome-do-slug",
          "name": "De R$50 atiÂ© R$75 por pessoa"
        },
        {
          "id": 4,
          "slug": "nome-do-slug",
          "name": "De R$75 atiÂ© R$100 por pessoa"
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
    }
  ]
}
```





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
