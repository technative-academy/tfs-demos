# API Design Guide

> _These notes are not intended as a comprehensive guide to the topic. Their purpose is to guide you through the main areas you should learn about, with resources provided for further exploration. The goal is for you to learn enough to complete the associated challenge._

These notes explain what a web API is and why you might build one before moving to how to design requests, responses, URLs, and errors.

Examples use JSON and a simple space theme with **planets**, **moons**, and **missions**.

**Helpful references**
- [HTTP overview on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [What is an API on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Introduction)
- [REST glossary on MDN](https://developer.mozilla.org/en-US/docs/Glossary/REST)
- [JSON introduction](https://www.json.org/json-en.html)

---

## What is an API

An **API** is a contract that lets one piece of software ask another to do something or to provide information

For web APIs the contract travels over the internet using **HTTP** which is the same protocol your browser uses to load web pages

Plain language

- An API call is a **request** you send to an address such as `/planets`
- The server sends back a **response** that says whether it worked and may include data in **JSON** which is a simple text format for name-value data like `{"name": "Jupiter"}`

Why teams build an API
- To let a website fetch or update data stored on a server
- To allow mobile apps to talk to the same back end as the website
- To integrate with other systems in a controlled and documented way

A good API is predictable, well documented, and hard to misuse

**Read more**
- [What is a web API](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Introduction)
- [JSON basics on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)

---

## The client and the server

- The **client** sends a request. This could be a browser or a mobile app
- The **server** receives the request, does some work such as reading a database, then sends a response back
- The **contract** is the shared understanding of the URL to call, the method to use, the headers and body to send, and the possible responses you might get

A useful mental model is a polite conversation
- Client says what it wants at a particular address
- Server replies with a **status code** that says how it went and possibly a body with data or error details

**Read more**
- [Client-server model](https://en.wikipedia.org/wiki/Client%E2%80%93server_model)
- [What is a URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL)

---

## Why REST

**REST** is a set of ideas for building web APIs that fit neatly with HTTP

It treats the things in your system as **resources** such as `planets` and `moons` and gives them stable URLs

You manipulate those resources using standard HTTP methods such as GET and POST

Why REST is popular

- It is simple to understand once you know HTTP
- It reuses standard methods, status codes, and headers
- It works well with the web infrastructure you already have

**Read more**
- [REST glossary on MDN](https://developer.mozilla.org/en-US/docs/Glossary/REST)
- [REST overview on Wikipedia](https://en.wikipedia.org/wiki/Representational_state_transfer)

---

## The building blocks of HTTP

### Requests

Every **request** has the same basic shape

```
METHOD PATH HTTP/VERSION
```

Requests can also have headers, which provide information about the request:

```
METHOD PATH HTTP/VERSION
Header-Name: value
Another-Header: value
```

Requests can also have an optional body:

```
METHOD PATH HTTP/VERSION

Header-Name: value
Another-Header: value

optional request body
```

### Responses

Every **response** has the same basic shape

```
HTTP/VERSION STATUS_CODE Reason-Phrase
Header-Name: value
Another-Header: value

optional response body
```

Key terms
- **Method** says what kind of action this is such as GET or POST
- **URL** or **path** says which resource you are talking about such as `/planets/42`
- **Headers** are extra lines of information such as content type and authentication
- **Body** is the data you send or receive such as JSON text
- **Status code** is a three digit number in the response that tells you the outcome at a glance

**Read more**
- [HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [Content types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

---

## HTTP methods with their meaning

| Method  | Plain English meaning | Typical use |
|--------|------------------------|-------------|
| GET    | Tell me about this thing or list of things | Read a resource or collection |
| POST   | Create a new thing under this URL or run a command | Create in a collection |
| PUT    | Replace the thing at this exact URL | Full update or create at a known URL |
| PATCH  | Change part of the thing at this URL | Partial update |
| DELETE | Remove the thing at this URL | Delete |

Two useful properties
- **Safe** means it does not change the server state. GET is safe
- **Idempotent** means repeating the same request ends in the same state. PUT and DELETE are idempotent. POST is not

**Read more**
- [HTTP methods on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

---

## Status codes as a shared vocabulary

A status code tells the client what happened

Success
- **200 OK** when you return data in the body
- **201 Created** when you have created something. Include a `Location` header that points to the new resource
- **204 No Content** when the request succeeded but there is nothing to return such as after a delete

Client problems
- **400 Bad Request** when the request is malformed JSON or otherwise not parseable
- **401 Unauthorised** when credentials are missing or invalid
- **403 Forbidden** when authenticated but not allowed to do this
- **404 Not Found** when the thing does not exist or you choose to hide it
- **409 Conflict** on unique constraint conflicts and similar state clashes
- **412 Precondition Failed** when an `If-Match` ETag does not match which protects against lost updates
- **415 Unsupported Media Type** when the `Content-Type` is wrong
- **418 I am a teapot** is self explanatory
- **422 Unprocessable Entity** when the shape is valid JSON but field values fail validation
- **429 Too Many Requests** when the client is over the rate limit

Server problems
- **500 Internal Server Error** for unexpected failures
- **503 Service Unavailable** during maintenance or dependency outages

**Read more**
- [Status codes on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [418 explanation on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/418)

---

## Representations and content negotiation

A resource can be represented in different formats

We will use **JSON** which is simple to read and write

Tell the server what you are sending and what you can accept

- `Content-Type: application/json` for request bodies
- `Accept: application/json` to say what response formats you will accept

Keep JSON simple and stable. Use predictable field names and types.

Use ISO 8601 date strings such as `1610-01-07`

**Read more**
- [Content negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation)
- [JSON format](https://www.json.org/json-en.html)
- [Date and time string format ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)

---

## An example scenario

We will design an API that stores information about **planets**, their **moons**, and **space missions** that visit those planets

This scenario gives clear examples of common API patterns

---

## Resource modelling and URLs

Think in **nouns**, not verbs. Nouns become resources, and resources get URLs

Top level resources have their own URL paths

- `/planets`
- `/moons`
- `/missions`

Use predictable, hierarchical paths

- List planets
  `GET /planets`
- One planet by id
  `GET /planets/42`
- Moons that belong to a planet
  `GET /planets/42/moons`
- Create a moon under a planet
  `POST /planets/42/moons`

Simple path rules
- Use lower case and hyphens in path segments such as `/space-missions`
- Put ids in the path. Use query parameters for filtering and sorting
- Avoid verbs in paths
- Use HTTP methods to express actions
- Consider adding a version number prefix such as `/v1` - this allows you to upgrade the API in future with breaking changes

**Read more**
- [URL basics](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL)
- [API design guidance from Google style guide for naming inspiration](https://cloud.google.com/apis/design/naming_conventions)

---

## Requests and responses example

### Create a planet

**Request**
```
POST /planets
Content-Type: application/json
Accept: application/json

{
  "name": "Jupiter",
  "discovered_at": "1610-01-07"
}
```

**Response**
```
HTTP/1.1 201 Created
Location: /planets/1
Content-Type: application/json

{
  "id": 1,
  "name": "Jupiter",
  "discovered_at": "1610-01-07"
}
```

### List moons for a planet with filtering and pagination

**Request**
```
GET /planets/1/moons?sort=name&order=asc&page=2&per_page=3
Accept: application/json
```

**Response**
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": [
    { "id": 7, "name": "Callisto" },
    { "id": 8, "name": "Europa" },
    { "id": 9, "name": "Ganymede" }
  ],
  "meta": { "page": 2, "per_page": 3, "total": 12 }
}
```

**Read more**
- [Pagination patterns overview](https://developer.mozilla.org/en-US/docs/Glossary/Chunked_transfer_encoding#pagination_and_chunked_responses)

---

## Designing collection endpoints

Use query parameters for common collection concerns

- **Filtering**
  - `GET /missions?visited_planet=1`
  - `GET /planets?discovered_at_gte=1600-01-01`
- **Sorting**
  - `GET /planets?sort=discovered_at&order=desc`
- **Pagination**
  - Offset style with `page` and `per_page` is easy to learn
  - Cursor style with a `cursor` token scales better for very large or changing data sets


**Read more**
- [Query strings on MDN](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL#parameters)
- [Designing filter parameters tips](https://cloud.google.com/apis/design/design_patterns#list_pagination)

---

## Errors that help users fix mistakes

Use a consistent format for errors, for example:

```
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/problem+json

{
  "title": "Validation failed",
  "status": 422,
  "detail": "One or more fields are invalid",
  "errors": [
    { "field": "name", "message": "Name is required" },
    { "field": "discovered_at", "message": "Use ISO date format YYYY-MM-DD" }
  ]
}
```

Use status codes:

- **404** when a resource is not found
- **409** for conflicts such as duplicate names
- **415** for wrong content types

**Read more**
- [MDN on 4xx responses](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#client_error_responses)

---

## Authentication and authorisation

Start simple and keep secrets out of URLs

Common approaches
- **API keys** for server to server calls. Send as `Authorization: Api-Key <key>`
- **Bearer tokens** such as short lived JWTs. Send as `Authorization: Bearer <token>`
- **Cookie based sessions** for first party web apps. Combine with CSRF protection on unsafe methods such as POST or DELETE

Return **401** for missing or invalid credentials and **403** when authenticated but not allowed

**Read more**
- [HTTP authentication on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)
- [OAuth 2.0 overview](https://oauth.net/2/)
- [CSRF explained on MDN](https://developer.mozilla.org/en-US/docs/Glossary/CSRF)
- [JWT introduction](https://jwt.io/introduction)

---

## Documentation that developers can run

Write the contract down in **OpenAPI** so tools can read it

Benefits
- Human readable docs with examples
- Code generation for clients and servers if you choose
- Contract tests that check your implementation matches the spec

A tiny OpenAPI fragment

```yaml
openapi: 3.1.0
info:
  title: Space API
  version: 1.0.0
servers:
  - url: https://api.example.com
paths:
  /planets:
    get:
      summary: List planets
      parameters:
        - in: query
          name: page
          schema: { type: integer, minimum: 1, default: 1 }
        - in: query
          name: per_page
          schema: { type: integer, minimum: 1, maximum: 100, default: 20 }
      responses:
        "200":
          description: OK
          content:
            application/json:
              schema:
                type: object
                properties:
                  data:
                    type: array
                    items:
                      $ref: '#/components/schemas/Planet'
  /planets/{planet_id}:
    get:
      summary: Get a planet
      parameters:
        - in: path
          name: planet_id
          required: true
          schema: { type: integer }
      responses:
        "200":
          description: OK
components:
  schemas:
    Planet:
      type: object
      properties:
        id: { type: integer }
        name: { type: string }
        discovered_at: { type: string, format: date }
```

**Read more**
- [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Swagger UI](https://swagger.io/tools/swagger-ui/)
- [Redoc](https://redocly.com/redoc/)

---

## A minimal service outline in Node.js

This is a sketch to show where HTTP concerns live. It reads like Express pseudo-code

Responsibilities
- A **router** matches methods and paths to handlers
- **Middleware** checks authentication, content type, body size, and validation
- **Handlers** call the database and build responses
- A **central error handler** turns exceptions into problem details

```js
// routes
router.get('/planets', listPlanets)
router.post('/planets', authenticate, createPlanet)
router.get('/planets/:id', getPlanet)
router.patch('/planets/:id', authenticate, updatePlanet)
router.delete('/planets/:id', authenticate, deletePlanet)

// handler shapes
async function listPlanets(req, res) {
  const { page = 1, per_page = 20, sort = 'name', order = 'asc', fields } = req.query
  const result = await db.planets.findMany({ page, per_page, sort, order, fields })
  res.status(200).json({
    data: result.rows,
    meta: { page, per_page, total: result.total }
  })
}

async function createPlanet(req, res) {
  const planet = await db.planets.create(req.body)
  res.status(201).json(planet)
}
```

**Read more**
- [Express guides](https://expressjs.com/en/guide/routing.html)

---

## Security basics

- Use HTTPS in production so traffic is encrypted
- Store secrets such as API keys and database passwords outside the codebase
- For cookie sessions set `HttpOnly`, `Secure`, and an appropriate `SameSite` value.

**Read more**
- [OWASP API Security Top 10](https://owasp.org/API-Security/)
- [RateLimit header fields RFC 9238](https://www.rfc-editor.org/rfc/rfc9238)

---

## Practical conventions that keep APIs consistent

- Use predictable field names and types across resources
- Keep timestamps in ISO 8601 in UTC such as `2025-10-13T09:00:00Z`
- Use integers for ids unless you have a reason to use strings
- Choose one pagination style and use it everywhere

**Read more**
- [API design patterns overview](https://cloud.google.com/apis/design)
- [A style guide for SQL and naming inspiration for payloads](https://www.sqlstyle.guide/)

---

## Exercises

1. Design the URLs and methods for a missions resource. Include list, create, get one, update name, and delete
2. Add filtering to list planets by discovery century. Choose parameter names and write example URLs
3. Design a complete request and response for creating a moon
4. Extend the OpenAPI fragment to include `GET /planets/{planet_id}/moons` with response schema and an example

