Topic 3: GET API --- Response Body & JSON Validation
==================================================

We'll continue using the same public API:

```
https://jsonplaceholder.typicode.com/users/1
```

When you open it, the API returns something like:

```
{
  "id": 1,
  "name": "Leanne Graham",
  "username": "Bret",
  "email": "Sincere@april.biz",
  "address": {
    "street": "Kulas Light",
    "city": "Gwenborough"
  },
  "phone": "1-770-736-8031",
  "website": "hildegard.org",
  "company": {
    "name": "Romaguera-Crona"
  }
}
```

Don't worry about every field yet. We'll focus on how Playwright reads this response.

* * * * *

1\. We already know how to get the status
-----------------------------------------

From Topic 2:

```
const response = await request.get(
  'https://jsonplaceholder.typicode.com/users/1'
);

expect(response.status()).toBe(200);
```

This checks:

> Did the API request succeed?

But **200 alone doesn't tell us whether the returned data is correct.**

For example, imagine the API returns:

```
{
  "id": 5,
  "name": "Wrong User"
}
```

The status could still be:

```
200
```

So our test would pass if we only checked:

```
expect(response.status()).toBe(200);
```

That's why we need to validate the **response body**.

* * * * *

2\. Getting the response body
=============================

Playwright provides:

```
await response.json()
```

Example:

```
const responseBody = await response.json();
```

Now:

```
response
   ↓
response.json()
   ↓
JSON response body
   ↓
responseBody
```

So your test becomes:

```
import { test, expect } from '@playwright/test';

test('Get user 1', async ({ request }) => {

    const response = await request.get(
        'https://jsonplaceholder.typicode.com/users/1'
    );

    expect(response.status()).toBe(200);

    const responseBody = await response.json();

    console.log(responseBody);
});
```

* * * * *

3\. What does `response.json()` actually do?
============================================

This is important.

The server sends a response body.

For example:

```
{
  "id": 1,
  "name": "Leanne Graham",
  "email": "Sincere@april.biz"
}
```

`response.json()` reads that JSON data and converts it into a JavaScript object that you can work with.

So:

```
const responseBody = await response.json();
```

gives you something conceptually like:

```
responseBody = {
    id: 1,
    name: "Leanne Graham",
    email: "Sincere@april.biz"
};
```

Now we can access individual fields.

* * * * *

4\. Accessing individual JSON fields
====================================

Suppose:

```
const responseBody = await response.json();
```

The response contains:

```
{
  "id": 1,
  "name": "Leanne Graham",
  "email": "Sincere@april.biz"
}
```

We can access:

```
responseBody.id
```

```
responseBody.name
```

```
responseBody.email
```

For example:

```
console.log(responseBody.id);
console.log(responseBody.name);
console.log(responseBody.email);
```

Output:

```
1
Leanne Graham
Sincere@april.biz
```

* * * * *

5\. Validating individual fields
================================

Now we get to the actual API testing.

We can write:

```
expect(responseBody.id).toBe(1);
```

This means:

> I expect the `id` returned by the API to be 1.

And:

```
expect(responseBody.name).toBe('Leanne Graham');
```

Meaning:

> I expect the returned user's name to be Leanne Graham.

And:

```
expect(responseBody.email).toBe('Sincere@april.biz');
```

* * * * *

6\. Complete example
====================

Your Topic 3 test can look like this:

```
import { test, expect } from '@playwright/test';

test('Get user 1', async ({ request }) => {

    const response = await request.get(
        'https://jsonplaceholder.typicode.com/users/1'
    );

    expect(response.status()).toBe(200);

    const responseBody = await response.json();

    console.log(responseBody);

    expect(responseBody.id).toBe(1);
    expect(responseBody.name).toBe('Leanne Graham');
    expect(responseBody.email).toBe('Sincere@april.biz');
});
```

Now we're testing **two things**:

### 1\. Status

```
expect(response.status()).toBe(200);
```

### 2\. Response data

```
expect(responseBody.id).toBe(1);
expect(responseBody.name).toBe('Leanne Graham');
expect(responseBody.email).toBe('Sincere@april.biz');
```

That's much more meaningful than checking only `200`.
