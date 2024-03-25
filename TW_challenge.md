# API Documentation: Desafio TW

## Introduction

Welcome to the API documentation for Desafio TW. This documentation provides details about the endpoints, request parameters, response formats, and error handling for interacting with the API.

## Endpoints

The following section describes the API endpoints details. 

### Authorization

This endpoint is used to obtain an access token required for authorization to access other API endpoints.

**Endpoint**  

- **Method:** POST
- **URL:** `https://horizon-api-sb.app.rpe.tech/oauth2/token`

##### Request Parameters

- **grant_type:** Type of access grant (e.g., "password").
- **username:** User's username for authentication.
- **password:** User's password.

##### Example Request

```
POST https://horizon-api-sb.app.rpe.tech/oauth2/token
Authorization: Basic cnBlY2xpZW50OlVreUk4UHRudGlpalczemdhSlQ1YkxOQWNJUGFEdUZS
Content-Type: application/x-www-form-urlencoded

grant_type=password&username=rpe-sandbox&password=1Rpe@dmi4.22
```

##### Example Response  

```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 3600,
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "scope": "read write"
}

```
### API portador  

#### GET/Portadores/{idPortador}

This endpoint is used to retrieve detailed information about a specific portador.

**Endpoint**   

- **Method:** GET
- **URL:** `{{gateway}}portadores/{idPortador}`

##### Request Parameters  

- **IdPortador:** Unique portador identifier

##### Request example 

```
GET https://horizon-api-sb.app.rpe.tech/api/v1/portadores/2001
Authorization: Bearer [Access Token]
```

##### Response example 

```json
{
  "id": 2001,
  "nome": "João da Silva",
  "email": "exemplo@email.com",
  ...
}
```

#### GET/Portadores/{idPortador}/telefones

This endpoint is used to retrieve telephone information for a specific portador.

**Endpoint**  

- **Method:** GET
- **URL:** `{{gateway}}portadores/{idPortador}/telefones`  

##### Request example

```
GET {{gateway}}portadores/2001/telefones
Authorization: Bearer <access_token>
```

##### Response example

```json
[
  {
    "id": 1,
    "tipo": "CELULAR",
    "ramal": "4020",
    "area": "83",
    "telefone": "999999999"
  }
]
```

#### PATCH/Portadores/{idPortador}

This endpoint is used to update information for a specific portador.

**Endpoint**  

- **Method:** PATCH
- **URL:** `{{gateway}}portadores/2001`  

##### Request example

```
PATCH {{gateway}}portadores/2001
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "nome": "João da Silva",
  "email": "exemplo@email.com",
  "nacionalidade": "BRASILEIRA",
  "cidadeNatal": "SÃO PAULO",
  "estadoNatal": "SP",
  ...
}
```

##### Response example

```json
{
  "message": "Portador information updated successfully."
}
```


### POST/portadores/bloqueios

This endpoint is used to block specific portadores.

**Endpoint**  

- **Method:** POST
- **URL:** `{{gateway}}portadores/bloqueios`

##### Request Parameters

- **IdTipoBloqueio:** Type of block to be applied
- **IdTitular:** ID of the holder to be blocked.
- **IdUsuario:** ID of the user responsible for the block.
- **Observacao:** Additional note about blocking.

##### Request example 

```
POST https://horizon-api-sb.app.rpe.tech/api/v1/portadores/bloqueios
Authorization: Bearer [Access Token]
Content-Type: application/json

{
  "idTipoBloqueio": 15,
  "idTitular": 2001,
  "idUsuario": 1,
  "observacao": "Bloqueado"
}
```

##### Example Response

```json
{
  "idBloqueio": 12345,
  "mensagem": "Portador bloqueado com sucesso."
}
```

### DELETE/portadores/{idPortador}/telefones/{idTelefone}

Delete a telephone record for a specific portador.

- **Method:** DELETE
- **URL:** `{{gateway}}portadores/2001/telefones/1`

#### Request example

```
DELETE {{gateway}}portadores/2001/telefones/1
Authorization: Bearer <access_token>
```

### Error Handling

The API may return the following HTTP status codes for error situations:

- **400 Bad Request:** Invalid request.
- **401 Unauthorized:** Authentication failure or lack of authorization.
- **404 Not found:** Resource not found.
- **500 Internal Server Error:** Server-side error.

