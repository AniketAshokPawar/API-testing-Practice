Topic 5 --- PUT, PATCH & DELETE API
-------------------------

### 1\. PUT

`PUT` is generally used when we want to **replace/update a resource**.

If the resource has 6 fields and you want to change only 2, a typical PUT request sends the **complete resource representation**, including the 4 unchanged fields.

Example:

```
{
  "name": "Rahul",
  "email": "rahul@gmail.com",
  "age": 27,
  "city": "Mumbai",
  "phone": "1234567890",
  "role": "QA"
}
```

The exact required fields depend on the **API contract**. So don't say in an interview that *PUT always requires every field*.

### 2\. PATCH

`PATCH` is used for a **partial update**.

If you want to change only `name` and `city`:

```
{
  "name": "Rahul",
  "city": "Mumbai"
}
```

You don't need to send the other unchanged fields.

### 3\. Playwright syntax

**PUT:**

```
const response = await request.put(url, {
    data: {
        id: 1,
        title: "Updated Title",
        body: "Updated Body",
        userId: 1
    }
});
```

**PATCH:**

```
const response = await request.patch(url, {
    data: {
        title: "Updated Title"
    }
});
```

### 4\. PUT vs PATCH --- VVIP

| PUT | PATCH |
| --- | --- |
| Generally used for complete replacement | Used for partial update |
| Usually sends the complete resource | Sends only fields to be changed |
| Can replace existing values | Changes specific fields |
| Exact behavior depends on API contract | Exact behavior depends on API contract |

### Interview answer

> **PUT is generally used to replace the complete resource, so the request usually contains the complete resource representation. PATCH is used for partial updates, where we can send only the fields that need to be changed. The exact behavior depends on the API contract.**

### Important point

Don't memorize:

> ❌ "PUT always requires all fields."

Memorize:

> ✅ **"PUT generally represents a complete replacement; whether all fields are mandatory depends on the API contract."**


### Complete example

```
import {test,expect} from "@playwright/test";

test("API topic 04 test", async({request})=>{

 const  response  =  await  request.put('https://jsonplaceholder.typicode.com/posts/1', {

 data:{

 title :  "Updated by Playwright",

 body :  "Learning PUT API",

 userId :  1

        }

    })

 const  responseBody  =  await  response.json();

 expect(response.status()).toBe(200);

 expect(responseBody.title).toBe("Updated by Playwright");

 expect(responseBody.body).toBe("Learning PUT API");

 expect(responseBody.userId).toBe(1);

 console.log(`Before patch:${responseBody}`);

 const  patchResponse  =  await  request.patch('https://jsonplaceholder.typicode.com/posts/1', {

 data:{

 title :  "Patched by Playwright"

        }

    })

 const  patchResponseBody  =  await  patchResponse.json();

 expect(patchResponse.status()).toBe(200);

 expect(patchResponseBody.title).toBe("Patched by Playwright");

 console.log(`After patch:${patchResponseBody}`);

})
```

DELETE API
----------

### DELETE

-   Used to **delete/remove a resource** from the server.
-   Playwright syntax:

```
const response = await request.delete(url);
```

### Status Codes

| Status | Meaning |
| --- | --- |
| `200` | Delete successful, response may contain body |
| `202` | Delete request accepted for processing |
| `204` | Delete successful, no response body |

> Expected status depends on the API contract. DELETE does **not always return 200**.

### Response Body

-   DELETE may or may not return a response body.
-   If JSON is returned:

```
const responseBody = await response.json();
```

-   For `204 No Content`, there is no response body to read.

### DELETE vs PATCH

| Method | Purpose |
| --- | --- |
| `DELETE` | Delete the resource |
| `PATCH` | Partially update the resource |
| `PUT` | Generally replace/update the complete resource |

-   DELETE normally **does not delete individual fields** from an object.
-   If only a field needs to be removed, the API may provide a `PATCH` or a specific API operation for that purpose.

### VVIP Interview Questions

**Q1. What is DELETE used for?**\
To remove a resource from the server.

**Q2. Does DELETE always return 200?**\
No. It can commonly return `200`, `202`, or `204`, depending on the API contract.

**Q3. Can DELETE delete individual fields?**\
Normally no. DELETE is intended to remove the resource. Removing individual fields is generally handled through PATCH or an API-specific operation.

```
```

### Complete example

```
import {test, expect} from "@playwright/test";

test("API topic 05 test", async({request})=>{

    const response = await request.delete('https://jsonplaceholder.typicode.com/posts/1');

    expect(response.status()).toBe(200);
    console.log(`Status code: ${response.status()}`);
})
```
