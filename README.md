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

## 3. Creating and Deleting Resources

### Summary

- A method is considered safe when it dosen't change the resource representation.
- A method is considered idempotent when it can be called multiple times with the same result.

- POST is used to create a resource
    - Is Unsafe
    - Is Not idempotent
    - Returns 201 Created
    - Returns Location header of the created resource

- Use the content-type header to signify the media type of the request body
- DELETE is used to delete resources
  - Unsafe
  - Idempotent
  - 204 No Content
  
## 4.Updating Resources

### Overview

#### Updating Resources
- PUT for full updates
- PATCH for partial updates

#### Upserting
- Creating a resource with PUT or PATCH

### Summary

#### PUT for full updates
- It's important to remember that all fields have to be updated with the PUT request. Fields that are not passed in the PUT request should be set to its default values.
- A successful PUT request warrents 200 Ok or 204 No Content
- Not safe as it changes the resource
- It is idempotent

#### PATCH for partial updates
- The body of the PATCH request is defined by the JSON patch standard. It describes how to pass through a list of operations that have to be applied to the resource. 
- A successful PATCH request also warrents 200 Ok or 204 No content StatusCode just like PUT.
- Not Safe
- Not idempotent

#### Upserting
- Possible when the consumer of the API is allowed to create the resource URI.






 

