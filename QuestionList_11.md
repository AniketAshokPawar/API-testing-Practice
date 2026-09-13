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

11\. ⭐⭐⭐ What is Bearer token authentication and how do you use it? What is API-key authentication and Basic authentication? | ⭐⭐⭐ |
=================================================

Think of authentication as the API asking:

> **"Before I give you this data or allow you to perform this action, how do I know you are allowed to access it?"**

Without authentication, anyone who knows the API URL could potentially call it.

Let's understand the 3 methods using **one common example: a banking API**.

* * * * *

First: What happens WITHOUT authentication?
===========================================

Suppose a banking API has:

```
GET /accounts/12345/balance
```

If there is **no authentication**, someone could simply send:

```
GET /accounts/12345/balance
```

and potentially get:

```
{
  "account": "12345",
  "balance": 85000
}
```

That's obviously dangerous.

So the API says:

> "Prove who you are / prove that you're allowed to access me."

That's where authentication comes in.

* * * * *

1\. Bearer Token 🔐
===================

### Think of it as:

**"I logged in. Here is my access pass."**

Suppose you log into a banking application:

```
Username: Aniket
Password: ********
```

The server verifies your credentials.

Then it gives you a token:

```
eyJhbGciOiJIUzI1NiIs...
```

Now when your application wants your account balance, it sends:

```
GET /accounts/12345/balance
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

The server checks the token.

If valid:

```
{
  "balance": 85000
}
```

If invalid/expired:

```
401 Unauthorized
```

### Why is this useful?

Because you **don't send your username/password with every API request**.

You login once → receive token → use token for subsequent requests.

### Where is Bearer token commonly used?

Very common in:

-   Web applications
-   Mobile applications
-   REST APIs
-   Microservices
-   OAuth 2.0-based systems

### Simple real-life analogy

You enter an office.

At reception:

> "Show your ID."

After verification, they give you an **access badge**.

For the rest of the day, you show the badge to enter authorized areas.

**Login = verification**

**Bearer token = access badge**

* * * * *

2\. API Key 🔑
==============

API key is slightly different.

Think:

> **"I am an application/service that has been given a key to use your API."**

Suppose you create an application that uses a weather API.

You register your application with the weather API provider.

They give you:

```
API Key = abc123xyz
```

Whenever your application asks for weather:

```
GET /weather?city=Pune
x-api-key: abc123xyz
```

The weather server checks:

```
Is abc123xyz a valid API key?
```

If yes:

```
{
  "city": "Pune",
  "temperature": 28
}
```

If not:

```
401 Unauthorized
```

### Why is API key useful?

The API provider can identify:

> "Which application is using my API?"

It can also help with:

-   Usage limits
-   Tracking API usage
-   Controlling access
-   Billing
-   Revoking access to a particular application

### Where is API key commonly used?

For example:

-   Weather APIs
-   Maps APIs
-   Payment/third-party APIs
-   Public developer APIs
-   AI/third-party service APIs

### Simple analogy

Imagine a hotel gives a **special key card to a travel agency** so its employees can access a particular service.

The key identifies the **application/service** using the API.

* * * * *

3\. Basic Authentication 👤🔑
=============================

This is the simplest one.

You directly send:

```
Username + Password
```

For example:

```
username = admin
password = admin123
```

The request uses:

```
Authorization: Basic <encoded username:password>
```

You don't normally manually create that Base64 value; the client/library does it.

### Playwright

```
const response = await request.get('/users/101', {
  httpCredentials: {
    username: 'admin',
    password: 'admin123',
  },
});
```

The server checks:

```
Username = admin?
Password = admin123?
```

If correct:

```
200 OK
```

If incorrect:

```
401 Unauthorized
```

### Where is Basic Auth useful?

You may see it in:

-   Internal APIs
-   Legacy applications
-   Simple services
-   Development/testing environments
-   Some admin tools

It is less common for modern public applications compared with token-based authentication.


13\. What is API Chaining?
==========================

API chaining means using the response from one API request as input for another API request.

### Real example: Create user → Get user

### Step 1: Create a user

```
POST /users
```

Response:

```
{
  "id": 101,
  "name": "Aniket"
}
```

### Step 2: Use the returned ID

```
GET /users/101
```

Here, the `id` received from the POST response is used in the GET request.

### Playwright example

```
test('API chaining', async ({ request }) => {
  const createResponse = await request.post('/users', {
    data: {
      name: 'Aniket',
      email: 'aniket@test.com',
    },
  });

  expect(createResponse.status()).toBe(201);

  const createdUser = await createResponse.json();
  const userId = createdUser.id;

  const getResponse = await request.get(`/users/${userId}`);

  expect(getResponse.status()).toBe(200);
});
```

Interview answer:

> API chaining means passing data from one API response to the next API request. For example, after creating a user, I take the generated user ID and use it to fetch or update that user.

14\. How do you perform Negative API Testing?
=============================================

Negative API testing checks how the API behaves when invalid or unexpected input is provided.

We should verify that:

-   The API returns the correct error status.

-   The error message is meaningful.

-   Invalid data is not saved.

-   Sensitive information is not exposed.


### Playwright example

```
test('Reject user creation without email', async ({ request }) => {
  const response = await request.post('/users', {
    data: {
      name: 'Aniket',
    },
  });

  expect(response.status()).toBe(400);

  const body = await response.json();
  expect(body.error).toContain('email');
});
```

Interview answer:

> In negative API testing, I send invalid data, missing fields, invalid tokens, incorrect IDs, and unauthorized requests. Then I verify the expected error status, error message, and that the invalid operation was not completed.

15\. How do you validate an API response?
=========================================

I validate an API response at different levels:

1.  Status code

2.  Response body

3.  Important fields

4.  Headers

5.  Response time, when required

6.  Schema, if contract validation is needed

### Playwright example

```
test('Validate API response', async ({ request }) => {
  const response = await request.get('/users/101');

  expect(response.status()).toBe(200);

  const body = await response.json();

  expect(body.id).toBe(101);
  expect(body.name).toBe('Aniket');
  expect(body.email).toContain('@');

  expect(response.headers()['content-type'])
    .toContain('application/json');
});
```

Interview answer:

> I validate the status code first, then parse the response body and verify important fields and their values. I also validate headers, error messages, and response schema when required.

16\. How do you perform API testing using Playwright?
=====================================================

Playwright supports API testing through its request functionality. We can send HTTP requests without opening a browser.

### Basic flow

1.  Use the `request` fixture.

2.  Send a GET, POST, PUT, PATCH, or DELETE request.

3.  Read the response.

4.  Validate status, body, fields, and headers.

### Example

```
import { test, expect } from '@playwright/test';

test('Get user API', async ({ request }) => {
  const response = await request.get('/users/101');

  expect(response.status()).toBe(200);

  const body = await response.json();

  expect(body.id).toBe(101);
});
```

Interview answer:

> In Playwright, I use the `request` fixture to send API requests. I validate the response status, JSON body, fields, headers, and error scenarios using Playwright assertions.


19\. How do you perform GET, POST, PUT, PATCH, and DELETE?
==========================================================

```
import { test, expect } from '@playwright/test';

test('HTTP methods using Playwright', async ({ request }) => {
  // GET
  const getResponse = await request.get('/users/101');
  expect(getResponse.status()).toBe(200);

  // POST
  const postResponse = await request.post('/users', {
    data: {
      name: 'Aniket',
      email: 'aniket@test.com',
    },
  });
  expect(postResponse.status()).toBe(201);

  // PUT
  const putResponse = await request.put('/users/101', {
    data: {
      name: 'Updated Aniket',
      email: 'updated@test.com',
      status: 'Active',
    },
  });
  expect(putResponse.status()).toBe(200);

  // PATCH
  const patchResponse = await request.patch('/users/101', {
    data: {
      status: 'Inactive',
    },
  });
  expect(patchResponse.status()).toBe(200);

  // DELETE
  const deleteResponse = await request.delete('/users/101');
  expect(deleteResponse.status()).toBe(204);
});
```

### Quick syntax

```
request.get(url)
request.post(url, { data: body })
request.put(url, { data: body })
request.patch(url, { data: body })
request.delete(url)
```

Interview answer:

> Playwright provides separate methods for each HTTP operation. I use `get()` for reading, `post()` for creating, `put()` for replacement, `patch()` for partial updates, and `delete()` for deleting resources.

> The expected status code depends on the API contract. For example, POST commonly returns 201 and DELETE commonly returns 204, but these are not guaranteed for every API.

20\. How do you validate status code, body, fields, and headers?
================================================================

```
import { test, expect } from '@playwright/test';

test('Validate complete API response', async ({ request }) => {
  const response = await request.get('/users/101');

  // 1. Validate status code
  expect(response.status()).toBe(200);

  // 2. Validate successful response
  await expect(response).toBeOK();

  // 3. Read response body
  const body = await response.json();

  // 4. Validate complete body or important fields
  expect(body).toEqual(
    expect.objectContaining({
      id: 101,
      name: 'Aniket',
    }),
  );

  // 5. Validate individual fields
  expect(body.id).toBe(101);
  expect(body.name).toBe('Aniket');
  expect(body.email).toContain('@');

  // 6. Validate response headers
  const headers = response.headers();

  expect(headers['content-type'])
    .toContain('application/json');
});
```

### `status()` vs `toBeOK()`

```
expect(response.status()).toBe(200);
```

Checks for exactly status 200.

```
await expect(response).toBeOK();
```

Checks whether the response is generally successful, usually within the 2xx range.

### Interview answer

> I validate the exact status code using `response.status()`. Then I parse the body using `response.json()` and verify important fields with assertions. I also check response headers such as `content-type`. When I only need to verify that the response is successful, I use `toBeOK()`.

21\. What is `expect(response).toBeOK()` and how is it different from `status() === 200`?
=========================================================================================

Suppose we send:

```
const response = await request.get('/users/101');
```

### Option 1 --- Check exact status

```
expect(response.status()).toBe(200);
```

This means:

> **I specifically expect status code 200.**

If the API returns `201`, `204`, etc., this assertion fails.

* * * * *

### Option 2 --- `toBeOK()`

```
await expect(response).toBeOK();
```

This means:

> **I expect the API request to be successful.**

`toBeOK()` checks for a successful **2xx status**.

For example:

```
200 → ✅
201 → ✅
204 → ✅

400 → ❌
401 → ❌
404 → ❌
500 → ❌
```

### Simple difference

| Code | Meaning |
| --- | --- |
| `response.status() === 200` | I want **exactly 200** |
| `expect(response).toBeOK()` | I want a **successful 2xx response** |

### When would you use which?

If your API contract specifically says:

> GET `/users/101` must return 200

Use:

```
expect(response.status()).toBe(200);
```

If you only care that the request was successful:

```
await expect(response).toBeOK();
```

### 🎯 Interview answer

> `toBeOK()` verifies that the response has a successful 2xx status code. `response.status()` allows me to check an exact status code, such as 200. So if I specifically expect 200, I use `status()`, while `toBeOK()` is useful when any successful 2xx response is acceptable.

* * * * *

22\. How do you pass headers, query parameters and request body in Playwright?
==============================================================================

This is **very important practically**.

There are three different things:

-   **Headers** → additional information about the request
-   **Query parameters** → parameters added to the URL
-   **Request body** → data sent inside the request

* * * * *

1\. Headers
-----------

Example:

```
Authorization: Bearer abc123
Content-Type: application/json
```

In Playwright:

```
const response = await request.get('/users/101', {
  headers: {
    Authorization: 'Bearer abc123',
    'Content-Type': 'application/json',
  },
});
```

* * * * *

2\. Query parameters
--------------------

Suppose API URL is:

```
/users?role=QA&status=Active
```

Instead of manually creating the URL, Playwright allows:

```
const response = await request.get('/users', {
  params: {
    role: 'QA',
    status: 'Active',
  },
});
```

Playwright creates:

```
/users?role=QA&status=Active
```

### Another example

```
const response = await request.get('/users', {
  params: {
    page: 2,
    limit: 10,
  },
});
```

* * * * *

3\. Request body
----------------

Usually used with POST, PUT and PATCH.

```
const response = await request.post('/users', {
  data: {
    name: 'Aniket',
    email: 'aniket@test.com',
    role: 'QA',
  },
});
```

The JSON body sent is:

```
{
  "name": "Aniket",
  "email": "aniket@test.com",
  "role": "QA"
}
```

### 🎯 Interview answer

> In Playwright, I pass headers using the `headers` option, query parameters using `params`, and request body using the `data` option. For example, `headers` can contain authentication information, `params` are used for URL query parameters, and `data` is used to send JSON request data.

### Quick memory

```
request.get(url, {
  headers: {},   // Header
  params: {},    // Query parameter
  data: {},      // Request body
});
```

* * * * *

23\. How do you reuse authentication/token in Playwright API tests?
===================================================================

Imagine you have **10 API tests**.

If every test does this:

```
Login
 ↓
Get token
 ↓
Call API
```

then you're unnecessarily logging in 10 times.

Instead, we can get the token once and reuse it.

### Simple example

Suppose login API returns:

```
{
  "token": "abc123xyz"
}
```

We store it:

```
const token = loginResponseBody.token;
```

Then use it:

```
const response = await request.get('/users/101', {
  headers: {
    Authorization: `Bearer ${token}`,
  },
});
```
