Topic 1: API Testing Basics
===========================

1\. What is an API?
-------------------

**API = Application Programming Interface**

An API allows two software systems to communicate with each other.

### Simple example

Suppose you have an e-commerce application:

**UI → Backend → Database**

When you open the **My Orders** page:

```
User clicks "My Orders"
        ↓
Frontend sends API request
        ↓
Backend processes request
        ↓
Backend gets data from database
        ↓
Backend sends API response
        ↓
UI displays orders
```

The API is the communication layer between the frontend and backend.

* * * * *

2\. What is API Testing?
========================

**API testing means testing the backend APIs directly without depending on the UI.**

We send a request to an API and verify the response.

For example:

```
GET /users/101
```

We verify:

-   Status code
-   Response body
-   Response data
-   Response headers
-   Response time, if required

### Interview answer

> **API testing is testing the backend services directly by sending API requests and validating the response, such as status code, response body, headers, and data.**

* * * * *

3\. What is an API Request?
===========================

A **request** is what the client sends to the server.

A request generally contains:

```
HTTP Method
Endpoint / URL
Headers
Request Body
```

Example:

```
POST https://example.com/api/users
```

Request body:

```
{
  "name": "Aniket",
  "email": "aniket@test.com"
}
```

* * * * *

4\. What is an API Response?
============================

A **response** is what the server sends back after processing the request.

Example:

```
Status: 201
```

Response body:

```
{
  "id": 101,
  "name": "Aniket",
  "email": "aniket@test.com"
}
```

So remember:

```
REQUEST  → Client sends something
RESPONSE → Server sends something back
```

* * * * *

5\. What is an Endpoint?
========================

An **endpoint** is the specific URL through which we access an API.

Example:

```
https://example.com/api/users
```

Here:

```
https://example.com
        ↓
Base URL

/api/users
        ↓
Endpoint path
```

Another example:

```
/api/users/101
```

This can represent a specific user.

### Easy way to remember

> **Endpoint = Address of an API**

* * * * *

6\. HTTP Methods
================

These are the most important methods for API testing.

| Method | Purpose | Example |
| --- | --- | --- |
| GET | Retrieve data | Get user |
| POST | Create data | Create user |
| PUT | Update entire resource | Update user |
| PATCH | Partially update resource | Update email |
| DELETE | Delete data | Delete user |

### Easy memory trick

```
GET     → Read
POST    → Create
PUT     → Update
PATCH   → Partial Update
DELETE  → Delete
```

* * * * *

7\. GET Request
===============

Used to **retrieve data**.

Example:

```
GET /api/users/101
```

Possible response:

```
{
  "id": 101,
  "name": "Aniket"
}
```

We may verify:

```
Status = 200
id = 101
name = Aniket
```

* * * * *

8\. POST Request
================

Used to **create new data**.

Example:

```
POST /api/users
```

Request body:

```
{
  "name": "Aniket",
  "email": "aniket@test.com"
}
```

Possible response:

```
Status = 201
```

```
{
  "id": 101,
  "name": "Aniket",
  "email": "aniket@test.com"
}
```

* * * * *

9\. PUT vs PATCH
================

Both are used for updating data.

### PUT

Generally used when updating/replacing the resource as a whole.

```
PUT /api/users/101
```

```
{
  "name": "Aniket",
  "email": "new@test.com",
  "city": "Pune"
}
```

### PATCH

Generally used when updating only specific fields.

```
PATCH /api/users/101
```

```
{
  "city": "Pune"
}
```

### Interview answer

> **PUT is generally used to update or replace the complete resource, while PATCH is used for partial updates.**

* * * * *

10\. DELETE Request
===================

Used to delete a resource.

```
DELETE /api/users/101
```

Possible response:

```
204 No Content
```

* * * * *

11\. HTTP Status Codes
======================

These are **very important for API testing interviews.**

### 2xx --- Success

| Code | Meaning |
| --- | --- |
| 200 | OK / successful request |
| 201 | Resource created |
| 204 | Successful request with no response body |

### 4xx --- Client-side error

| Code | Meaning |
| --- | --- |
| 400 | Bad Request |
| 401 | Unauthorized / authentication required |
| 403 | Forbidden |
| 404 | Resource not found |

### 5xx --- Server-side error

| Code | Meaning |
| --- | --- |
| 500 | Internal Server Error |

### Easy memory

```
2xx → Success
4xx → Client/request problem
5xx → Server problem
```

* * * * *

12\. What do we validate in API Testing?
========================================

When testing an API, don't just check the status code.

Usually we validate:

### 1\. Status code

```
Expected: 200
Actual:   200
```

### 2\. Response body

Example:

```
{
  "id": 101,
  "name": "Aniket"
}
```

Verify:

```
id = 101
name = Aniket
```

### 3\. Response headers

For example:

```
Content-Type: application/json
```

### 4\. Response structure

Verify that expected fields exist:

```
id
name
email
```

### 5\. Business data

For example:

```
User status should be "active"
```

* * * * *

13\. API Testing vs UI Testing
==============================

This is useful in interviews.

### UI Testing

```
Browser
   ↓
UI
   ↓
API
   ↓
Backend
```

You test the application through the user interface.

### API Testing

```
Test script
   ↓
API
   ↓
Backend
```

You directly communicate with the backend API.

### Advantage of API testing

API tests are generally:

-   Faster than UI tests
-   Less dependent on UI
-   Useful for validating backend functionality
-   Useful for preparing test data
-   Useful for validating data created through UI

* * * * *

14\. API Testing using Playwright
=================================

Playwright provides **`APIRequestContext`** for API testing.

It allows us to send requests such as:

```
GET
POST
PUT
PATCH
DELETE
```

and validate the responses.

Example:

```
import { test, expect } from '@playwright/test';

test('Get users through API', async ({ request }) => {
  const response = await request.get('https://example.com/api/users');

  expect(response.status()).toBe(200);
});
```

Here:

```
request.get(...)
```

sends a GET request.

And:

```
response.status()
```

gets the HTTP status code.

Then:

```
expect(response.status()).toBe(200);
```

checks that the API returned `200`.

* * * * *

15\. Important Playwright API Terms
===================================

You will see these frequently:

### `request`

Playwright's request fixture used to make API calls.

```
async ({ request }) => {
```

### `APIRequestContext`

Playwright's API request object/context used for sending HTTP requests.

### `response`

The object returned by the API call.

```
const response = await request.get(url);
```

Then we can get information from it:

```
response.status()
response.headers()
response.json()
response.text()
```

* * * * *

16\. The basic API testing flow
===============================

Remember this flow:

```
1\. Identify API endpoint
        ↓
2. Select HTTP method
        ↓
3. Send request
        ↓
4. Receive response
        ↓
5. Check status code
        ↓
6. Check response body
        ↓
7. Check headers/data/business conditions
```

This is basically what you'll do repeatedly while writing API tests.

* * * * *

17\. VVIP Interview Questions
=============================

### Q1. What is API testing?

> API testing is testing backend services directly by sending API requests and validating the response, including status code, response body, headers, and data.

### Q2. What is an endpoint?

> An endpoint is the specific URL through which an API can be accessed.

### Q3. What is the difference between GET and POST?

> GET is generally used to retrieve data, while POST is used to create new data.

### Q4. PUT vs PATCH?

> PUT is generally used to update or replace the complete resource, while PATCH is used for partial updates.

### Q5. What does 200 mean?

> The request was successfully processed.

### Q6. What does 201 mean?

> A resource was successfully created.

### Q7. What does 401 mean?

> Authentication is required or the provided authentication credentials are invalid.

### Q8. What does 404 mean?

> The requested resource or endpoint was not found.

### Q9. What does 500 mean?

> An internal server-side error occurred.

### Q10. How do you perform API testing in Playwright?

> Playwright provides `APIRequestContext` and the `request` fixture, which allow us to send HTTP requests such as GET, POST, PUT, PATCH, and DELETE and validate their responses.
