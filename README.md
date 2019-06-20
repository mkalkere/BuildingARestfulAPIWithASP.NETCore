# Building A Restful API With ASP.NET Core

## 1. Introducing REST

## 2. Getting Resources

### Outer facing contract
- Resource Identifiers
- HTTP Methods
- Optional Payload

### Resource identifiers
- Use pluraized nouns that convey meaning
- Represent model hierarchy
- Be consistent

### HTTP Methods
- GET - for getting resources
- POST - for creating resources
- PUT/PATCH - PUT for full and PATCH for partial updates
- DELETE - for deleting resources
- HEAD - is identical to GET but does not contain the payload in the response body. It is used to obtain the information on the resource
- OPTIONS - specifices what actions are allowed on the specific resource

### Payload
- Media Type: application/json, application/xml, ...

### Status codes
- Level 200: success
- Level 400: errors(client)
- Level 500: faults(server)

The outer facing model is conceptually different from the business model and/or entity model.