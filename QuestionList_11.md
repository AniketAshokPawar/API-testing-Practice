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
