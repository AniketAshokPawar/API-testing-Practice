1\. What is a Header?
---------------------

Think of an API request/response like sending a **parcel**.

-   **Body** = the actual content/data inside the parcel.
-   **Headers** = information/labels attached to the parcel that tell the receiver how to handle the content.

For an API:

```
Request
├── Headers → additional information about the request
└── Body    → actual data being sent
```

And the server sends back:

```
Response
├── Headers → additional information about the response
└── Body    → actual data returned by the server
```

* * * * *

2\. What kind of information is in headers?
-------------------------------------------

For example, the server might return:

```
content-type: application/json
```

This basically means:

> "The data I'm returning is in JSON format."

Another common header is:

```
Authorization: Bearer abc123
```

This means:

> "Here is the authentication information for this request."

Another example:

```
Content-Type: application/json
```

This tells the server:

> "The data I'm sending in my request body is JSON."

So headers provide **metadata/information about the request or response**.

* * * * *

3\. Why are headers used in APIs?
=================================

Headers are used for things like:

### Authentication

```
Authorization: Bearer <token>
```

Used to tell the server **who is making the request / whether they are authorized**.

### Data format

```
Content-Type: application/json
```

Tells the server what format the request body contains.

### Response format

```
Accept: application/json
```

Tells the server:

> "I want the response in JSON format."

There are many other headers, but these are the important ones for your current API-testing preparation.

* * * * *

4\. Where are headers used?
===========================

Headers can exist in **both requests and responses**.

### Request

Your Playwright test sends:

```
GET /users/1

Headers:
Authorization: Bearer abc123
Accept: application/json
```

The server uses this information to process your request.

### Response

The server sends back:

```
200 OK

Headers:
Content-Type: application/json

Body:
{
   "id": 1,
   "name": "Leanne Graham"
}
```

So:

**Request headers → Client → Server**

**Response headers → Server → Client**

* * * * *

5\. Now your code becomes easy to understand
============================================

You have:

```
expect(response.headers()['content-type'])
    .toContain('application/json');
```

Break it down:

### `response`

This is the response you received from the API.

### `response.headers()`

This gets the **headers from that response**.

For example, it might give something conceptually like:

```
{
    "content-type": "application/json; charset=utf-8",
    "cache-control": "..."
}
```

### `['content-type']`

We are selecting only the `content-type` header.

So:

```
response.headers()['content-type']
```

might give:

```
application/json; charset=utf-8
```

### `.toContain('application/json')`

We're checking that the value contains:

```
application/json
```

Therefore:

```
expect(response.headers()['content-type'])
    .toContain('application/json');
```

basically means:

> **"Verify that the API response says its content is JSON."**

* * * * *

6\. Why do we test headers?
---------------------------

Because the API might return the **correct data but incorrect metadata**.

For example, your API returns:

```
{
  "id": 1,
  "name": "Aniket"
}
```

The body looks correct.

But suppose the response header says:

```
Content-Type: text/html
```

That's suspicious because you're expecting JSON.

So API testing can verify **both the actual data and the information describing that data**.

### Simple memory trick

**Body = What data did I get?**

**Headers = What information/metadata came with that data?**
