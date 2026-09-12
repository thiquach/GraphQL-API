# GraphQL-API
 
Learn GraphQL based on REST API experience

| REST/gRPC concept          | GraphQL equivalent                      |
| -------------------------- | --------------------------------------- |
| Endpoint                   | Field/query/mutation                    |
| `GET /customers/123`       | `query { customer(id: "123") { ... } }` |
| Request/response DTO       | GraphQL type/schema                     |
| URL parameters             | Arguments                               |
| JSON response              | Selection set                           |
| Multiple REST calls        | One GraphQL query                       |
| HTTP POST/PUT/DELETE       | Mutations                               |
| API contract               | GraphQL schema                          |
| Service implementation     | Resolver                                |
| Authentication             | Context/middleware                      |
| Service-to-service calls   | Resolver → backend services             |
| -------------------------- | --------------------------------------- |

Five important concepts:

Schema and types
Queries
Mutations
Resolvers
Variables and arguments

Then learn authentication/authorisation, error handling, pagination and N+1/query performance.

=============================================================

Part 1 — GraphQL fundamentals

Learn:

GraphQL architecture
schema
types
queries
mutations
arguments
variables
resolvers
GraphQL vs REST

Write several queries.

Part 2 — Go implementation

Build the small Go API.

Focus on:

GraphQL schema
     ↓
Resolver
     ↓
Service
     ↓
Repository

Get queries and mutations working.

================================
Tools:

Use Apollo Explorer/Sandbox to experiment with real queries without first having to build a GraphQL server

- Use Apollo GraphOS Studio to build, test, and manage GraphQL APIs
- Connect to a public Countries GraphQL API: https://countries.trevorblades.com by entering the URL as the graph/API endpoint
- Check that the schema/documentation become available

================================
Exercise 1:

Use Apollo Explorer to run the first query

query {
  countries {
    code
    name
  }
}

Response is in the JSON format something conceptually like the following:
{
  "data": {
    "countries": [
      {
        "code": "AD",
        "name": "Andorra"
      },
      {
        "code": "AE",
        "name": "United Arab Emirates"
      }
    ]
  }
}

Look carefully at the structure:

query
  ↓
countries
  ↓
code
name

This is the fundamental GraphQL mental model. The server responds to the query and sends exactly which fields that were requested.

Exercise 2:

Use Apollo Explorer to run other queries to access other available fields and then into the types returned by those fields.

Try this:
Query
 └── countries
       ├── code
       ├── name
       ├── capital
       ├── currency
       └── ...

Select different fields and observe how Explorer changes my query.

This is actually a very good way to learn as I'm  discovering the schema rather than memorising syntax.

Exercise 3:

Try:
Query {
  country(code: "AU") {
    code
    name
    capital
    currency
  }
}

Notice what changed.

Instead of:
countries

I have:
country(code: "AU")

I've just encountered a GraphQL argument.

Exercise 4:

Introduce variables

Instead of harding the code "AU".
Write:

query GetCountry($code: ID!) {
  country(code: $code) {
    code
    name
    capital
    currency
  }
}

Then find the Variables area in Explorer and enter:

{
  "code": "AU"
}

Now I have learned three important concepts:

Operation
   ↓
Variables
   ↓
Arguments
   ↓
Fields

Apollo's tooling supports working with variables separately from the operation, which is an important pattern for real GraphQL clients.

The GraphQL query and response flow:

                    GraphQL client
                         |
                         | query
                         ↓
                  ┌───────────────┐
                  │ GraphQL API   │
                  │               │
                  │    Schema     │
                  │       ↓       │
                  │   Resolver    │
                  │       ↓       │
                  │ Backend svc   │
                  └───────┬───────┘
                          |
                          ↓
                    Data sources

Exercise 5:

More queries

Exercise 6:

Mutations

Exercise 7:

Go implementation
