### ⭐⭐⭐ Must know --- don't skip

| # | Question | Priority |
| --- | --- | --- |
| 1 | **What is API testing and why do we perform it?** | ⭐⭐⭐ |
| 2 | **What is REST API? REST vs SOAP?** | ⭐⭐⭐ |
| 3 | **Explain GET, POST, PUT, PATCH and DELETE.** | ⭐⭐⭐ |
| 4 | **What is the difference between PUT and PATCH?** | ⭐⭐⭐ |
| 5 | **What is idempotency? Which HTTP methods are idempotent?** | ⭐⭐⭐ |
| 6 | **Explain important HTTP status codes: 200, 201, 204, 400, 401, 403, 404, 409, 500.** | ⭐⭐⭐ |
| 7 | **What is the difference between 400, 401 and 403?** | ⭐⭐⭐ |
| 8 | **What is the difference between path parameter, query parameter and request body?** | ⭐⭐⭐ |
| 9 | **What are request headers and response headers?** | ⭐⭐⭐ |
| 10 | **What is authentication vs authorization?** | ⭐⭐⭐ |
| 11 | **What is Bearer token authentication and how do you use it?** | ⭐⭐⭐ |
| 12 | **What is API-key authentication and Basic authentication?** | ⭐⭐⭐ |
| 13 | **What is API chaining? Give a real example.** | ⭐⭐⭐ |
| 14 | **How do you perform negative API testing?** | ⭐⭐⭐ |
| 15 | **How do you validate an API response?** | ⭐⭐⭐ |
| 16 | **How do you perform API testing using Playwright?** | ⭐⭐⭐ |
| 17 | **What is `APIRequestContext` in Playwright?** | ⭐⭐⭐ |
| 18 | **What is the Playwright `request` fixture?** | ⭐⭐⭐ |
| 19 | **How do you perform GET/POST/PUT/PATCH/DELETE using Playwright?** | ⭐⭐⭐ |
| 20 | **How do you validate status code, response body, fields and headers in Playwright?** | ⭐⭐⭐ |
| 21 | **What is `expect(response).toBeOK()` and how is it different from checking `status() === 200`?** | ⭐⭐⭐ |
| 22 | **How do you pass headers, query parameters and request body in Playwright?** | ⭐⭐⭐ |
| 23 | **How do you reuse authentication/token in Playwright API tests?** | ⭐⭐⭐ |
| 24 | **How would you create data through API and verify it through UI?** | ⭐⭐⭐ |
| 25 | **How would you perform a UI action and validate the result through API?** | ⭐⭐⭐ |
```
```
1\. ⭐⭐⭐ What is API testing and why do we perform it?
-----------------------------------------------------

### Answer

**API testing is testing the application's APIs directly by sending requests and validating the responses.**

We validate things like:

-   Status code
-   Response body
-   Response fields
-   Headers
-   Authentication
-   Error handling
-   Business logic


### Why API testing?

API testing is useful because:

-   It is faster than UI testing.
-   We can test backend functionality directly.
-   We can validate business logic before UI is ready.
-   It helps find backend issues early.
-   It can be automated easily.

### 🎯 Interview answer

> API testing is the process of testing APIs by sending requests and validating responses such as status codes, response body, headers, authentication and business logic. It helps us validate backend functionality independently of the UI and is generally faster than UI testing.

2\. ⭐⭐⭐ What is REST API? REST vs SOAP?
-----------------------------------------------------

1\. REST API --- simple explanation
---------------------------------

REST is a common, lightweight way for applications to communicate over HTTP.

It usually uses:

```
GET
POST
PUT
PATCH
DELETE
```

and commonly sends data in JSON format.

### Example

Your application wants user details:

```
GET /users/101
```

The server returns:

```
{
  "id": 101,
  "name": "Aniket",
  "role": "QA"
}
```

This is easy to read and easy to test using Playwright or Postman.

### Where is REST used?

REST is commonly used in:

-   Web applications

-   Mobile applications

-   E-commerce applications

-   Social media applications

-   Modern microservices

-   Frontend-to-backend communication

For example:

```
React/Angular UI
       ↓
REST API
       ↓
Backend/database
```

2\. SOAP API --- simple explanation
---------------------------------

SOAP is another way for applications to communicate.

The main difference is that SOAP normally uses a strict XML message format.

### Example

Instead of returning simple JSON:

```
{
  "id": 101,
  "name": "Aniket"
}
```

SOAP may return XML like:

```
<soap:Envelope>
    <soap:Body>
        <GetUserResponse>
            <User>
                <Id>101</Id>
                <Name>Aniket</Name>
            </User>
        </GetUserResponse>
    </soap:Body>
</soap:Envelope>
```

You do not need to memorize the complete XML structure. Just understand that SOAP messages are usually more structured and verbose.

### Where is SOAP used?

SOAP is commonly found in:

-   Banking systems

-   Insurance systems

-   Payment systems

-   Enterprise applications

-   Older/legacy systems

-   Systems requiring strict contracts and standards

For example, an old banking application may use SOAP for communication between internal services.

Main difference with a real-life example
========================================

Imagine ordering a product.

REST style
----------

You send a simple request:

```
POST /orders
```

```
{
  "productId": 101,
  "quantity": 2
}
```

Response:

```
{
  "orderId": 5001,
  "status": "Created"
}
```

The request and response are relatively simple.

SOAP style
----------

You send the same information inside a structured XML envelope:

```
<soap:Envelope>
    <soap:Body>
        <CreateOrder>
            <ProductId>101</ProductId>
            <Quantity>2</Quantity>
        </CreateOrder>
    </soap:Body>
</soap:Envelope>
```

The response also comes in a SOAP XML envelope.


The easiest way to remember
===========================

### REST

> Simple communication using HTTP methods and commonly JSON.

### SOAP

> Structured communication using XML-based messages and a defined protocol.

Interview-ready answer
======================

> REST and SOAP are two approaches for communication between applications. REST is an architectural style that commonly uses HTTP methods such as GET, POST, PUT, PATCH and DELETE, with JSON as the usual data format. SOAP is a protocol that uses structured XML messages. REST is commonly used in modern web and mobile applications, while SOAP is often found in enterprise, banking and legacy systems where strict messaging standards are required.

3\. ⭐⭐⭐ Explain GET, POST, PUT, PATCH and DELETE.
=================================================

This is **VVIP**.

| Method | Purpose | Example |
| --- | --- | --- |
| GET | Retrieve data | Get user |
| POST | Create resource/send data | Create user |
| PUT | Replace/update resource | Update complete user |
| PATCH | Partially update resource | Update only email |
| DELETE | Remove resource | Delete user |

### Example

```
GET /users/101
```

Get user.

```
POST /users
```

Create user.

```
PUT /users/101
```

Replace/update user.

```
PATCH /users/101
```

Update selected fields.

```
DELETE /users/101
```

Delete user.

### 🎯 Interview answer

> GET is used to retrieve data, POST is generally used to create a resource, PUT is generally used for complete replacement or update, PATCH is used for partial updates, and DELETE is used to remove a resource.


4\. ⭐⭐⭐ What is the difference between PUT and PATCH?
=====================================================

This is one of the **most commonly asked questions**.

Suppose a user has six fields:

```
{
  "name": "Aniket",
  "email": "aniket@test.com",
  "age": 27,
  "city": "Pune",
  "role": "QA",
  "status": "Active"
}
```

You want to update only:

```
name
email
```

### PUT

PUT is generally used to **replace the complete resource**.

A typical PUT request may contain:

```
{
  "name": "New Name",
  "email": "new@test.com",
  "age": 27,
  "city": "Pune",
  "role": "QA",
  "status": "Active"
}
```

### PATCH

PATCH is used for **partial updates**.

```
{
  "name": "New Name",
  "email": "new@test.com"
}
```

### Important interview nuance

Don't say:

> "PUT always requires every field."

Better say:

> **PUT is generally used to replace the complete resource, so the API contract may expect the complete resource representation. PATCH is generally used for partial updates.**

5\. ⭐⭐⭐ What is idempotency? Which HTTP methods are idempotent?
===============================================================

This is one of the **gaps we identified earlier**, so learn this properly.

### Simple meaning

An operation is **idempotent** if performing the same request multiple times has the same intended effect on the server state as performing it once.

### Example

Suppose:

```
PUT /users/101
```

with:

```
{
  "name": "Aniket"
}
```

Send it once:

```
name = Aniket
```

Send the same request again:

```
name = Aniket
```

The final state is still:

```
name = Aniket
```

So PUT is generally considered idempotent.

### Common classification

| Method | Generally idempotent? |
| --- | --- |
| GET | ✅ Yes |
| PUT | ✅ Yes |
| DELETE | ✅ Yes |
| POST | ❌ Generally no |
| PATCH | ⚠️ Not guaranteed |

### Important nuance

**Idempotent does not mean the response must be identical every time.**

It means the **intended server state** remains the same after repeated identical requests.

### 🎯 Interview answer

> Idempotency means that making the same request multiple times has the same intended effect on the server state as making it once. GET, PUT and DELETE are generally considered idempotent, while POST is generally non-idempotent. PATCH depends on how the API operation is designed.

6\. ⭐⭐⭐ Explain important HTTP status codes: 200, 201, 204, 400, 401, 403, 404, 409, 500.
===============================================================

HTTP Status Codes with Simple Examples
--------------------------------------

Assume we have a user API:

```
/users/101
```

### 200 --- OK ✅

The request was successful, and the server returns a response.

Example:

```
GET /users/101
```

Response:

```
{
  "id": 101,
  "name": "Aniket"
}
```

Meaning: User details were successfully fetched.

### 201 --- Created ✅

The request was successful, and a new resource was created.

Example:

```
POST /users
```

Request body:

```
{
  "name": "Aniket",
  "email": "aniket@test.com"
}
```

Response:

```
{
  "id": 101,
  "name": "Aniket",
  "email": "aniket@test.com"
}
```

Meaning: A new user was successfully created.

### 204 --- No Content ✅

The request was successful, but the server does not return a response body.

Example:

```
DELETE /users/101
```

Response:

```
204 No Content
```

Meaning: User 101 was deleted successfully, and there is no response body.

### 400 --- Bad Request ❌

The client sent invalid or incomplete data.

Example:

```
POST /users
```

Request body:

```
{
  "name": "Aniket"
}
```

Suppose the API requires both `name` and `email`.

Response:

```
{
  "error": "Email is required"
}
```

Meaning: The request data is invalid.

### 401 --- Unauthorized ❌

The request does not contain valid authentication credentials.

Example:

```
GET /users/101
Authorization: Bearer invalid_token
```

Response:

```
{
  "error": "Invalid or expired token"
}
```

Meaning: The user must provide valid authentication credentials.

> Simple memory trick: 401 = Who are you?

### 403 --- Forbidden ❌

The user is authenticated, but does not have permission to perform the action.

Example:

A normal user tries to delete another user:

```
DELETE /users/101
Authorization: Bearer valid_user_token
```

Response:

```
{
  "error": "You do not have permission to delete users"
}
```

Meaning: The user is logged in, but is not allowed to perform this action.

> Simple memory trick: 403 = I know who you are, but you are not allowed.

### 404 --- Not Found ❌

The requested resource does not exist.

Example:

```
GET /users/999
```

Suppose user `999` does not exist.

Response:

```
{
  "error": "User not found"
}
```

Meaning: The requested user or endpoint could not be found.

### 409 --- Conflict ❌

The request conflicts with the current server data.

Example:

A user already exists with this email:

```
POST /users
```

```
{
  "name": "Aniket",
  "email": "aniket@test.com"
}
```

Response:

```
{
  "error": "Email already exists"
}
```

Meaning: Creating this user conflicts with an existing user.

Other examples include:

-   Duplicate username

-   Duplicate email

-   Trying to book an already-booked seat

-   Updating a record that was changed by another user

### 500 --- Internal Server Error ❌

Something unexpected went wrong inside the server.

Example:

```
GET /users/101
```

The server has a database failure or an unhandled exception.

Response:

```
{
  "error": "Internal server error"
}
```

Meaning: The request reached the server, but the server failed while processing it.

8\. ⭐⭐⭐ Difference between path parameter, query parameter and request body?
============================================================================

Very important.

Path parameter
--------------

Used to identify a specific resource.

```
GET /users/101
```

Here:

```
101
```

is the path parameter.

Playwright:

```
await request.get('/users/101');
```

* * * * *

Query parameter
---------------

Usually used for filtering, searching, sorting or pagination.

```
GET /users?page=2&limit=10
```

Here:

```
page=2
limit=10
```

are query parameters.

Playwright:

```
await request.get('/users', {
    params: {
        page: 2,
        limit: 10
    }
});
```

* * * * *

Request body
------------

Used to send data to the server, commonly with POST/PUT/PATCH.

```
{
  "name": "Aniket",
  "email": "aniket@test.com"
}
```

Playwright:

```
await request.post('/users', {
    data: {
        name: "Aniket",
        email: "aniket@test.com"
    }
});
```

### Easy memory

> **Path = which resource**\
> **Query = filtering/options**\
> **Body = data being sent**

9\. ⭐⭐⭐ What are request headers and response headers?
======================================================

Headers contain **metadata/information about the HTTP request or response**.

### Request headers

Sent from client → server.

Example:

```
Authorization: Bearer abc123
Content-Type: application/json
Accept: application/json
```

### Response headers

Sent from server → client.

Example:

```
Content-Type: application/json
Cache-Control: no-cache
```

### In Playwright

Send headers:

```
const response = await request.get('/users', {
    headers: {
        Authorization: `Bearer ${token}`,
        Accept: 'application/json'
    }
});
```

Read response headers:

```
const headers = response.headers();

console.log(headers);
```

Validate:

```
expect(response.headers()['content-type'])
    .toContain('application/json');
```

### 🎯 Interview answer

> Headers contain metadata that provides additional information about an HTTP request or response. Request headers can contain things like authentication and content type, while response headers can provide information such as the response content type and caching behavior.

10\. ⭐⭐⭐ What is authentication vs authorization?
=================================================

This is extremely common.

### Authentication

**Authentication = Who are you?**

Example:

```
Username + Password
       ↓
Login successful
       ↓
Token generated
```

### Authorization

**Authorization = What are you allowed to do?**

Example:

```
User logged in
       ↓
Is this user allowed to delete an order?
       ↓
Yes / No
```

### Real example

Suppose:

```
Aniket logs in successfully
```

That's **authentication**.

Then:

```
Aniket tries to delete another user's account
```

The system checks whether Aniket has permission.

That's **authorization**.

### 🎯 Interview answer

> Authentication verifies the identity of the user or client, while authorization determines what that authenticated user or client is allowed to access or perform.
