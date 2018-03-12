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
management all aspects of you're eventing records. Through the Eventing API
endpoints you can upload and get ERQI information.

Currently our API support's REST Https calls which you can consume using cURL or
directly using whatever HTTP wrapper your language of choice supports.

Currently the API is in Beta, and it is subject to change. Don't worry we will
inform our partner's about any change's long before we deploy.

# Authentication

The Eventing API uses JWT token's for authentication. Please contact EquiRatings
in order to get setup on our system. Once you have been assigned user for your
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
curl -H "Content-type: application/json"
     -d '{"email": "user@domain.com", "password": "abc123"}'
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
      "token": "eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9"
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
      "first-name": "First",
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
        "first-name": "First",
        "email": "email7@domain.com"
      }
    }
  ]
}
```

Returns all user for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/users`

### Query Parameters

This endpoint does not support query parameters.

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
      "first-name": "First",
      "email": "email13@domain.com"
    }
  }
}
```

Returns a user for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/users/:id`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the user to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a User

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"user": {"first_name": "Sam", "surname": "Watson", "email": "user@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/users/1"
    },
    "id": "1",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 1,
      "first-name": "Sam",
      "email": "user@domain.com"
    }
  }
}
```

Create a user for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/users/`

### Attributes

| Parameter  | Description                                                                    |
| ---------- | ------------------------------------------------------------------------------ |
| first_name | The first name of the user                                                     |
| surname    | The surname of the user                                                        |
| email      | The email of the user                                                          |
| password   | The password of the user                                                       |
| roles      | The user role, valid roles are as follows: ["provider_admin", "provider_user"] |

### Query Parameters

This endpoint does not support query parameters.

## Update a User

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"user": {"first_name": "Sam", "surname": "Watson", "email": "user@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/users/1"
    },
    "id": "1",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 1,
      "first-name": "Sam",
      "email": "user@domain.com"
    }
  }
}
```

Update a user for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/users/:id`

### Attributes

| Parameter  | Description                                                                    |
| ---------- | ------------------------------------------------------------------------------ |
| first_name | The first name of the user                                                     |
| surname    | The surname of the user                                                        |
| email      | The email of the user                                                          |
| password   | The password of the user                                                       |
| roles      | The user role, valid roles are as follows: ["provider_admin", "provider_user"] |

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the user to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a User

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/users/1'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a user with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/users/:id`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the user to retrieve |

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
  "jsonapi": {
    "version": "1.0"
  },
  "data": [
    {
      "type": "venue",
      "links": {
        "self": "/venues/1"
      },
      "id": "1",
      "attributes": {
        "name": "Chatsworth",
        "id": 1
      }
    }
  ]
}
```

Returns all venue for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/venues`

### Query Parameters

This endpoint does not support query parameters.

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
      "self": "/venues/1"
    },
    "id": "1",
    "attributes": {
      "name": "Chatsworth",
      "id": 1
    }
  }
}
```

Returns a venue for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/venues/:id`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the venue to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Venue

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"venue": {"name": Chatsworth}}'
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
      "self": "/venues/1"
    },
    "id": "1",
    "attributes": {
      "name": "Chatsworth",
      "id": 1
    }
  }
}
```

Create a venue for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/venues/`

### Attributes

| Parameter  | Description                                                                      |
| ---------- | -------------------------------------------------------------------------------- |
| name       | The name of the Venue                                                            |


### Query Parameters

This endpoint does not support query parameters.

## Update a Venue

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"venue": {"name": :Updated name}}'
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
    "relationships": {},
    "links": {
      "self": "/venues/1"
    },
    "id": "1",
    "attributes": {
      "name": "Updated name",
      "id": 1
    }
  }
}
```

Update a venue for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/venues/:id`

### Attributes

| Parameter  | Description                                                           |
| ---------- | --------------------------------------------------------------------- |
| name       | The name of the venue                                                 |


### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the venue to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Venue

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/venues/1'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a venue with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/venues/:id`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the venue to retrieve |

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
  "jsonapi": {
    "version": "1.0"
  },
  "data": [{
    "type": "show",
    "links": {
      "self": "/shows/1"
    },
    "id": "1",
    "attributes": {
      "venue-id": 1,
      "start-date": "2018-03-12",
      "source-id": null,
      "provider-id": 1,
      "name": "Chatsworth International",
      "id": 1,
      "end-date": "2018-03-15"
      }
    }
  ]
}
```

Returns all show for the current users's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/shows`

### Query Parameters

This endpoint does not support query parameters.

## Get a Specific Show

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/shows/1'
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
      "self": "/shows/1"
    },
    "id": "1",
    "attributes": {
      "venue-id": 1,
      "start-date": "2018-03-12",
      "source-id": null,
      "provider-id": 1,
      "name": "Chatsworth International",
      "id": 1,
      "end-date": "2018-03-15"
    }
  }
}
```

Returns a show for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/shows/:id`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the show to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Show

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"show": { "start_date": "2018-03-12", "name": "Chatsworth International", "end_date": "2018-03-15", "venue_id": 1}}'
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
      "self": "/shows/1"
    },
    "id": "1",
    "attributes": {
      "venue-id": 1,
      "start-date": "2018-03-12",
      "source-id": null,
      "provider-id": 1,
      "name": "Chatsworth International",
      "id": 1,
      "end-date": "2018-03-15"
    }
  }
}
```

Create a show for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/shows/`

### Attributes

| Parameter  | Description                                                                    |
| ---------- | ------------------------------------------------------------------------------ |
| start_date | The start_date of the show                                                     |
| name       | The name of the show                                                           |
| end_date   | The end_date of the show                                                       |
| venue_id | The venue id for the venue of the show |

### Query Parameters

This endpoint does not support query parameters.

## Update a Show

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"show": {"name": "Updated name"}}'
     'https://eventing.api.equiratings.com/v1/shows/1'
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
      "self": "/shows/1"
    },
    "id": "1",
    "attributes": {
      "venue-id": 1,
      "start-date": "2018-03-12",
      "source-id": null,
      "provider-id": 1,
      "name": "Chatsworth International",
      "id": 1,
      "end-date": "2018-03-15"
    }
  }
}
```

Update a show for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/shows/:id`

### Attributes

| Parameter  | Description                                                                    |
| ---------- | ------------------------------------------------------------------------------ |
| start_date | The start_date of the show                                                     |
| name       | The name of the show                                                           |
| end_date   | The end_date of the show                                                       |
| venue_id | The venue id for the venue of the show |


### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the show to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Show

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/shows/1'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a show with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/shows/:id`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the show to retrieve |

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
  "jsonapi": {
    "version": "1.0"
  },
  "data": [
    {
      "type": "competition",
      "links": {
        "self": "/competitions/1"
      },
      "id": "1",
      "attributes": {
        "sj-before-xc": true,
        "second-hi-order": null,
        "name": "N",
        "id": 1,
        "first-hi-order": null,
        "display-name": null,
        "date": "2018-03-12",
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

This endpoint does not support query parameters.

## Get a Specific Competition

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/competitions/1'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "competition",
    "links": {
      "self": "/competitions/1"
    },
    "id": "1",
    "attributes": {
      "sj-before-xc": true,
      "second-hi-order": null,
      "name": "N",
      "id": 1,
      "first-hi-order": null,
      "display-name": null,
      "date": "2018-03-12",
      "championship": false
    }
  }
}
```

Returns a competition for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/competitions/:id`

### URL Parameters

| Parameter | Description                           |
| --------- | ------------------------------------- |
| ID        | The ID of the competition to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Competition

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{
       "competition": {
         "sj_before_xc": true,
         "results": [
           {
             "xc_status": "EL",
             "xc_jump": 0,
             "xc_code": "FH",
             "sj_status": "NS",
             "provider_id": 2812,
             "horse_id": 1108,
             "final_status": "EL",
             "dr_status": "OK",
             "athlete_id": 1120
           }
         ],
         "name": "N",
         "date": "2018-03-12",
         "class_category_id": 1465,
         "championship": false,
         "display_name": null
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
  "data": {
    "type": "competition",
    "links": {
      "self": "/competitions/1"
    },
    "id": "1",
    "attributes": {
      "sj-before-xc": true,
      "second-hi-order": null,
      "name": "N",
      "id": 1,
      "first-hi-order": null,
      "display-name": null,
      "date": "2018-03-12",
      "championship": false
    }
  }
}
```

Create a competition for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/competitions/`

### Attributes

| Parameter  | Description                                                                                  |
| ---------- | -------------------------------------------------------------------------------------------- |
| name      | The name of the competition                                                           |
| date | The date that the competition started |
| sj-before-xc       | If SJ is before XC this will be true, otherwise false                                |
| first-hi-order      | If a 1st Horse Inspection takes place and if so before which phase the HI happens|
| second-hi-order    | If a 2nd Horse Inspection takes place and if so before which phase the HI happens                     |
| display-name | The display name of the competition if different to the competition name |
| championship | Is the competition a championship competition |
| results | These are the results for the compeition |
| class_category_id | This is the class level for the competition |

### Query Parameters

This endpoint does not support query parameters.

## Update a Competition

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"competition": {"name": "Updated name"}}'
     'https://eventing.api.equiratings.com/v1/competitions/1'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "competition",
    "links": {
      "self": "/competitions/1"
    },
    "id": "1",
    "attributes": {
      "sj-before-xc": true,
      "second-hi-order": null,
      "name": "Updated name",
      "id": 1,
      "first-hi-order": null,
      "display-name": null,
      "date": "2018-03-12",
      "championship": false
    }
  }
}
```

Update a competition for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/competitions/:id`

### Attributes

| Parameter  | Description                                                                                |
| ---------- | ------------------------------------------------------------------------------------------ |
| name      | The name of the competition                                                   |
| date | The date that the competition started |
| sj-before-xc       | If SJ is before XC this will be true, otherwise false                                |
| first-hi-order      | If a 1st Horse Inspection takes place and if so before which phase the HI happens|
| second-hi-order    | If a 2nd Horse Inspection takes place and if so before which phase the HI happens                     |
| display-name | The display name of the competition if different to the competition name |
| championship | Is the competition a championship competition |
| results | These are the results for the compeition |
| class_category_id | This is the class level for the competition |

### URL Parameters

| Parameter | Description                           |
| --------- | ------------------------------------- |
| ID        | The ID of the competition to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Competition

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/competitions/1'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a competition with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/competitions/:id`

### URL Parameters

| Parameter | Description                           |
| --------- | ------------------------------------- |
| ID        | The ID of the competition to retrieve |

### Query Parameters

This endpoint does not support query parameters.

# ClassCategories

## Get all ClassCategories

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/class_categories'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": [
    {
      "type": "CCI",
      "links": {
        "self": "/class_categories/1"
      },
      "id": "1",
      "attributes": {
        "type": "CCI",
        "provider-id": 2822,
        "name": "CCI3*",
        "level": "3",
        "id": 1,
        "er-level": 12
      }
    }
  ]
}
```

Returns all class_category for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/class_categories`

### Query Parameters

This endpoint does not support query parameters.

## Get a Specific ClassCategory

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/class_categories/1'
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
      "self": "/class_categories/1"
    },
    "id": "1",
    "attributes": {
      "type": "CCI",
      "provider-id": 2822,
      "name": "CCI3*",
      "level": "3",
      "id": 1,
      "er-level": 12
    }
  }
}
```

Returns a class_category for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/class_categories/:id`

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| ID        | The ID of the class_category to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a ClassCategory

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"class_category": {
       "type": "CCI", "provider_id": 2818, "name": "CCI3*", "level": "3", "er_level": 12}}'
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
      "self": "/class_categories/1"
    },
    "id": "1",
    "attributes": {
      "type": "CCI",
      "provider-id": 2818,
      "name": "CCI3*",
      "level": "3",
      "id": 1,
      "er-level": 12
    }
  }
}
```

Create a class_category for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/class_categories/`

### Attributes

| Parameter  | Description                                                                                        |
| ---------- | -------------------------------------------------------------------------------------------------- |
| type | The type of the class |
| name | The full name of the class |
| level | The level of the class |
| er-level | The equiraitings level of the class |
| provider_id | The id of the provider ?????????? |

### Query Parameters

This endpoint does not support query parameters.

## Update a ClassCategory

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"class_category": {"name": "Updated name"}}'
     'https://eventing.api.equiratings.com/v1/class_categories/1'
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
      "self": "/class_categories/1"
    },
    "id": "1",
    "attributes": {
      "type": "CCI",
      "provider-id": 2821,
      "name": "Updated name",
      "level": "3",
      "id": 1,
      "er-level": 12
    }
  }
}
```

Update a class_category for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/class_categories/:id`

### Attributes

| Parameter  | Description                                                                                        |
| ---------- | -------------------------------------------------------------------------------------------------- |
| type | The type of the class |
| name | The full name of the class |
| level | The level of the class |
| er-level | The equiraitings level of the class |
| provider_id | The id of the provider ?????????? |

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| ID        | The ID of the class_category to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a ClassCategory

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/class_categories/1'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a class_category with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/class_categories/:id`

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| ID        | The ID of the class_category to retrieve |

### Query Parameters

This endpoint does not support query parameters.

# Results

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
  "jsonapi": {
    "version": "1.0"
  },
  "data": [
    {
      "type": "result",
      "links": {
        "self": "/results/1"
      },
      "id": "1",
      "attributes": {
        "xc-time": null,
        "xc-status": "EL",
        "xc-jump": "0",
        "xc-comment": null,
        "xc-code": "FH",
        "sj-time": null,
        "sj-status": "NS",
        "sj-jump": null,
        "sj-code": null,
        "second-hi-status": null,
        "id": 1,
        "horse-id": 1102,
        "first-hi-status": null,
        "final-status": "EL",
        "final-score": null,
        "final-position": null,
        "final-comment": null,
        "final-code": null,
        "dr-status": "OK",
        "dr-score": null,
        "dr-percentage": null,
        "dr-comment": null,
        "dr-code": null,
        "disqualification-code": null,
        "competition-id": 2183,
        "athlete-id": 1117
      }
    }
  ]
}
```

Returns all result for the current users's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/results`

### Query Parameters

This endpoint does not support query parameters.

## Get a Specific Result

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/results/1'
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
      "self": "/results/1"
    },
    "id": "1",
    "attributes": {
      "xc-time": null,
      "xc-status": "EL",
      "xc-jump": "0",
      "xc-comment": null,
      "xc-code": "FH",
      "sj-time": null,
      "sj-status": "NS",
      "sj-jump": null,
      "sj-code": null,
      "second-hi-status": null,
      "id": 1,
      "horse-id": 1102,
      "first-hi-status": null,
      "final-status": "EL",
      "final-score": null,
      "final-position": null,
      "final-comment": null,
      "final-code": null,
      "dr-status": "OK",
      "dr-score": null,
      "dr-percentage": null,
      "dr-comment": null,
      "dr-code": null,
      "disqualification-code": null,
      "competition-id": 2183,
      "athlete-id": 1117
    }
  }
}
```

Returns a result for the supplied ID parameter.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/results/:id`

### URL Parameters

| Parameter | Description                      |
| --------- | -------------------------------- |
| ID        | The ID of the result to retrieve |

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
  "jsonapi": {
    "version": "1.0"
  },
  "data": [
    {
      "type": "athlete",
      "links": {
        "self": "/athletes/1"
      },
      "id": "1",
      "attributes": {
        "surname": "Watson",
        "nationality": "Irish",
        "id": 1,
        "gender": "Male",
        "first-name": "Sam",
        "fei-id": 10007367,
        "federation-id": 3041,
        "dob": "1982-01-14",
        "display-name": null
      }
    }
  ]
}
```

Returns all athlete for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/athletes`

### Query Parameters

This endpoint does not support query parameters.

## Get a Specific Athlete

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/athletes/1'
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
      "self": "/athletes/1"
    },
    "id": "1",
    "attributes": {
      "surname": "Watson",
      "nationality": "Irish",
      "id": 1,
      "gender": "Male",
      "first-name": "Sam",
      "fei-id": 10007367,
      "federation-id": 3041,
      "dob": "1982-01-14",
      "display-name": null
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
| ID        | The ID of the athlete to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Athlete

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"athlete": {"surname": "Watson", "nationality": "Irish", "gender": "Male", "first_name": "Sam", "fei_id": 10007367, "dob": "1982-01-14"}}'
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
      "self": "/athletes/1"
    },
    "id": "1",
    "attributes": {
      "surname": "Watson",
      "nationality": "Irish",
      "id": 1,
      "gender": "Male",
      "first-name": "Sam",
      "fei-id": 10007367,
      "federation-id": null,
      "dob": "1982-01-14",
      "display-name": null
    }
  }
}
```

Create a athlete for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/athletes/`

### Attributes

| Parameter  | Description                                                                          |
| ---------- | ------------------------------------------------------------------------------------ |
| first_name | The first name of the athlete                                                        |
| surname    | The surname of the athlete                                                           |
| gender | The gender of the athlete |
| nationality | The nationality of the athlete |
| dob | The date of birth of the athlete |
| display-name  | The name that is displayed for the athlete if it is different to their name  |
| fei-id | The fei-id of the athlete |
|federation-id| The id of the federation the athlete belongs to |

### Query Parameters

This endpoint does not support query parameters.

## Update a Athlete

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"athlete": {"first_name": "Updated name"}'
     'https://eventing.api.equiratings.com/v1/athletes/1'
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
      "self": "/athletes/1125"
    },
    "id": "1",
    "attributes": {
      "surname": "Watson",
      "nationality": "Irish",
      "id": 1,
      "gender": "Male",
      "first-name": "Updated name",
      "fei-id": 10007367,
      "federation-id": 3040,
      "dob": "1982-01-14",
      "display-name": null
    }
  }
}
```

Update a athlete for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/athletes/:id`

### Attributes

| Parameter  | Description                                                                          |
| ---------- | ------------------------------------------------------------------------------------ |
| first_name | The first name of the athlete                                                        |
| surname    | The surname of the athlete                                                           |
| gender | The gender of the athlete |
| nationality | The nationality of the athlete |
| dob | The date of birth of the athlete |
| display-name  | The name that is displayed for the athlete if it is different to their name  |
| fei-id | The fei-id of the athlete |
|federation-id| The id of the federation the athlete belongs to |


### URL Parameters

| Parameter | Description                       |
| --------- | --------------------------------- |
| ID        | The ID of the athlete to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Athlete

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/athletes/1'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a athlete with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/athletes/:id`

### URL Parameters

| Parameter | Description                       |
| --------- | --------------------------------- |
| ID        | The ID of the athlete to retrieve |

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
  "jsonapi": {
    "version": "1.0"
  },
  "data": [
    {
      "type": "horse",
      "links": {
        "self": "/horses/1"
      },
      "id": "1",
      "attributes": {
        "ueln": null,
        "risk-data": [],
        "name": "Horseware Bushman",
        "id": 1,
        "gender": "Gelding",
        "fei-id": "IRL03630",
        "dob": "1999-05-24",
        "display-name": null
      }
    }
  ]
}
```

Returns all horse for the current user's organization.

### HTTP Request

`GET https://eventing.api.equiratings.com/v1/horses`

### Query Parameters

This endpoint does not support query parameters.

## Get a Specific Horse

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/horses/1'
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
      "self": "/horses/1"
    },
    "id": "1",
    "attributes": {
      "ueln": null,
      "risk-data": [],
      "name": "Horseware Bushman",
      "id": 1,
      "gender": "Gelding",
      "fei-id": "IRL03630",
      "dob": "1999-05-24",
      "display-name": null
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
| ID        | The ID of the horse to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Horse

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"horse": {"provider_id": 2794, "name": "Horseware Bushman", "gender": "Gelding", "fei_id": "IRL03630", "dob": "1999-05-24"}}'
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
      "self": "/horses/1"
    },
    "id": "1",
    "attributes": {
      "ueln": null,
      "risk-data": [],
      "name": "Horseware Bushman",
      "id": 1,
      "gender": "Gelding",
      "fei-id": "IRL03630",
      "dob": "1999-05-24",
      "display-name": null
    }
  }
}
```

Create a horse for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/horses/`

### Attributes

| Parameter  | Description                                                                      |
| ---------- | -------------------------------------------------------------------------------- |
| name | The name of the horse |
| gender | The gender of the horse |
| dob | The date of birth of the horse |
| fei-id| The fei id for the horse |
| ueln | The unique equine life number of the horse |
| display-name | The display name of the horse if different from the name |

### Query Parameters

This endpoint does not support query parameters.

## Update a Horse

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"horse": {"name": "Update name"}}'
     'https://eventing.api.equiratings.com/v1/horses/1'
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
      "self": "/horses/1"
    },
    "id": "1",
    "attributes": {
      "ueln": null,
      "risk-data": [],
      "name": "Updated name",
      "id": 1,
      "gender": "Gelding",
      "fei-id": "IRL03630",
      "dob": "1999-05-24",
      "display-name": null
    }
  }
}
```

Update a horse for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/horses/:id`

### Attributes

| Parameter  | Description                                                                      |
| ---------- | -------------------------------------------------------------------------------- |
| name | The name of the horse |
| gender | The gender of the horse |
| dob | The date of birth of the horse |
| fei-id| The fei id for the horse |
| ueln | The unique equine life number of the horse |
| display-name | The display name of the horse if different from the name |

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the horse to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Horse

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/horses/1'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a horse with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/horses/:id`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the horse to retrieve |

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
  "jsonapi": {
    "version": "1.0"
  },
  "data": [
    {
      "type": "federation",
      "links": {
        "self": "/federations/1"
      },
      "id": "1",
      "attributes": {
        "name": "British Eventing",
        "id": 1,
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

This endpoint does not support query parameters.

## Get a Specific Federation

```shell
curl -XGET
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/federations/1'
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
      "self": "/federations/1"
    },
    "id": "1",
    "attributes": {
      "name": "British Eventing",
      "id": 1,
      "code": "GBR"
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
| ID        | The ID of the federation to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Create a Federation

```shell
curl -XPOST
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"federation": {"name": "British Eventing", "code": "GBR"}}'
     'https://eventing.api.equiratings.com/v1/federations/'
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
      "self": "/federations/1"
    },
    "id": "1",
    "attributes": {
      "name": "British Eventing",
      "id": 1,
      "code": "GBR"
    }
  }
}
```

Create a federation for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/federations/`

### Attributes

| Parameter  | Description                                                                                |
| ---------- | ----------------------------------------------------------------------------------------- |
| name | The name of the federation |
| code | The country code for the federation |

### Query Parameters

This endpoint does not support query parameters.

## Update a Federation

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"federation": {"name": "Updated name"}}'
     'https://eventing.api.equiratings.com/v1/federations/1'
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
      "self": "/federations/1"
    },
    "id": "1",
    "attributes": {
      "name": "Updated name",
      "id": 1,
      "code": "GBR"
    }
  }
}
```

Update a federation for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/federations/:id`

### Attributes

| Parameter  | Description                                                                                |
| ---------- | ----------------------------------------------------------------------------------------- |
| name | The name of the federation |
| code | The country code for the federation |

### URL Parameters

| Parameter | Description                          |
| --------- | ------------------------------------ |
| ID        | The ID of the federation to retrieve |

### Query Parameters

This endpoint does not support query parameters.

## Delete a Federation

```shell
curl -XDELETE
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     'https://eventing.api.equiratings.com/v1/federations/1'
```

> DELETE request will return a 204 HTTP status code, with no json payload

Deletes a federation with the supplied id.

### HTTP Request

`DELETE https://eventing.api.equiratings.com/v1/federations/:id`

### URL Parameters

| Parameter | Description                          |
| --------- | ------------------------------------ |
| ID        | The ID of the federation to retrieve |

### Query Parameters

This endpoint does not support query parameters.

<!-- This endpoint retrieves all kittens. -->

<!--  -->

<!-- ### HTTP Request -->

<!--  -->

<!-- `GET http://example.com/api/kittens` -->

<!--  -->

<!-- ### Query Parameters -->

<!--  -->

<!-- | Parameter    | Default | Description                                                                      | -->

<!-- | ------------ | ------- | -------------------------------------------------------------------------------- | -->

<!-- | include_cats | false   | If set to true, the result will also include cats.                               | -->

<!-- | available    | true    | If set to false, the result will include kittens that have already been adopted. | -->

<!--  -->

<!-- <aside class="success"> -->

<!-- Remember — a happy kitten is an authenticated kitten! -->

<!-- </aside> -->

<!-- ## Get a Specific Kitten -->

<!--  -->

<!-- ```ruby -->

<!-- require 'kittn' -->

<!--  -->

<!-- api = Kittn::APIClient.authorize!('meowmeowmeow') -->

<!-- api.kittens.get(2) -->

<!-- ``` -->

<!--  -->

<!-- ```python -->

<!-- import kittn -->

<!--  -->

<!-- api = kittn.authorize('meowmeowmeow') -->

<!-- api.kittens.get(2) -->

<!-- ``` -->

<!--  -->

<!-- ```shell -->

<!-- curl "http://example.com/api/kittens/2" -->

<!--   -H "Authorization: meowmeowmeow" -->

<!-- ``` -->

<!--  -->

<!-- ```javascript -->

<!-- const kittn = require('kittn'); -->

<!--  -->

<!-- let api = kittn.authorize('meowmeowmeow'); -->

<!-- let max = api.kittens.get(2); -->

<!-- ``` -->

<!--  -->

<!-- > The above command returns JSON structured like this: -->

<!--  -->

<!-- ```json -->

<!-- { -->

<!--   "id": 2, -->

<!--   "name": "Max", -->

<!--   "breed": "unknown", -->

<!--   "fluffiness": 5, -->

<!--   "cuteness": 10 -->

<!-- } -->

<!-- ``` -->

<!--  -->

<!-- This endpoint retrieves a specific kitten. -->

<!--  -->

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

<!--  -->

<!-- ### HTTP Request -->

<!--  -->

<!-- `GET http://example.com/kittens/<ID>` -->

<!--  -->

<!-- ### URL Parameters -->

<!--  -->

<!-- | Parameter | Description                      | -->

<!-- | --------- | -------------------------------- | -->

<!-- | ID        | The ID of the kitten to retrieve | -->

<!--  -->

<!-- ## Delete a Specific Kitten -->

<!--  -->

<!-- ```ruby -->

<!-- require 'kittn' -->

<!--  -->

<!-- api = Kittn::APIClient.authorize!('meowmeowmeow') -->

<!-- api.kittens.delete(2) -->

<!-- ``` -->

<!--  -->

<!-- ```python -->

<!-- import kittn -->

<!--  -->

<!-- api = kittn.authorize('meowmeowmeow') -->

<!-- api.kittens.delete(2) -->

<!-- ``` -->

<!--  -->

<!-- ```shell -->

<!-- curl "http://example.com/api/kittens/2" -->

<!--   -X DELETE -->

<!--   -H "Authorization: meowmeowmeow" -->

<!-- ``` -->

<!--  -->

<!-- ```javascript -->

<!-- const kittn = require('kittn'); -->

<!--  -->

<!-- let api = kittn.authorize('meowmeowmeow'); -->

<!-- let max = api.kittens.delete(2); -->

<!-- ``` -->

<!--  -->

<!-- > The above command returns JSON structured like this: -->

<!--  -->

<!-- ```json -->

<!-- { -->

<!--   "id": 2, -->

<!--   "deleted": ":(" -->

<!-- } -->

<!-- ``` -->

<!--  -->

<!-- This endpoint deletes a specific kitten. -->

<!--  -->

<!-- ### HTTP Request -->

<!--  -->

<!-- `DELETE http://example.com/kittens/<ID>` -->

<!--  -->

<!-- ### URL Parameters -->

<!--  -->

<!-- | Parameter | Description                    | -->

<!-- | --------- | ------------------------------ | -->

<!-- | ID        | The ID of the kitten to delete | -->
