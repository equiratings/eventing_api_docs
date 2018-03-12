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
      "self": "/users/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "user@domain.com"
    }
  }
}
```

Create a user for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/users/:id`

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
      "self": "/users/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
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
      "relationships": {
        "token": {
          "data": null
        }
      },
      "links": {
        "self": "/venues/90"
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

Returns all venue for the current venue's organization.

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
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/venues/96"
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
     -d '{"venue": {"first_name": "Sam", "surname": "Watson", "email": "venue@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/venues/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "venue@domain.com"
    }
  }
}
```

Create a venue for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/venues/:id`

### Attributes

| Parameter  | Description                                                                      |
| ---------- | -------------------------------------------------------------------------------- |
| first_name | The first name of the venue                                                      |
| surname    | The surname of the venue                                                         |
| email      | The email of the venue                                                           |
| password   | The password of the venue                                                        |
| roles      | The venue role, valid roles are as follows: ["provider_admin", "provider_venue"] |

### Query Parameters

This endpoint does not support query parameters.

## Update a Venue

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"venue": {"first_name": "Sam", "surname": "Watson", "email": "venue@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/venues/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "venue@domain.com"
    }
  }
}
```

Update a venue for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/venues/:id`

### Attributes

| Parameter  | Description                                                                      |
| ---------- | -------------------------------------------------------------------------------- |
| first_name | The first name of the venue                                                      |
| surname    | The surname of the venue                                                         |
| email      | The email of the venue                                                           |
| password   | The password of the venue                                                        |
| roles      | The venue role, valid roles are as follows: ["provider_admin", "provider_venue"] |

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
  "data": [
    {
      "type": "show",
      "relationships": {
        "token": {
          "data": null
        }
      },
      "links": {
        "self": "/shows/90"
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

Returns all show for the current show's organization.

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
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/shows/96"
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
     -d '{"show": {"first_name": "Sam", "surname": "Watson", "email": "show@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/shows/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "show@domain.com"
    }
  }
}
```

Create a show for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/shows/:id`

### Attributes

| Parameter  | Description                                                                    |
| ---------- | ------------------------------------------------------------------------------ |
| first_name | The first name of the show                                                     |
| surname    | The surname of the show                                                        |
| email      | The email of the show                                                          |
| password   | The password of the show                                                       |
| roles      | The show role, valid roles are as follows: ["provider_admin", "provider_show"] |

### Query Parameters

This endpoint does not support query parameters.

## Update a Show

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"show": {"first_name": "Sam", "surname": "Watson", "email": "show@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/shows/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "show@domain.com"
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
| first_name | The first name of the show                                                     |
| surname    | The surname of the show                                                        |
| email      | The email of the show                                                          |
| password   | The password of the show                                                       |
| roles      | The show role, valid roles are as follows: ["provider_admin", "provider_show"] |

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
      "relationships": {
        "token": {
          "data": null
        }
      },
      "links": {
        "self": "/competitions/90"
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

Returns all competition for the current competition's organization.

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
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/competitions/96"
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
     -d '{"competition": {"first_name": "Sam", "surname": "Watson", "email": "competition@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/competitions/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "competition@domain.com"
    }
  }
}
```

Create a competition for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/competitions/:id`

### Attributes

| Parameter  | Description                                                                                  |
| ---------- | -------------------------------------------------------------------------------------------- |
| first_name | The first name of the competition                                                            |
| surname    | The surname of the competition                                                               |
| email      | The email of the competition                                                                 |
| password   | The password of the competition                                                              |
| roles      | The competition role, valid roles are as follows: ["provider_admin", "provider_competition"] |

### Query Parameters

This endpoint does not support query parameters.

## Update a Competition

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"competition": {"first_name": "Sam", "surname": "Watson", "email": "competition@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/competitions/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "competition@domain.com"
    }
  }
}
```

Update a competition for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/competitions/:id`

### Attributes

| Parameter  | Description                                                                                  |
| ---------- | -------------------------------------------------------------------------------------------- |
| first_name | The first name of the competition                                                            |
| surname    | The surname of the competition                                                               |
| email      | The email of the competition                                                                 |
| password   | The password of the competition                                                              |
| roles      | The competition role, valid roles are as follows: ["provider_admin", "provider_competition"] |

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
      "type": "class_category",
      "relationships": {
        "token": {
          "data": null
        }
      },
      "links": {
        "self": "/class_categories/90"
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

Returns all class_category for the current class_category's organization.

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
    "type": "class_category",
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/class_categories/96"
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
     -d '{"class_category": {"first_name": "Sam", "surname": "Watson", "email": "class_category@domain.com", "password": "abc123", role:"provider_admin"}}'
     'https://eventing.api.equiratings.com/v1/class_categories'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "class_category",
    "relationships": {},
    "links": {
      "self": "/class_categories/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "class_category@domain.com"
    }
  }
}
```

Create a class_category for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/class_categories/:id`

### Attributes

| Parameter  | Description                                                                                        |
| ---------- | -------------------------------------------------------------------------------------------------- |
| first_name | The first name of the class_category                                                               |
| surname    | The surname of the class_category                                                                  |
| email      | The email of the class_category                                                                    |
| password   | The password of the class_category                                                                 |
| roles      | The class_category role, valid roles are as follows: ["provider_admin", "provider_class_category"] |

### Query Parameters

This endpoint does not support query parameters.

## Update a ClassCategory

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"class_category": {"first_name": "Sam", "surname": "Watson", "email": "class_category@domain.com", "password": "abc123", role:"provider_admin"}}'
     'https://eventing.api.equiratings.com/v1/class_categories'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "class_category",
    "relationships": {},
    "links": {
      "self": "/class_categories/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "class_category@domain.com"
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
| first_name | The first name of the class_category                                                               |
| surname    | The surname of the class_category                                                                  |
| email      | The email of the class_category                                                                    |
| password   | The password of the class_category                                                                 |
| roles      | The class_category role, valid roles are as follows: ["provider_admin", "provider_class_category"] |

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
      "relationships": {
        "token": {
          "data": null
        }
      },
      "links": {
        "self": "/results/90"
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

Returns all result for the current result's organization.

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
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/results/96"
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
      "relationships": {
        "token": {
          "data": null
        }
      },
      "links": {
        "self": "/athletes/90"
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

Returns all athlete for the current athlete's organization.

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
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/athletes/96"
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
     -d '{"athlete": {"first_name": "Sam", "surname": "Watson", "email": "athlete@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/athletes/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "athlete@domain.com"
    }
  }
}
```

Create a athlete for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/athletes/:id`

### Attributes

| Parameter  | Description                                                                          |
| ---------- | ------------------------------------------------------------------------------------ |
| first_name | The first name of the athlete                                                        |
| surname    | The surname of the athlete                                                           |
| email      | The email of the athlete                                                             |
| password   | The password of the athlete                                                          |
| roles      | The athlete role, valid roles are as follows: ["provider_admin", "provider_athlete"] |

### Query Parameters

This endpoint does not support query parameters.

## Update a Athlete

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"athlete": {"first_name": "Sam", "surname": "Watson", "email": "athlete@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/athletes/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "athlete@domain.com"
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
| email      | The email of the athlete                                                             |
| password   | The password of the athlete                                                          |
| roles      | The athlete role, valid roles are as follows: ["provider_admin", "provider_athlete"] |

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
      "relationships": {
        "token": {
          "data": null
        }
      },
      "links": {
        "self": "/horses/90"
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

Returns all horse for the current horse's organization.

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
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/horses/96"
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
     -d '{"horse": {"first_name": "Sam", "surname": "Watson", "email": "horse@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/horses/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "horse@domain.com"
    }
  }
}
```

Create a horse for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/horses/:id`

### Attributes

| Parameter  | Description                                                                      |
| ---------- | -------------------------------------------------------------------------------- |
| first_name | The first name of the horse                                                      |
| surname    | The surname of the horse                                                         |
| email      | The email of the horse                                                           |
| password   | The password of the horse                                                        |
| roles      | The horse role, valid roles are as follows: ["provider_admin", "provider_horse"] |

### Query Parameters

This endpoint does not support query parameters.

## Update a Horse

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"horse": {"first_name": "Sam", "surname": "Watson", "email": "horse@domain.com", "password": "abc123", role:"provider_admin"}}'
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
    "relationships": {},
    "links": {
      "self": "/horses/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "horse@domain.com"
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
| first_name | The first name of the horse                                                      |
| surname    | The surname of the horse                                                         |
| email      | The email of the horse                                                           |
| password   | The password of the horse                                                        |
| roles      | The horse role, valid roles are as follows: ["provider_admin", "provider_horse"] |

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
      "relationships": {
        "token": {
          "data": null
        }
      },
      "links": {
        "self": "/federations/90"
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

Returns all federation for the current federation's organization.

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
    "relationships": {
      "token": {
        "data": null
      }
    },
    "links": {
      "self": "/federations/96"
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
     -d '{"federation": {"first_name": "Sam", "surname": "Watson", "email": "federation@domain.com", "password": "abc123", role:"provider_admin"}}'
     'https://eventing.api.equiratings.com/v1/federations'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "federation",
    "relationships": {},
    "links": {
      "self": "/federations/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "federation@domain.com"
    }
  }
}
```

Create a federation for the supplied data.

### HTTP Request

`POST https://eventing.api.equiratings.com/v1/federations/:id`

### Attributes

| Parameter  | Description                                                                                |
| ---------- | ------------------------------------------------------------------------------------------ |
| first_name | The first name of the federation                                                           |
| surname    | The surname of the federation                                                              |
| email      | The email of the federation                                                                |
| password   | The password of the federation                                                             |
| roles      | The federation role, valid roles are as follows: ["provider_admin", "provider_federation"] |

### Query Parameters

This endpoint does not support query parameters.

## Update a Federation

```shell
curl -XPUT
     -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9'
     -H "Content-type: application/json"
     -d '{"federation": {"first_name": "Sam", "surname": "Watson", "email": "federation@domain.com", "password": "abc123", role:"provider_admin"}}'
     'https://eventing.api.equiratings.com/v1/federations'
```

> The above command returns JSON structured like this:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "type": "federation",
    "relationships": {},
    "links": {
      "self": "/federations/92"
    },
    "id": "92",
    "attributes": {
      "surname": "Watson",
      "role": "provider_admin",
      "id": 92,
      "first-name": "Sam",
      "email": "federation@domain.com"
    }
  }
}
```

Update a federation for the supplied data.

### HTTP Request

`PUT https://eventing.api.equiratings.com/v1/federations/:id`

### Attributes

| Parameter  | Description                                                                                |
| ---------- | ------------------------------------------------------------------------------------------ |
| first_name | The first name of the federation                                                           |
| surname    | The surname of the federation                                                              |
| email      | The email of the federation                                                                |
| password   | The password of the federation                                                             |
| roles      | The federation role, valid roles are as follows: ["provider_admin", "provider_federation"] |

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
