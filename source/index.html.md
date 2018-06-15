---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ

toc_footers:
  - <a href='https://equiratings.com'>Powered by EquiRatings</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to EquiRatings API for Eventing. You can use this API to upload and
manage all aspects of your eventing records. Through the Eventing API
endpoints you can upload and get ERQI information.

Currently our API supports REST Https calls which you can consume using cURL or
directly using whatever HTTP wrapper your language of choice supports.

Currently the API is in Beta, and it is subject to change. Don't worry we will
inform our partners about any changes long before we deploy.

# Authentication

The Eventing API uses JWT tokens for authentication. Please contact EquiRatings
in order to get set-up on our system. Once you have been assigned a user for your
provider account, you will be able to login to the API using the Sessions
endpoint.

With each request you will need to supply an authorization header. The header
should look like this:

`Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9`

Except your real token will be a lot longer.

<aside class="notice">
You must replace <code>eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9</code> with your own token.
</aside>

Your token will be valid for two weeks from when you create a new session.

# Sessions

## Create a session

```shell
curl -XPOST
     -H "Content-type: application/json"
     -d '{"email": "user@domain.com", "password": "abcd1234"}'
		 'https://eventing.api.equiratings.com/v1/sessions'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "token",
    "links": {
      "self": "/sessions"
    },
    "id": "",
    "attributes": {
      "refresh_token": "jsdlka;fjl;kfjaljfslkjfslkjflkjoiwejwi232434$#%##",
      "access_token": "eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9"
    }
  }
}
```

Provided the user credentials are correct the endpoint will return a valid authorization token for the API.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/sessions`

### Query Parameters

This endpoint does not support query parameters.

## Get a Session

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/sessions'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "user",
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/users/103"
    },
    "id": "103",
    "attributes": {
      "surname": "Surname",
      "role": "provider_admin",
      "id": 103,
      "first_name": "First",
      "email": "email@domain.com"
    }
  }
}
```

Gets the user information for the supplied authorization token.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/sessions`

### Query Parameters

This endpoint does not support query parameters.

# Token

## Create a token

```shell
curl -XPOST
     -H "Content-type: application/json"
     -d '{"refresh_token": "jsdlka;fjl;kfjaljfslkjfslkjflkjoiwejwi232434$#%##"}'
		 'https://eventing.api.equiratings.com/v1/tokens'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "token",
    "links": {
      "self": "/v1/tokens"
    },
    "id": "",
    "attributes": {
      "refresh_token": "jsdlka;fjl;kfjaljfslkjfslkjflkjoiwejwi232434$#%##",
      "access_token": "eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9"
    }
  }
}
```

Provided the refresh token has not expired. It will be used to generate a new
access token.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/tokens`

### Query Parameters

This endpoint does not support query parameters.

# Users

## Get all Users

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/users'
```

> The above command returns JSON structured like this:

```json
{
  "links": {
    "self": "/v1/users?page[page]=1&page[page_size]=50"
  },
  "jsonapi": {
    "version": "1.0"
  },
  "data": [
    {
      "type": "user",
      "relationships": {
        "token": {
          "data": null
        }
      },
      "links": {
        "self": "/users/90"
      },
      "id": "90",
      "attributes": {
        "surname": "Surname",
        "role": "provider_admin",
        "id": 90,
        "first_name": "First",
        "email": "email90@domain.com"
      }
    }
  ]
}
```

Returns all users for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/users`

### Query Parameters

This endpoint supports query parameters for paging:

| Parameter         | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| page[page]        | **Integer**<br>The number of the page to be returned.                                                   |
| page[page_size]   | **Integer**<br>The number of records per page. <br>This is a read-only parameter and is locked at 50.   |

Predefined paging URLs are also returned within the json payload.

## Get a Specific User

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/users/1'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "user",
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/users/96"
    },
    "id": "96",
    "attributes": {
      "surname": "Surname",
      "role": "provider_admin",
      "id": 96,
      "first_name": "First",
      "email": "email13@domain.com"
    }
  }
}
```

Returns a user for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/users/:id`

### URL Parameters

| Parameter | Description                                              |
| --------- | -------------------------------------------------------- |
| ID        | **Integer (required)**<br>The internal EquiRatings API ID of the user to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a User

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"user": {"first_name": "New", "surname": "User", "email": "new_user@domain.com", "password": "abcd1234", "role": "provider_user"}}'
     'https://eventing.api.equiratings.com/v1/users'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "user",
        "relationships": {
            "token": {
                "data": null
            }
        },
        "links": {
            "self": "/users/11"
        },
        "id": "11",
        "attributes": {
            "surname": "User",
            "role": "provider_user",
            "id": 11,
            "first_name": "New",
            "email": "new_user@domain.com"
        }
    }
}
```

Create a user for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/users/`

### Attributes

| Parameter  | Description                                                                                             |
| ---------- | ------------------------------------------------------------------------------------------------------- |
| first_name | **String (required)**<br>The first name of the user                                                     |
| surname    | **String (required)**<br>The surname of the user                                                        |
| email      | **String (required)**<br>The email of the user                                                          |
| password   | **String (required)**<br>The password of the user, must be at least 8 characters                        |
| roles      | **String (required)**<br>The user role, valid roles are as follows: ["provider_admin", "provider_user"] |

### Query Parameters

This endpoint does not support query parameters.

## Update a User

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"user": {"first_name": "Updated", "password": "abcd1234"}}'
     'https://eventing.api.equiratings.com/v1/users/11'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "user",
        "relationships": {
            "token": {
                "data": null
            }
        },
        "links": {
            "self": "/users/11"
        },
        "id": "11",
        "attributes": {
            "surname": "User",
            "role": "provider_user",
            "id": 11,
            "first_name": "Updated",
            "email": "new_user@domain.com"
        }
    }
}
```

Update a user for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/users/:id`

### Attributes

| Parameter  | Description                                                                                  |
| ---------- | -------------------------------------------------------------------------------------------- |
| first_name | **String**<br>The first name of the user                                                     |
| surname    | **String**<br>The surname of the user                                                        |
| email      | **String**<br>The email of the user                                                          |
| password   | **String (required)**<br>The password of the user, must be at least 8 characters             |
| roles      | **String**<br>The user role, valid roles are as follows: ["provider_admin", "provider_user"] |

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The internal EquiRatings API ID of the user to update   |

### Query Parameters

This endpoint does not support query parameters.

## Delete a User

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/users/11'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a user with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/users/:id`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The internal EquiRatings API ID of the user to delete   |

### Query Parameters

This endpoint does not support query parameters.

# Federations

## Get all Federations

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/federations'
```

> The above command returns JSON structured like this:

```json
{
    "links": {
        "self": "/v1/federations?page[page]=1&page[page_size]=50",
        "next": "/v1/federations?page[page]=2&page[page_size]=50",
        "last": "/v1/federations?page[page]=3&page[page_size]=50"
    },
    "jsonapi": {
        "version": "1.0"
    },
    "data": [
		{
			"type": "federation",
			"links": {
				"self": "/federations/188"
			},
			"id": "188",
			"attributes": {
				"name": "HORSE SPORT IRELAND",
				"id": 188,
				"code": "IRL"
			}
		},
		{
			"type": "federation",
			"links": {
				"self": "/federations/176"
			},
			"id": "176",
			"attributes": {
				"name": "BRITISH EQUESTRIAN FEDERATION",
				"id": 176,
				"code": "GBR"
			}
		}
	]
}
```

Returns all federation for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/federations`

### Query Parameters

This endpoint supports query parameters for paging:

| Parameter         | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| page[page]        | **Integer**<br>The number of the page to be returned.                                                   |
| page[page_size]   | **Integer**<br>The number of records per page. <br>This is a read-only parameter and is locked at 50.   |

Predefined paging URLs are also returned within the json payload.

## Get a Specific Federation

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/federations/188'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "federation",
        "links": {
            "self": "/federations/188"
        },
        "id": "188",
        "attributes": {
            "name": "HORSE SPORT IRELAND",
            "id": 188,
            "code": "IRL"
        }
    }
}
```

Returns a federation for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/federations/:id`

### URL Parameters

| Parameter | Description                          |
| --------- | ------------------------------------ |
| ID        | The internal EquiRatings API ID of the federation to retrieve |

### Query Parameters

This endpoint does not support query parameters.

# Athletes

## Get all Athletes

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/athletes'
```

> The above command returns JSON structured like this:

```json
{
    "links": {
        "self": "/v1/athletes?page[page]=1&page[page_size]=50"
    },
    "jsonapi": {
        "version": "1.0"
    },
    "data": [
        {
            "type": "athlete",
            "links": {
                "self": "/v1/athletes/27996"
            },
            "id": "27996",
            "attributes": {
                "surname": "Taylor",
                "source_id": "002",
                "nationality": "GBR",
                "id": 27996,
                "gender": "female",
                "first_name": "Isabelle",
                "fei_id": 10004377,
                "federation_id": 176,
                "dob": "1983-06-11",
                "display_name": "Izzy Taylor"
            }
        },
        {
            "type": "athlete",
            "links": {
                "self": "/v1/athletes/27995"
            },
            "id": "27995",
            "attributes": {
                "surname": "Watson",
                "source_id": "001",
                "nationality": "IRL",
                "id": 27995,
                "gender": "male",
                "first_name": "Sam",
                "fei_id": 10007367,
                "federation_id": 188,
                "dob": "1982-01-14",
                "display_name": "Sam Watson"
            }
        }
    ]
}
```

Returns all athlete for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/athletes`

### Query Parameters

This endpoint supports query parameters for paging:

| Parameter         | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| page[page]        | **Integer**<br>The number of the page to be returned.                                                   |
| page[page_size]   | **Integer**<br>The number of records per page. <br>This is a read-only parameter and is locked at 50.   |

Predefined paging URLs are also returned within the json payload.

## Get a Specific Athlete

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/athletes/27995'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "athlete",
        "links": {
            "self": "/v1/athletes/27995"
        },
        "id": "27995",
        "attributes": {
            "surname": "Watson",
            "source_id": "001",
            "nationality": "IRL",
            "id": 27995,
            "gender": "male",
            "first_name": "Sam",
            "fei_id": 10007367,
            "federation_id": 188,
            "dob": "1982-01-14",
            "display_name": "Sam Watson"
        }
    }
}
```

Returns a athlete for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/athletes/:id`

### URL Parameters

| Parameter | Description                       |
| --------- | --------------------------------- |
| ID        | The internal EquiRatings API ID of the athlete to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Athlete

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"athlete": {"surname": "Athlete", "nationality": "IRL", "gender": "non binary", "first_name": "New", "fei_id": 12345678, "dob": "1900-01-01", "source_id": "003", "display_name": "New Athlete", "federation_id": "188"}}'
     'https://eventing.api.equiratings.com/v1/athletes'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "athlete",
        "links": {
            "self": "/v1/athletes/27997"
        },
        "id": "27997",
        "attributes": {
            "surname": "Athlete",
            "source_id": "003",
            "nationality": "IRL",
            "id": 27997,
            "gender": "non binary",
            "first_name": "New",
            "fei_id": 12345678,
            "federation_id": 188,
            "dob": "1900-01-01",
            "display_name": "New Athlete"
        }
    }
}
```

Create a athlete for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/athletes/`

### Attributes

| Parameter     | Description                                                                                   |
| ------------- | --------------------------------------------------------------------------------------------- |
| first_name    | **String (required)**<br>The first name of the athlete                                        |
| surname       | **String (required)**<br>The surname of the athlete                                           |
| gender        | **String (required)**<br>The gender of the athlete                                            |
| nationality   | **String (required)**<br>The nationality of the athlete (ISO country code)                    |
| dob           | **Date**<br>The date of birth of the athlete (YYYY-MM-DD)                                     |
| display_name  | **String**<br>The name that is displayed for the athlete if it is different to their name     |
| fei_id        | **Integer**<br>The fei_id of the athlete                                                      |
| federation_id | **Integer**<br>The internal EquiRatings API ID of the federation the athlete belongs to       |
| source_id     | **String (required)**<br>The ID that the Provider uses locally on their own system            |

### Query Parameters

This endpoint does not support query parameters.

## Update an Athlete

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"athlete": {"display_name": "Updated Athlete"}'
     'https://eventing.api.equiratings.com/v1/athletes/27997'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "athlete",
        "links": {
            "self": "/v1/athletes/27997"
        },
        "id": "27997",
        "attributes": {
            "surname": "Athlete",
            "source_id": "003",
            "nationality": "IRL",
            "id": 27997,
            "gender": "non binary",
            "first_name": "New",
            "fei_id": 12345678,
            "federation_id": 188,
            "dob": "1900-01-01",
            "display_name": "Updated Athlete"
        }
    }
}
```

Update a athlete for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/athletes/:id`

### Attributes

| Parameter     | Description                                                                                   |
| ------------- | --------------------------------------------------------------------------------------------- |
| first_name    | **String**<br>The first name of the athlete                                                   |
| surname       | **String**<br>The surname of the athlete                                                      |
| gender        | **String**<br>The gender of the athlete                                                       |
| nationality   | **String**<br>The nationality of the athlete (ISO country code)                               |
| dob           | **Date**<br>The date of birth of the athlete (YYYY-MM-DD)                                     |
| display_name  | **String**<br>The name that is displayed for the athlete if it is different to their name     |
| fei_id        | **Integer**<br>The fei_id of the athlete                                                      |
| federation_id | **Integer**<br>The internal EquiRatings API ID of the federation the athlete belongs to       |
| source_id     | **String**<br>The ID that the Provider uses locally on their own system                       |

### URL Parameters

| Parameter | Description                       |
| --------- | --------------------------------- |
| ID        | The internal EquiRatings API ID of the athlete to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Athlete

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/athletes/27997'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a athlete with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/athletes/:id`

### URL Parameters

| Parameter | Description                       |
| --------- | --------------------------------- |
| ID        | The internal EquiRatings API ID of the athlete to retrieve |

### Query Parameters

This endpoint does not support query parameters.

# Horses

## Get all Horses

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/horses'
```

> The above command returns JSON structured like this:

```json
{
    "links": {
        "self": "/v1/horses?page[page]=1&page[page_size]=50"
    },
    "jsonapi": {
        "version": "1.0"
    },
    "data": [
        {
            "type": "horse",
            "links": {
                "self": "/v1/horses/54738"
            },
            "id": "54738",
            "attributes": {
                "ueln": null,
                "source_id": "001",
                "risk_data": [],
                "name": "Horseware Bushman",
                "id": 54738,
                "gender": "Gelding",
                "fei_id": "IRL03630",
                "dob": "1999-05-24",
                "display_name": "Horseware Bushman"
            }
        },
        {
            "type": "horse",
            "links": {
                "self": "/v1/horses/54739"
            },
            "id": "54739",
            "attributes": {
                "ueln": null,
                "source_id": "002",
                "risk_data": [],
                "name": "Mr Bass",
                "id": 54739,
                "gender": "Gelding",
                "fei_id": "104KA86",
                "dob": "2008-06-19",
                "display_name": "Mr Bass"
            }
        }
    ]
}
```

Returns all horse for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/horses`

### Query Parameters

This endpoint supports query parameters for paging:

| Parameter         | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| page[page]        | **Integer**<br>The number of the page to be returned.                                                   |
| page[page_size]   | **Integer**<br>The number of records per page. <br>This is a read-only parameter and is locked at 50.   |

Predefined paging URLs are also returned within the json payload.

## Get a Specific Horse

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/horses/54738'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "horse",
        "links": {
            "self": "/v1/horses/54738"
        },
        "id": "54738",
        "attributes": {
            "ueln": null,
            "source_id": "001",
            "risk_data": [],
            "name": "Horseware Bushman",
            "id": 54738,
            "gender": "Gelding",
            "fei_id": "IRL03630",
            "dob": "1999-05-24",
            "display_name": "Horseware Bushman"
        }
    }
}
```

Returns a horse for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/horses/:id`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The internal EquiRatings API ID of the horse to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Horse

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"horse": {"name": "New Horse", "gender": "Gelding", "fei_id": "", "dob": "1900-01-01", "ueln": "", "source_id": "003", "display_name": "New Horse"}}'
     'https://eventing.api.equiratings.com/v1/horses'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "horse",
        "links": {
            "self": "/v1/horses/54740"
        },
        "id": "54740",
        "attributes": {
            "ueln": null,
            "source_id": "003",
            "risk_data": [],
            "name": "New Horse",
            "id": 54740,
            "gender": "Gelding",
            "fei_id": null,
            "dob": "1900-01-01",
            "display_name": "New Horse"
        }
    }
}
```

Create a horse for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/horses/`

### Attributes

| Parameter    | Description                                                                        |
| ------------ | ---------------------------------------------------------------------------------- |
| name         | **String (required)**<br>The name of the horse                                     |
| gender       | **String (required)**<br>The gender of the horse                                   |
| dob          | **Date (required)**<br>The date of birth of the horse (YYYY-MM-DD)                 |
| fei_id       | **String**<br>The fei id for the horse                                             |
| ueln         | **String**<br>The unique equine life number of the horse                           |
| display_name | **String**<br>The display name of the horse if different from the name             |
| source_id    | **String (required)**<br>The ID that the Provider uses locally on their own system |

### Query Parameters

This endpoint does not support query parameters.

## Update a Horse

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"horse": {"display_name": "Updated Horse"}}'
     'https://eventing.api.equiratings.com/v1/horses/54740'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "horse",
        "links": {
            "self": "/v1/horses/54740"
        },
        "id": "54740",
        "attributes": {
            "ueln": null,
            "source_id": "003",
            "risk_data": [],
            "name": "New Horse",
            "id": 54740,
            "gender": "Gelding",
            "fei_id": null,
            "dob": "1900-01-01",
            "display_name": "Updated Horse"
        }
    }
}
```

Update a horse for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/horses/:id`

### Attributes

| Parameter    | Description                                                             |
| ------------ | ----------------------------------------------------------------------- |
| name         | **String**<br>The name of the horse                                     |
| gender       | **String**<br>The gender of the horse                                   |
| dob          | **Date**<br>The date of birth of the horse (YYYY-MM-DD)                 |
| fei_id       | **String**<br>The fei id for the horse                                  |
| ueln         | **String**<br>The unique equine life number of the horse                |
| display_name | **String**<br>The display name of the horse if different from the name  |
| source_id    | **String**<br>The ID that the Provider uses locally on their own system |

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The internal EquiRatings API ID of the horse to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Horse

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/horses/54740'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a horse with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/horses/:id`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The internal EquiRatings API ID of the horse to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Risk data

### Returned values
When risk data is returned you will find an ERQI for each of the 13 er_levels, these each link to a competition level. Below is a list of what level each number represents:

 ER Level	| Competition Level
 --- | ----
1	| Competitions where the XC Course max fixed height is 80cm or 90cm
2	| Competitions where the XC Course max fixed height is 95cm or 100cm
3	| Competitions where the XC Course max fixed height is 105cm
4	| National competitions where the XC course max fixed height is 110cm
5	| CIC1* and FEI Introductory level
6	| CCI1*
7	| National competitions where the XC Course max fixed height is 115cm
8	| CIC2*
9	| CCI2*
10	| National competitions where the XC Course max fixed height is 120cm
11	| CIC3*
12 |	CCI3*
13 |	CCI4*



# Class Categories

## Get all Class Categories

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/class_categories'
```

> The above command returns JSON structured like this:

```json
{
    "links": {
        "self": "/v1/class_categories?page[page]=1&page[page_size]=50"
    },
    "jsonapi": {
        "version": "1.0"
    },
    "data": [
        {
            "type": "CCI",
            "links": {
                "self": "/v1/class_categories/146"
            },
            "id": "146",
            "attributes": {
                "type": "CCI",
                "name": "CCI1*",
                "level": "1",
                "id": 146,
                "er_level": 6
            }
        },
        {
            "type": "CCI",
            "links": {
                "self": "/v1/class_categories/147"
            },
            "id": "147",
            "attributes": {
                "type": "CCI",
                "name": "CCI2*",
                "level": "2",
                "id": 147,
                "er_level": 9
            }
        }
    ]
}
```

Returns all class_category records for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/class_categories`

### Query Parameters

This endpoint supports query parameters for paging:

| Parameter         | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| page[page]        | **Integer**<br>The number of the page to be returned.                                                   |
| page[page_size]   | **Integer**<br>The number of records per page. <br>This is a read-only parameter and is locked at 50.   |

Predefined paging URLs are also returned within the json payload.

## Get a Specific ClassCategory

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/class_categories/146'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "CCI",
        "links": {
            "self": "/v1/class_categories/146"
        },
        "id": "146",
        "attributes": {
            "type": "CCI",
            "name": "CCI1*",
            "level": "1",
            "id": 146,
            "er_level": 6
        }
    }
}
```

Returns a class_category for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/class_categories/:id`

### URL Parameters

| Parameter | Description                                                       |
| --------- | ----------------------------------------------------------------- |
| ID        | The internal EquiRatings API ID of the class_category to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a ClassCategory

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"class_category": {"type": "CCI", "name": "CCI3*", "level": "3"}}'
     'https://eventing.api.equiratings.com/v1/class_categories'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "CCI",
        "links": {
            "self": "/v1/class_categories/148"
        },
        "id": "148",
        "attributes": {
            "type": "CCI",
            "name": "CCI3*",
            "level": "3",
            "id": 148,
            "er_level": 12
        }
    }
}
```

Create a class_category for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/class_categories/`

### Attributes

| Parameter | Description                                                   |
| --------- | ------------------------------------------------------------- |
| type      | **String (required)**<br>The type of the class category (Allowed Class Types)      |
| name      | **String (required)**<br>The full name of the class category  |
| level     | **String (required)**<br>The level of the class category (Allowed Class Levels)     |

### Allowed Types and Levels

#### Allowed Class Types
* CCI - International 3-day
* CIC - International 1-day
* CCN - National 3-day
* CNC - National 1-day

#### Allowed Class Levels
This is the level of the competition, expressed as either height of jumps or FEI level.
* 4
* 3
* 2
* 1
* 105
* 100
* 95
* 90
* 80

#### Examples
| Class | name | type | level |
| --- | --- | --- | --- |
|CCI4* | CCI4 | CCI | 4 |
|CIC3* | CIC3 | CIC | 3 |
| Advanced | Advanced | CNC | 3 |
| Preliminary | Preliminary | CNC | 1 |
| CNC1 | CNC1| CNC | 1 |
| EvA95 | EvA95 | CNC | 95 |

### Query Parameters

This endpoint does not support query parameters.

## Update a ClassCategory

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"class_category": {"name": "Updated CCI3*"}}'
     'https://eventing.api.equiratings.com/v1/class_categories/148'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "CCI",
        "links": {
            "self": "/v1/class_categories/148"
        },
        "id": "148",
        "attributes": {
            "type": "CCI",
            "name": "Updated CCI3*",
            "level": "3",
            "id": 148,
            "er_level": 12
        }
    }
}
```

Update a class_category for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/class_categories/:id`

### Attributes

| Parameter | Description                                        |
| --------- | -------------------------------------------------- |
| type      | **String**<br>The type of the class category       |
| name      | **String**<br>The full name of the class category  |
| level     | **String**<br>The level of the class category      |

### URL Parameters

| Parameter | Description                                                       |
| --------- | ----------------------------------------------------------------- |
| ID        | The internal EquiRatings API ID of the class_category to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a ClassCategory

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/class_categories/146'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a class_category with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/class_categories/:id`

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| ID        | The internal EquiRatings API ID of the class_category to retrieve |

### Query Parameters

This endpoint does not support query parameters.

# Venues

## Get all Venues

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/venues'
```

> The above command returns JSON structured like this:

```json
{
    "links": {
        "self": "/v1/venues?page[page]=1&page[page_size]=50"
    },
    "jsonapi": {
        "version": "1.0"
    },
    "data": [
        {
            "type": "venue",
            "links": {
                "self": "/v1/venues/1"
            },
            "id": "1",
            "attributes": {
                "source_id": "001",
                "name": "First Venue",
                "id": 1,
                "federation_id": 176
            }
        },
        {
            "type": "venue",
            "links": {
                "self": "/v1/venues/2"
            },
            "id": "2",
            "attributes": {
                "source_id": "002",
                "name": "Second Venue",
                "id": 2,
                "federation_id": 176
            }
        }
    ]
}
```

Returns all venues for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/venues`

### Query Parameters

This endpoint supports query parameters for paging:

| Parameter         | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| page[page]        | **Integer**<br>The number of the page to be returned.                                                   |
| page[page_size]   | **Integer**<br>The number of records per page. <br>This is a read-only parameter and is locked at 50.   |

Predefined paging URLs are also returned within the json payload.

## Get a Specific Venue

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/venues/1'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "venue",
        "links": {
            "self": "/v1/venues/1"
        },
        "id": "1",
        "attributes": {
            "source_id": "001",
            "name": "First Venue",
            "id": 1,
            "federation_id": 176
        }
    }
}
```

Returns a venue for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/venues/:id`

### URL Parameters

| Parameter | Description                                           |
| --------- | ----------------------------------------------------- |
| ID        | The internal Eventing API ID of the venue to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Venue

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"venue": {"name": "New Venue", "federation_id": "176", "source_id": "007"}}'
     'https://eventing.api.equiratings.com/v1/venues'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "venue",
        "links": {
            "self": "/v1/venues/7"
        },
        "id": "7",
        "attributes": {
            "source_id": "007",
            "name": "New Venue",
            "id": 7,
            "federation_id": 176
        }
    }
}
```

Create a venue for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/venues/`

### Attributes

| Parameter     | Description                                                                        |
| ------------- | ---------------------------------------------------------------------------------- |
| name          | **String (required)**<br>The name of the Venue                                     |
| federation_id | **String (required)**<br>The internal EquiRatings API ID of the Federation where the venue is located       |
| source_id     | **String (required)**<br>The ID that the Provider uses locally on their own system |

### Query Parameters

This endpoint does not support query parameters.

## Update a Venue

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"venue": {"name": "Updated Venue"}}'
     'https://eventing.api.equiratings.com/v1/venues/7'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "venue",
        "links": {
            "self": "/v1/venues/7"
        },
        "id": "7",
        "attributes": {
            "source_id": "007",
            "name": "Updated Venue",
            "id": 7,
            "federation_id": 176
        }
    }
}
```

Update a venue for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/venues/:id`

### Attributes

| Parameter     | Description                                                             |
| ------------- | ----------------------------------------------------------------------- |
| name          | **String**<br>The name of the venue                                     |
| federation_id | **Integer**<br>The internal EquiRatings API ID of the Federation where the venue is located      |
| source_id     | **String**<br>The ID that the Provider uses locally on their own system |

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The internal EquiRatings API ID of the venue to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Venue

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/venues/7'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a venue with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/venues/:id`

### URL Parameters

| Parameter | Description                                              |
| --------- | -------------------------------------------------------- |
| ID        | The internal EquiRatings API ID of the venue to delete   |

### Query Parameters

This endpoint does not support query parameters.

# Shows

## Get all Shows

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/shows'
```

> The above command returns JSON structured like this:

```json
{
    "links": {
        "self": "/v1/shows?page[page]=1&page[page_size]=50"
    },
    "jsonapi": {
        "version": "1.0"
    },
    "data": [
        {
            "type": "show",
            "links": {
                "self": "/v1/shows/4975"
            },
            "id": "4975",
            "attributes": {
                "venue_id": 1,
                "start_date": "2018-03-12",
                "source_id": "show_001",
                "name": "First Show",
                "id": 4975,
                "end_date": "2018-03-15"
            }
        },
        {
            "type": "show",
            "links": {
                "self": "/v1/shows/4976"
            },
            "id": "4976",
            "attributes": {
                "venue_id": 1,
                "start_date": "2018-03-19",
                "source_id": "show_002",
                "name": "Second Show",
                "id": 4976,
                "end_date": "2018-03-22"
            }
        }
    ]
}
```

Returns all show for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/shows`

### Query Parameters

This endpoint supports query parameters for paging:

| Parameter         | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| page[page]        | **Integer**<br>The number of the page to be returned.                                                   |
| page[page_size]   | **Integer**<br>The number of records per page. <br>This is a read-only parameter and is locked at 50.   |

Predefined paging URLs are also returned within the json payload.

## Get a Specific Show

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/shows/4975'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "show",
        "links": {
            "self": "/v1/shows/4975"
        },
        "id": "4975",
        "attributes": {
            "venue_id": 1,
            "start_date": "2018-03-12",
            "source_id": "show_001",
            "name": "First Show",
            "id": 4975,
            "end_date": "2018-03-15"
        }
    }
}
```

Returns a show for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/shows/:id`

### URL Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| ID        | The internal EquiRatings API ID of the show to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Show

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"show": {"venue_id": 1, "start_date": "2018-03-26", "source_id": "show_003", "name": "New Show", "end_date": "2018-03-29"}}'
     'https://eventing.api.equiratings.com/v1/shows'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "show",
        "links": {
            "self": "/v1/shows/4977"
        },
        "id": "4977",
        "attributes": {
            "venue_id": 1,
            "start_date": "2018-03-26",
            "source_id": "show_003",
            "name": "New Show",
            "id": 4977,
            "end_date": "2018-03-29"
        }
    }
}
```

Create a show for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/shows/`

### Attributes

| Parameter  | Description                                                                            |
| ---------- | -------------------------------------------------------------------------------------- |
| name       | **String (required)**<br>The name of the show                                          |
| start_date | **Date (required)**<br>The start_date of the show (YYYY-MM-DD)                         |
| end_date   | **Date (required)**<br>The end_date of the show (YYYY-MM-DD)                           |
| venue_id   | **Integer (required)**<br>The internal EquiRatings API ID for the venue of the show    |
| source_id  | **String (required)**<br>The ID that the Provider uses locally on their own system     |

### Query Parameters

This endpoint does not support query parameters.

## Update a Show

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"show": {"name": "Updated Show"}}'
     'https://eventing.api.equiratings.com/v1/shows/4977'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "show",
        "links": {
            "self": "/v1/shows/4977"
        },
        "id": "4977",
        "attributes": {
            "venue_id": 1,
            "start_date": "2018-03-26",
            "source_id": "show_003",
            "name": "Updated Show",
            "id": 4977,
            "end_date": "2018-03-29"
        }
    }
}
```

Update a show for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/shows/:id`

### Attributes

| Parameter  | Description                                                                 |
| ---------- | --------------------------------------------------------------------------- |
| name       | **String**<br>The name of the show                                          |
| start_date | **Date**<br>The start_date of the show (YYYY-MM-DD)                         |
| end_date   | **Date**<br>The end_date of the show (YYYY-MM-DD)                           |
| venue_id   | **Integer**<br>The internal EquiRatings API ID for the venue of the show    |
| source_id  | **String**<br>The ID that the Provider uses locally on their own system     |

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The internal EquiRatings API ID of the show to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Show

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/shows/4977'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a show with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/shows/:id`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The internal EquiRatings API ID of the show to retrieve |

### Query Parameters

This endpoint does not support query parameters.

# Competitions

## Get all Competitions

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/competitions'
```

> The above command returns JSON structured like this:

```json
{
    "links": {
        "self": "/v1/competitions?page[page]=1&page[page_size]=50"
    },
    "jsonapi": {
        "version": "1.0"
    },
    "included": [
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335818"
            },
            "id": "335818",
            "attributes": {
                "xc_time": null,
                "xc_status": "EL",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": "FH",
                "source_id": "001",
                "sj_time": null,
                "sj_status": "NS",
                "sj_jump": null,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335818,
                "horse_id": 54739,
                "first_hi_status": "OK",
                "final_status": "EL",
                "final_score": null,
                "final_position": null,
                "final_comment": null,
                "final_code": "XC",
                "dr_status": "OK",
                "dr_score": "33.2",
                "dr_percentage": "66.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10650,
                "athlete_id": 27996
            }
        },
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335819"
            },
            "id": "335819",
            "attributes": {
                "xc_time": "0",
                "xc_status": "OK",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": null,
                "source_id": "002",
                "sj_time": 0,
                "sj_status": "OK",
                "sj_jump": 0,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335819,
                "horse_id": 54738,
                "first_hi_status": "OK",
                "final_status": "OK",
                "final_score": "30.2",
                "final_position": 1,
                "final_comment": null,
                "final_code": null,
                "dr_status": "OK",
                "dr_score": "30.2",
                "dr_percentage": "69.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10650,
                "athlete_id": 27995
            }
        }
    ],
    "data": [
        {
            "type": "competition",
            "relationships": {
                "results": {
                    "data": [
                        {
                            "type": "result",
                            "id": "335819"
                        },
                        {
                            "type": "result",
                            "id": "335818"
                        }
                    ]
                }
            },
            "links": {
                "self": "/v1/competitions/10650"
            },
            "id": "10650",
            "attributes": {
                "source_id": "001",
                "sj_before_xc": false,
                "show_id": 4975,
                "second_hi_order": "Before_SJ",
                "name": "Competition 1",
                "id": 10650,
                "first_hi_order": "Before_DR",
                "display_name": "First Competition",
                "date": "2018-03-12",
                "class_category_id": 148,
                "championship": false
            }
        }
    ]
}
```

Returns all competition for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/competitions`

### Query Parameters

This endpoint supports query parameters for paging:

| Parameter         | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| page[page]        | **Integer**<br>The number of the page to be returned.                                                   |
| page[page_size]   | **Integer**<br>The number of records per page. <br>This is a read-only parameter and is locked at 50.   |

Predefined paging URLs are also returned within the json payload.

## Get a Specific Competition

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/competitions/10650'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "included": [
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335818"
            },
            "id": "335818",
            "attributes": {
                "xc_time": null,
                "xc_status": "EL",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": "FH",
                "source_id": "001",
                "sj_time": null,
                "sj_status": "NS",
                "sj_jump": null,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335818,
                "horse_id": 54739,
                "first_hi_status": "OK",
                "final_status": "EL",
                "final_score": null,
                "final_position": null,
                "final_comment": null,
                "final_code": "XC",
                "dr_status": "OK",
                "dr_score": "33.2",
                "dr_percentage": "66.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10650,
                "athlete_id": 27996
            }
        },
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335819"
            },
            "id": "335819",
            "attributes": {
                "xc_time": "0",
                "xc_status": "OK",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": null,
                "source_id": "002",
                "sj_time": 0,
                "sj_status": "OK",
                "sj_jump": 0,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335819,
                "horse_id": 54738,
                "first_hi_status": "OK",
                "final_status": "OK",
                "final_score": "30.2",
                "final_position": 1,
                "final_comment": null,
                "final_code": null,
                "dr_status": "OK",
                "dr_score": "30.2",
                "dr_percentage": "69.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10650,
                "athlete_id": 27995
            }
        }
    ],
    "data": {
        "type": "competition",
        "relationships": {
            "results": {
                "data": [
                    {
                        "type": "result",
                        "id": "335819"
                    },
                    {
                        "type": "result",
                        "id": "335818"
                    }
                ]
            }
        },
        "links": {
            "self": "/v1/competitions/10650"
        },
        "id": "10650",
        "attributes": {
            "source_id": "001",
            "sj_before_xc": false,
            "show_id": 4975,
            "second_hi_order": "Before_SJ",
            "name": "Competition 1",
            "id": 10650,
            "first_hi_order": "Before_DR",
            "display_name": "First Competition",
            "date": "2018-03-12",
            "class_category_id": 148,
            "championship": false
        }
    }
}
```

Returns a competition for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/competitions/:id`

### URL Parameters

| Parameter | Description                                                    |
| --------- | -------------------------------------------------------------- |
| ID        | The internal EquiRatings API ID of the competition to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Competition

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{
         "competition": {
             "source_id": "002",
             "sj_before_xc": false,
             "show_id": 4975,
             "second_hi_order": "Before_SJ",
             "name": "Competition 2",
             "first_hi_order": "Before_DR",
             "display_name": "Second Competition",
             "date": "2018-03-13",
             "class_category_id": 147,
             "championship": false,
             "results": [
                 {
                     "xc_time": null,
                     "xc_status": "EL",
                     "xc_jump": 0,
                     "xc_comment": null,
                     "xc_code": "FH",
                     "source_id": "003",
                     "sj_time": null,
                     "sj_status": "NS",
                     "sj_jump": null,
                     "sj_code": null,
                     "second_hi_status": null,
                     "horse_id": 54739,
                     "first_hi_status": "OK",
                     "final_status": "EL",
                     "final_score": null,
                     "final_position": null,
                     "final_comment": null,
                     "final_code": "XC",
                     "dr_status": "OK",
                     "dr_score": 33.2,
                     "dr_percentage": 66.8,
                     "dr_comment": null,
                     "dr_code": "",
                     "disqualification_code": null,
                     "athlete_id": 27996
                },
                {
                     "xc_time": 0,
                     "xc_status": "OK",
                     "xc_jump": 0,
                     "xc_comment": null,
                     "xc_code": "",
                     "source_id": "004",
                     "sj_time": 0,
                     "sj_status": "OK",
                     "sj_jump": 0,
                     "sj_code": "",
                     "second_hi_status": null,
                     "horse_id": 54738,
                     "first_hi_status": "OK",
                     "final_status": "OK",
                     "final_score": 30.2,
                     "final_position": 1,
                     "final_comment": "",
                     "final_code": "",
                     "dr_status": "OK",
                     "dr_score": 30.2,
                     "dr_percentage": 69.8,
                     "dr_comment": "",
                     "dr_code": "",
                     "disqualification_code": "",
                     "athlete_id": 27995
                }
             ]
         }
     }'
     'https://eventing.api.equiratings.com/v1/competitions'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "included": [
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335821"
            },
            "id": "335821",
            "attributes": {
                "xc_time": null,
                "xc_status": "EL",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": "FH",
                "source_id": "003",
                "sj_time": null,
                "sj_status": "NS",
                "sj_jump": null,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335821,
                "horse_id": 54739,
                "first_hi_status": "OK",
                "final_status": "EL",
                "final_score": null,
                "final_position": null,
                "final_comment": null,
                "final_code": "XC",
                "dr_status": "OK",
                "dr_score": "33.2",
                "dr_percentage": "66.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10652,
                "athlete_id": 27996
            }
        },
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335822"
            },
            "id": "335822",
            "attributes": {
                "xc_time": "0",
                "xc_status": "OK",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": null,
                "source_id": "004",
                "sj_time": 0,
                "sj_status": "OK",
                "sj_jump": 0,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335822,
                "horse_id": 54738,
                "first_hi_status": "OK",
                "final_status": "OK",
                "final_score": "30.2",
                "final_position": 1,
                "final_comment": null,
                "final_code": null,
                "dr_status": "OK",
                "dr_score": "30.2",
                "dr_percentage": "69.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10652,
                "athlete_id": 27995
            }
        }
    ],
    "data": {
        "type": "competition",
        "relationships": {
            "results": {
                "data": [
                    {
                        "type": "result",
                        "id": "335821"
                    },
                    {
                        "type": "result",
                        "id": "335822"
                    }
                ]
            }
        },
        "links": {
            "self": "/v1/competitions/10652"
        },
        "id": "10652",
        "attributes": {
            "source_id": "002",
            "sj_before_xc": false,
            "show_id": 4975,
            "second_hi_order": "Before_SJ",
            "name": "Competition 2",
            "id": 10652,
            "first_hi_order": "Before_DR",
            "display_name": "Second Competition",
            "date": "2018-03-13",
            "class_category_id": 147,
            "championship": false
        }
    }
}
```

Create a competition for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/competitions/`

### Attributes

| Parameter         | Description                                                                                                       |
| ----------------- | ----------------------------------------------------------------------------------------------------------------- |
| name              | **String (required)**<br>The name of the competition                                                       		|
| date              | **Date (required)**<br>The date that the competition started                                             			|
| sj_before_xc      | **Boolean (required)**<br>If SJ is before XC this will be true, otherwise false                             		|
| first_hi_order    | **String**<br>If a 1st Horse Inspection takes place and if so before which phase the HI happens 					|
| second_hi_order   | **String**<br>If a 2nd Horse Inspection takes place and if so before which phase the HI happens 					|
| display_name      | **String**<br>The display name of the competition if different to the competition name          					|
| championship      | **Boolean**<br>Is the competition a championship competition                                    					|
| results           | **Results (required)**<br>These are the results for the competition                                          		|
| class_category_id | **Integer (required)**<br>This is the internal EquiRatings API ID for the class category of this competition 		|
| show_id           | **Integer (required)**<br>This is the internal EquiRatings API ID of the show that this competition is part of.   |
| source_id         | **String (required)**<br>The ID that the Provider uses locally on their own system                         					|

### Query Parameters

This endpoint does not support query parameters.

## Update a Competition

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"competition": {"display_name": "Updated Second Competition"}}'
     'https://eventing.api.equiratings.com/v1/competitions/10652'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "included": [
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335821"
            },
            "id": "335821",
            "attributes": {
                "xc_time": null,
                "xc_status": "EL",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": "FH",
                "source_id": "003",
                "sj_time": null,
                "sj_status": "NS",
                "sj_jump": null,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335821,
                "horse_id": 54739,
                "first_hi_status": "OK",
                "final_status": "EL",
                "final_score": null,
                "final_position": null,
                "final_comment": null,
                "final_code": "XC",
                "dr_status": "OK",
                "dr_score": "33.2",
                "dr_percentage": "66.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10652,
                "athlete_id": 27996
            }
        },
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335822"
            },
            "id": "335822",
            "attributes": {
                "xc_time": "0",
                "xc_status": "OK",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": null,
                "source_id": "004",
                "sj_time": 0,
                "sj_status": "OK",
                "sj_jump": 0,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335822,
                "horse_id": 54738,
                "first_hi_status": "OK",
                "final_status": "OK",
                "final_score": "30.2",
                "final_position": 1,
                "final_comment": null,
                "final_code": null,
                "dr_status": "OK",
                "dr_score": "30.2",
                "dr_percentage": "69.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10652,
                "athlete_id": 27995
            }
        }
    ],
    "data": {
        "type": "competition",
        "relationships": {
            "results": {
                "data": [
                    {
                        "type": "result",
                        "id": "335822"
                    },
                    {
                        "type": "result",
                        "id": "335821"
                    }
                ]
            }
        },
        "links": {
            "self": "/v1/competitions/10652"
        },
        "id": "10652",
        "attributes": {
            "source_id": "002",
            "sj_before_xc": false,
            "show_id": 4975,
            "second_hi_order": "Before_SJ",
            "name": "Competition 2",
            "id": 10652,
            "first_hi_order": "Before_DR",
            "display_name": "Updated Second Competition",
            "date": "2018-03-13",
            "class_category_id": 147,
            "championship": false
        }
    }
}
```

Update a competition for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/competitions/:id`

### Attributes

| Parameter         | Description                                                                                           |
| ----------------- | ----------------------------------------------------------------------------------------------------- |
| name              | **String**<br>The name of the competition                                                       		|
| date              | **Date**<br>The date that the competition started                                             		|
| sj_before_xc      | **Boolean**<br>If SJ is before XC this will be true, otherwise false                             		|
| first_hi_order    | **String**<br>If a 1st Horse Inspection takes place and if so before which phase the HI happens 		|
| second_hi_order   | **String**<br>If a 2nd Horse Inspection takes place and if so before which phase the HI happens 		|
| display_name      | **String**<br>The display name of the competition if different to the competition name          		|
| championship      | **Boolean**<br>Is the competition a championship competition                                    		|
| results           | **Results**<br>These are the results for the compeition                                          		|
| class_category_id | **Integer**<br>This is the internal EquiRatings API ID for the class category of this competition 	|
| show_id           | **Integer**<br>This is the internal EquiRatings API ID of the show that this competition is part of.  |
| source_id         | **String**<br>The ID that the Provider uses locally on their own system                         	    |

### URL Parameters

| Parameter | Description                                                    |
| --------- | -------------------------------------------------------------- |
| ID        | the internal EquiRatings API ID of the competition to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Competition

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/competitions/10652'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a competition with the supplied id. Also deletes all results from that competition and there respective ERQIs.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/competitions/:id`

### URL Parameters

| Parameter | Description                           |
| --------- | ------------------------------------- |
| ID        | The internal EquiRatings API ID of the competition to retrieve |

### Query Parameters

This endpoint does not support query parameters.

# Results

##Result fields

Here you will find support for results:

* List of fields in results
* Descriptions of each field
* Allowed values for fields

### Key Term's Explained

* Phase Status: Shows if a combination is Eliminated or Retires in this phase, does not start the phase or completes the phase
* Phase Code: A code to represent the reason for a given status
* Phase comment: Used to give further context for a given status, and code combination

### Result fields

| Field | Definition |
|-----| ------- |
|dr_status	| Dressage Phase Status (Allowed Phase Statuses) |
|dr_code |	Dressage Phase Code (Allowed Phase Codes) |
|dr_score	| Dressage score in penalty points (1 decimal point) |
|dr_percentage |	The percentage of good marks |
|dr_comment	| Dressage Phase Comment |
|xc_status	| Cross Country Phase Status (Allowed Phase Statuses) |
|xc_code	| Cross Country Phase Code (Allowed Phase Codes) |
|xc_jump	| Cross Country Obstacle penalties (integer) |
|xc_time	| Cross country time penalties (only multiples of 0.4) |
|xc_comment |	Cross Country Phase Comment |
|sj_status |	Show Jumping Phase Status (Allowed Phase Statuses) |
|sj_code |	Show Jumping Phase Code (Allowed Phase Codes) |
|sj_jump |	Show Jumping obstacle penalties (integer) |
|sj_time |	Show Jumping time penalties (integer) |
|sj_comment |	Show Jumping Phase Comment |
|final_status	| The outcome of the combination in the competition (Allowed Final Statuses) |
|final_code |	When final_status is not OK, explains at which phase the final_status applies to. (e.g. XC-FR would be a final_code of XC) (Allowed Final Codes) |
|final_comment |	The final comment |
|final_score	| The final score of the combination (only when final_status is OK or DSQ) |
|final_position	| The final position of the combination (only when final_status is OK) |
|first_hi_status	| First Horse Inspection Phase Status (Allowed Phase Statuses) |
|second_hi_status	| Second Horse Inspection Phase Status (Allowed Phase Statuses) |
|disqualification_code	| Codes for dangerous riding |

### Allowed Statuses and Codes

#### Phase Statuses
* OK – Completed the phase
* EL – Eliminated in the phase
* RET – Retired in the phase
*	NS – Did not start the phase

#### Phase Codes

|Code| Description |
|---|-----|
|3E	| 3 errors of course (dressage) |
|AH	| abuse of horse |
|AR	| Accumulated Refusals (British Eventing) |
|CR	| compulsory retirement |
|DR	| dangerous riding |
|F2	| rider unseated twice (national federation specific) |
|FH	| fall of horse |
|FOF	|fall on the flat |
|FR	| fall of rider |
|MJ	| missed jump |
|OT	| other |
|R	| multiple refusals |
|TH	| trapped horse |
|nil	| when no code is required |

#### Final Statuses

* OK – Completed the competition
* EL- Eliminated in the competition
* RET – Retired in the competition
* WD – Withdrew from the competition
* DSQ – Disqualified from the competition

#### Final Codes

*	H1 – 1st Horse Inspection
*	H2 – 2nd Horse Inspection
*	DR – Dressage
* XC – Cross Country
* SJ – Show Jumping

#### Disqualification Codes

* Warning_DR – a warning given for dangerous riding
* Minor_DR – a minor dangerous riding
* Major_DR – a major dangerous riding fault

## Get all Results

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/results'
```

> The above command returns JSON structured like this:

```json
{
    "links": {
        "self": "/v1/results?page[page]=1&page[page_size]=50"
    },
    "jsonapi": {
        "version": "1.0"
    },
    "data": [
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335818"
            },
            "id": "335818",
            "attributes": {
                "xc_time": null,
                "xc_status": "EL",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": "FH",
                "source_id": "001",
                "sj_time": null,
                "sj_status": "NS",
                "sj_jump": null,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335818,
                "horse_id": 54739,
                "first_hi_status": "OK",
                "final_status": "EL",
                "final_score": null,
                "final_position": null,
                "final_comment": null,
                "final_code": "XC",
                "dr_status": "OK",
                "dr_score": "33.2",
                "dr_percentage": "66.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10650,
                "athlete_id": 27996
            }
        },
        {
            "type": "result",
            "links": {
                "self": "/v1/results/335819"
            },
            "id": "335819",
            "attributes": {
                "xc_time": "0",
                "xc_status": "OK",
                "xc_jump": 0,
                "xc_comment": null,
                "xc_code": null,
                "source_id": "002",
                "sj_time": 0,
                "sj_status": "OK",
                "sj_jump": 0,
                "sj_code": null,
                "second_hi_status": null,
                "id": 335819,
                "horse_id": 54738,
                "first_hi_status": "OK",
                "final_status": "OK",
                "final_score": "30.2",
                "final_position": 1,
                "final_comment": null,
                "final_code": null,
                "dr_status": "OK",
                "dr_score": "30.2",
                "dr_percentage": "69.8",
                "dr_comment": null,
                "dr_code": null,
                "disqualification_code": null,
                "competition_id": 10650,
                "athlete_id": 27995
            }
        }
    ]
}
```

Returns all result for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/results`

### Query Parameters

This endpoint supports query parameters for paging:

| Parameter         | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| page[page]        | **Integer**<br>The number of the page to be returned.                                                   |
| page[page_size]   | **Integer**<br>The number of records per page. <br>This is a read-only parameter and is locked at 50.   |

Predefined paging URLs are also returned within the json payload.

## Get a Specific Result

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/results/335818'
```

> The above command returns JSON structured like this:

```json
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "result",
        "links": {
            "self": "/v1/results/335818"
        },
        "id": "335818",
        "attributes": {
            "xc_time": null,
            "xc_status": "EL",
            "xc_jump": 0,
            "xc_comment": null,
            "xc_code": "FH",
            "source_id": "001",
            "sj_time": null,
            "sj_status": "NS",
            "sj_jump": null,
            "sj_code": null,
            "second_hi_status": null,
            "id": 335818,
            "horse_id": 54739,
            "first_hi_status": "OK",
            "final_status": "EL",
            "final_score": null,
            "final_position": null,
            "final_comment": null,
            "final_code": "XC",
            "dr_status": "OK",
            "dr_score": "33.2",
            "dr_percentage": "66.8",
            "dr_comment": null,
            "dr_code": null,
            "disqualification_code": null,
            "competition_id": 10650,
            "athlete_id": 27996
        }
    }
}
```

Returns a result for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/results/:id`

### URL Parameters

| Parameter | Description                                               |
| --------- | --------------------------------------------------------- |
| ID        | The internal EquiRatings API ID of the result to retrieve |

### Query Parameters

This endpoint does not support query parameters.
