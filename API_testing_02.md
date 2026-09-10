Topic 2: Playwright `APIRequestContext`
=======================================

Now we move from **API concepts → actually using Playwright for API testing**.

The goal of this topic is that you understand what `request` is, how Playwright creates an API connection, and how we send our first API request.

* * * * *

1\. What is `APIRequestContext`?
--------------------------------

In Playwright, **`APIRequestContext` is the object/context that allows us to send HTTP API requests.**

Think of it like this:

```
Browser Context
      ↓
Used for UI testing

APIRequestContext
      ↓
Used for API testing
```

For API testing, instead of opening a browser and clicking things, Playwright can directly communicate with the backend.

```
Your test
   ↓
APIRequestContext
   ↓
Backend API
   ↓
Response
```

* * * * *

2\. The easiest way --- Playwright `request` fixture
==================================================

For normal API tests, Playwright provides a built-in fixture called **`request`**.

Example:

```
import { test, expect } from '@playwright/test';

test('Get user', async ({ request }) => {

  const response = await request.get('https://example.com/api/users/1');

  expect(response.status()).toBe(200);

});
```

Don't worry about the URL for now. We'll use proper practice APIs when we start actual testing.

* * * * *

3\. Understand this code carefully
==================================

### Line 1

```
import { test, expect } from '@playwright/test';
```

Same as your normal Playwright UI tests.

-   `test` → creates the test
-   `expect` → performs assertions

* * * * *

### Line 2

```
test('Get user', async ({ request }) => {
```

This is the important part.

Normally in UI testing you might have:

```
test('Login', async ({ page }) => {
```

Here:

```
page
 ↓
UI/browser testing
```

For API testing:

```
async ({ request }) => {
```

Here:

```
request
 ↓
API testing
```

So:

> **`page` is mainly used to interact with the UI, while `request` is used to send API requests.**

* * * * *

4\. Sending a GET request
=========================

```
const response = await request.get(
  'https://example.com/api/users/1'
);
```

Let's break it down.

### `request.get()`

Means:

> Send a GET request to this endpoint.

### `await`

The API call takes some time.

So we wait until the server responds.

### `response`

The API returns a response, and we store it in:

```
const response
```

Think:

```
request.get()
      ↓
API call
      ↓
server response
      ↓
response variable
```

* * * * *

5\. What can we get from `response`?
====================================

This is very important.

The response object gives us information about the API response.

For example:

```
response.status()
```

gets the status code.

```
response.headers()
```

gets response headers.

```
response.json()
```

gets the response body as JSON.

```
response.text()
```

gets the response body as text.

So:

```
response
 ├── status()
 ├── headers()
 ├── json()
 └── text()
```

We'll learn each of these properly in upcoming topics.

* * * * *

6\. First assertion
===================

We can check the status code:

```
expect(response.status()).toBe(200);
```

Meaning:

> I expect the API response status to be 200.

If actual response is:

```
200
```

Test passes.

If actual response is:

```
404
```

Test fails.

* * * * *

7\. Complete basic example
==========================

```
import { test, expect } from '@playwright/test';

test('Get user', async ({ request }) => {

  const response = await request.get(
    'https://example.com/api/users/1'
  );

  expect(response.status()).toBe(200);

});
```

### Flow

```
test starts
   ↓
request.get()
   ↓
GET API called
   ↓
server responds
   ↓
response stored
   ↓
status extracted
   ↓
status compared with 200
   ↓
PASS / FAIL
```

That's your first basic Playwright API test.

* * * * *

8\. What is `baseURL`?
======================

Suppose your application has many APIs:

```
https://myapp.com/api/users
https://myapp.com/api/products
https://myapp.com/api/orders
```

Writing the complete URL every time is repetitive.

We can define:

```
baseURL = https://myapp.com
```

Then use:

```
/api/users
/api/products
/api/orders
```

instead.

In Playwright configuration, you can define a base URL:

```
import { defineConfig } from '@playwright/test';

export default defineConfig({
  use: {
    baseURL: 'https://myapp.com'
  }
});
```

Then:

```
const response = await request.get('/api/users');
```

Playwright uses:

```
https://myapp.com
      +
/api/users
```

So the actual request becomes:

```
https://myapp.com/api/users
```

### Why is this useful?

If your environment changes:

```
DEV
QA
PREPROD
PROD
```

you don't want to hard-code the complete URL in every test.

* * * * *

9\. `request` vs `APIRequestContext`
====================================

This can be confusing initially.

### `request`

The fixture you commonly use directly inside tests:

```
test('API test', async ({ request }) => {
```

### `APIRequestContext`

The actual Playwright API request context.

You can also create one manually when you need more control.

For example:

```
const context = await request.newContext();
```

Then:

```
const response = await context.get(url);
```

But **don't worry about manually creating contexts yet**.

For your normal API tests, start with:

```
async ({ request }) => {
```

That's the simplest approach.

* * * * *

10\. Why do we need an API request context?
===========================================

Imagine you have 20 API tests.

You need something that can:

-   Send GET requests
-   Send POST requests
-   Send PUT requests
-   Send PATCH requests
-   Send DELETE requests
-   Handle headers
-   Handle authentication
-   Receive responses

`APIRequestContext` provides that API-testing capability.

* * * * *

11\. Important difference from UI testing
=========================================

### UI test

```
test('Login', async ({ page }) => {

  await page.goto('/login');

  await page.locator('#username').fill('Aniket');

  await page.locator('#password').fill('12345');

  await page.locator('button').click();

});
```

You're interacting with the UI.

### API test

```
test('Get user', async ({ request }) => {

  const response = await request.get('/api/users/1');

  expect(response.status()).toBe(200);

});
```

No browser.

No clicking.

No locator.

You're directly communicating with the backend.

* * * * *

12\. What about POST?
=====================

The same `request` object can send different HTTP methods.

```
await request.get(url);
```

```
await request.post(url);
```

```
await request.put(url);
```

```
await request.patch(url);
```

```
await request.delete(url);
```

So you can think:

```
request
   │
   ├── get()
   ├── post()
   ├── put()
   ├── patch()
   └── delete()
```

We'll learn these one by one.

* * * * *

13\. Headers --- basic understanding
==================================

An API request can also contain headers.

For example:

```
const response = await request.get('/api/users', {
  headers: {
    'Accept': 'application/json'
  }
});
```

Here:

```
headers
   ↓
Additional information sent with request
```

Later you'll commonly see headers such as:

```
Content-Type
Authorization
Accept
```

Don't try to memorize all headers now. Authentication and headers will be covered separately.

* * * * *

14\. One important concept: API context is not the browser
==========================================================

This is worth remembering.

When you do:

```
const response = await request.get('/api/users');
```

Playwright **doesn't open a browser**.

It directly sends an HTTP request.

```
❌ Browser → UI → API

API test:

✅ Test → API → Backend
```

That's one of the biggest differences between Playwright UI testing and Playwright API testing.

* * * * *

15\. Interview Questions --- Topic 2
==================================

### Q1. How do you perform API testing in Playwright?

> Playwright provides `APIRequestContext` for API testing. We can use the built-in `request` fixture to send HTTP requests and validate the responses.

* * * * *

### Q2. What is the `request` fixture?

> `request` is a built-in Playwright fixture that allows us to send API requests such as GET, POST, PUT, PATCH, and DELETE.

* * * * *

### Q3. What is `APIRequestContext`?

> `APIRequestContext` is Playwright's API request context used to send HTTP requests and work with API responses.

* * * * *

### Q4. Does Playwright open a browser when we use `request.get()`?

> No. `request.get()` directly sends an HTTP request to the API without interacting with the browser UI.

* * * * *

### Q5. How do you get the status code from an API response?

```
response.status()
```

* * * * *

### Q6. How do you get the response body?

```
await response.json()
```
