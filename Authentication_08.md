Topic 8 --- Authentication
========================

Authentication is used when an API needs to **verify who is making the request** before allowing access.

For example, a public API like JSONPlaceholder can be accessed without authentication. But a real company API may require a token, API key, username/password, etc.

The main authentication methods we need to know are:

1.  Bearer Token
2.  API Key
3.  Basic Authentication
4.  Reusing authentication

* * * * *

1\. Bearer Token
----------------

A **Bearer token** is a token sent with the request, usually in the `Authorization` header.

Example:

```
Authorization: Bearer abc123xyz
```

In Playwright:

```
const response = await request.get(url, {
    headers: {
        Authorization: `Bearer ${token}`
    }
});
```

Here:

-   `Authorization` → header name
-   `Bearer` → authentication scheme
-   `token` → actual token

### Where does the token come from?

Usually, you first call a **login/authentication API**.

For example:

```
POST /login
```

with username/password.

The server may return:

```
{
    "token": "abc123xyz"
}
```

Then you use that token in subsequent API requests.

* * * * *

2\. API Key
-----------

An **API key** is another way of identifying/authenticating the client.

It may be sent in a header such as:

```
x-api-key: abc123xyz
```

Playwright:

```
const response = await request.get(url, {
    headers: {
        "x-api-key": apiKey
    }
});
```

The exact header name depends on the API.

Some APIs may use:

```
x-api-key
```

while others may use a different name.

* * * * *

3\. Basic Authentication
------------------------

Basic authentication uses a **username and password**.

Playwright provides a convenient option:

```
const response = await request.get(url, {
    httpCredentials: {
        username: "testuser",
        password: "password123"
    }
});
```

Playwright handles the Basic Authentication mechanism for the request.

### Important

Don't confuse Basic Authentication with sending:

```
{
    "username": "testuser",
    "password": "password123"
}
```

in the request body.

With Basic Authentication, the credentials are provided through the HTTP authentication mechanism.

* * * * *

4\. Reusing Authentication
==========================

This is very important for automation.

Imagine you have **20 API tests**.

If every test has to:

```
Login → get token → call API
```

then you're repeating the login process unnecessarily.

Instead, you can:

1.  Authenticate once.
2.  Get the token.
3.  Reuse the authentication information for multiple API requests.

For example:

```
const token = "abc123xyz";

const response1 = await request.get("/users", {
    headers: {
        Authorization: `Bearer ${token}`
    }
});

const response2 = await request.get("/orders", {
    headers: {
        Authorization: `Bearer ${token}`
    }
});
```

In a real Playwright framework, authentication is often moved into a **setup/helper/fixture** so that individual tests don't repeatedly implement the login logic.

Complete Bearer Token Workflow
==============================

### Real-world scenario

Imagine an application has these APIs:

1.  `POST /login` → user logs in and receives a token
2.  `GET /users` → requires that token
3.  `GET /orders` → also requires that token

So the automation flow is:

**Login → Get token → Send token in header → Access protected API → Validate response**

* * * * *

Complete Playwright example
---------------------------

```
import { test, expect } from '@playwright/test';

test("Complete API authentication workflow", async ({ request }) => {

    // 1. Login API
    const loginResponse = await request.post('https://api.example.com/login', {
        data: {
            username: "testuser",
            password: "password123"
        }
    });

    // 2. Validate login response
    expect(loginResponse.status()).toBe(200);

    // 3. Read login response body
    const loginBody = await loginResponse.json();

    // 4. Extract token from response
    const token = loginBody.token;

    expect(token).toBeTruthy();

    // 5. Call protected API using Bearer token
    const usersResponse = await request.get(
        'https://api.example.com/users',
        {
            headers: {
                Authorization: `Bearer ${token}`
            }
        }
    );

    // 6. Validate protected API response
    expect(usersResponse.status()).toBe(200);

    // 7. Read protected API response
    const usersBody = await usersResponse.json();

    // 8. Validate response data
    expect(usersBody).toBeTruthy();

    console.log(usersBody);
});
```

Now let's understand **exactly what happens at every step**.

* * * * *

Step 1 --- Import Playwright
==========================

```
import { test, expect } from '@playwright/test';
```

We import:

-   `test` → to create our test
-   `expect` → to perform assertions

Nothing special about authentication here.

* * * * *

Step 2 --- Start the test
=======================

```
test("Complete API authentication workflow", async ({ request }) => {
```

Here:

```
request
```

is Playwright's built-in API request fixture.

We use it to send API requests without opening a browser.

For example:

```
request.get()
request.post()
request.put()
request.patch()
request.delete()
```

* * * * *

Step 3 --- Login
==============

First, the application needs to know **who we are**.

So we call the login API:

```
const loginResponse = await request.post(
    'https://api.example.com/login',
    {
        data: {
            username: "testuser",
            password: "password123"
        }
    }
);
```

We send:

```
{
    "username": "testuser",
    "password": "password123"
}
```

to the login endpoint.

Think of this as:

> "Hello server, here are my username and password. Please authenticate me."

* * * * *

Step 4 --- Server validates login
===============================

Suppose the server says:

> Username and password are correct.

It may return:

```
{
    "token": "abc123xyz789"
}
```

So:

```
loginResponse
```

contains the complete HTTP response.

* * * * *

Step 5 --- Check login was successful
===================================

```
expect(loginResponse.status()).toBe(200);
```

We verify that login succeeded.

For example:

```
200 → Login successful
401 → Invalid credentials
403 → Access forbidden
```

The exact status depends on the API contract.

* * * * *

Step 6 --- Read the response body
===============================

```
const loginBody = await loginResponse.json();
```

Suppose the response was:

```
{
    "token": "abc123xyz789"
}
```

Then:

```
loginBody
```

contains:

```
{
    token: "abc123xyz789"
}
```

* * * * *

Step 7 --- Extract the token
==========================

This is the **most important line**:

```
const token = loginBody.token;
```

We take:

```
abc123xyz789
```

and store it in:

```
token
```

So now:

```
token = "abc123xyz789"
```

* * * * *

Step 8 --- Validate that token exists
===================================

```
expect(token).toBeTruthy();
```

This checks that the token is actually present.

Basically:

> "After login, did I really receive a token?"

* * * * *

Step 9 --- Call protected API
===========================

Now suppose we want to access:

```
GET /users
```

But this API requires authentication.

So we send the token in the request header:

```
const usersResponse = await request.get(
    'https://api.example.com/users',
    {
        headers: {
            Authorization: `Bearer ${token}`
        }
    }
);
```

This produces a request header like:

```
Authorization: Bearer abc123xyz789
```

* * * * *

Why do we use `Bearer`?
=======================

Because this is the authentication scheme expected by many APIs.

The actual header looks like:

```
Authorization: Bearer <token>
```

For example:

```
Authorization: Bearer abc123xyz789
```

So this:

```
Authorization: `Bearer ${token}`
```

is basically saying:

> "Server, here is my authentication token. Please verify it and allow me to access this API."

* * * * *

Step 10 --- Server validates token
================================

The server receives:

```
GET /users

Authorization: Bearer abc123xyz789
```

The server checks the token.

If valid:

```
200 OK
```

If missing/invalid:

```
401 Unauthorized
```

So our test checks:

```
expect(usersResponse.status()).toBe(200);
```

* * * * *

Step 11 --- Read the protected API response
=========================================

```
const usersBody = await usersResponse.json();
```

Suppose the server returns:

```
{
    "users": [
        {
            "id": 1,
            "name": "John"
        },
        {
            "id": 2,
            "name": "David"
        }
    ]
}
```

Now `usersBody` contains that JSON.

* * * * *

Step 12 --- Validate the actual data
==================================

For example:

```
expect(usersBody).toBeTruthy();
```

Or, depending on the API:

```
expect(usersBody.users.length).toBeGreaterThan(0);
```

or:

```
expect(usersBody.users[0].id).toBe(1);
```

Now we're not only checking:

> "Did the API respond?"

We're checking:

> "Did the API return the correct data?"

* * * * *

So the COMPLETE FLOW is
=======================

Imagine this happening in real life:

### 1\. Login

```
POST /login
username + password
```

Server:

```
{
    "token": "abc123"
}
```

### 2\. Store token

```
const token = loginBody.token;
```

### 3\. Send token

```
GET /users

Authorization: Bearer abc123
```

### 4\. Server validates token

```
Token valid
      ↓
Allow access
```

### 5\. API returns data

```
{
    "users": [...]
}
```

### 6\. Test validates data

```
expect(usersResponse.status()).toBe(200);
```
