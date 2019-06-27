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

## 5.Working with Validation and Logging

### Overview

- Working with validation in a RESTful world.
- Validating on create and update.
- Logging faults, errors and additional information.

When talking about validation there is essentialy 3 things we need:
- We need a way to define validation rules
- We need a way to check validation the validation rules
- We need a way to report the validation errors to the consumer of the API

We don't use the error messages to let the consumer know whether he or the server made the mistake. That's what the status codes are for.

#### 1. Defining Validation Rules

In ASP.NET Core, rules are by default defined by using 
- Data annotations
- Custom code for when the annotations aren't sufficient

Validation is done on the input, not output.

#### 2. Checking Validation Rules
For checking validation rules in ASP.NET Core the building concept of ModelState is used. ModelState is the dictionary containing both the state of the model and the model binding Validation. It represents the collection of name and value pairs that were submitted to the API for each property. Whenever the request comes in the rules we defined in the step 1 are checked. When one of them is not checked out the ModelState's valid property will be false and this property will also be false if an invalid value for the property type is passed in.

##### ModelState
- A dictionary containing both the state of the model, and model binding validation.
- Contains a collection of error messages for each peoperty value submitted.
- ModelState.IsValid()

#### 3.Reporting Validation Errors
When the validation error happens the consumer of the API needs to be notified. It's the mistake of the client so the warrents 400 level StatusCode. There is one specifically used for this 422 Unprocessable entity. 422 status meanse the server understood the content type of the request entity, and the syntax of the request entity is correct but it was unable to process the contained instructions. For ex, the syntax is correct and the semantics are off and that's the perfect fit for what we need. But when we are talking about reporting validation errors we are not only talking about the StatusCodes, we are also talking about the response body. What we write out in the response body isn't regulated by REST, nor any of the standards we are using, but for validation issues this will often be a list of properties and the related error messages. 

Ex: 
> __Reporting Validation Errors__
> _Properties and their related error message(s)_ 
```  
    {
        ...        
        "Title":["You should fill out a title."],        
        "Description" : ["The description shouldn't have more than 500 characters."]        
    }
```
 If the client application needs to be able to do someting more than simply binding these errors to the control, Often an error code is included as well so the client application can act on that error code, also quite useful for multi-language applications. In ASP.NET Core MVC typically the ModelState's errors are searilized, so we end up with list of propertn names and related validation errors, But this can vary depending on what we are building API for. 

- Response status should be 422 - Unprocessable entity.
- Response body should contain validation errors.
- Often with an additional, custom error code.


#### Deom

##### Working with Validation on POST

##### Working with Validation on PUT

##### Working with Validation on PATCH

##### Logging Faults

##### Logging Errors and Other Information

##### Logging to a File


### Summary
#### Validation

There are 3 parts we have to keep in mind:
1. Defining validation rules 
    - (In ASP.NET core this is achieved with data annotations or with custom code. For more complex applications, acomponent like               [fluent validation can be used](https://github.com/JeremySkinner/FluentValidation,"FLUENT VALIDATION") )
    - Validations are defined for Input and not for Output.
    - If we do it with data annotations then it is one more good reason to use the different Dto's for different actions.
    
2. Checking Validation rules
    - This is what the ModelState is used for, a dictionary contating both the state of the model and the model binding validation 
    - We can check it's IsValid property.
3. Reporting validation errors
    - The advised StatusCode to use is 422 Unprocessable Entity. 
    - How errors should be defined in the response isn't covered by a standard, but field names combined with their errors and possibly         a custom error code are advised.
 
- When errors or faults happen, or you just want to save some additional information, we can use ASP.NET Core's built in logger.
- A logger can be extended with the third party middleware such as (NLog, Serilog etc..)
 
 
 Most restful API's provide additional functionalities like Paging, Filtering and Sorting.
    



 

