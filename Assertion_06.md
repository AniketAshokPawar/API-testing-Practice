Topic 7 --- Assertions
--------------------

### Assertions

Used to **verify that the API response matches the expected result**.

### 1\. Status Code

```
expect(response.status()).toBe(200);
```

Checks for an **exact status code**.

### 2\. `toBeOK()`

```
expect(response).toBeOK();
```

Checks that the response has a **successful 2xx status**.

-   `toBe(200)` → exactly `200`
-   `toBeOK()` → any successful `2xx` status

### 3\. Response Body

```
const responseBody = await response.json();

expect(responseBody.id).toBe(1);
expect(responseBody.name).toBe("Leanne Graham");
```

Used to validate values returned in the response body.

### 4\. Specific / Nested Fields

```
expect(responseBody.email).toBe("Sincere@april.biz");
expect(responseBody.address.city).toBe("Gwenborough");
```

You can validate only the fields relevant to your test instead of checking the entire response.

### 5\. Response Headers

```
expect(response.headers()['content-type'])
    .toContain('application/json');
```

Used to validate specific response headers.

### VVIP Interview Point

**What can we validate in an API response?**

> Status code, response body, specific fields, headers, and other expected response properties.

**Difference between `toBe(200)` and `toBeOK()`?**

> `toBe(200)` checks for exactly 200, whereas `toBeOK()` checks whether the response status is successful in the 2xx range.
