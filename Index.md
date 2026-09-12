### Playwright API Testing --- our roadmap

We'll cover it in this order:

1.  **API Testing Basics**
    -   What is API testing?
    -   HTTP methods
    -   Request / Response
    -   Status codes
    -   Headers
    -   Request body
    -   Response body
2.  **Playwright APIRequestContext**
    -   `request.newContext()`
    -   `request.get()`
    -   `request.post()`
    -   `request.put()`
    -   `request.patch()`
    -   `request.delete()`
3.  **GET API**
    -   Send GET request
    -   Check status
    -   Read response
    -   Validate response body
4.  **POST API**
    -   Send JSON request body
    -   Validate response
    -   Dynamic request data
5.  **PUT / PATCH / DELETE**
6.  **Assertions**
    -   Status code
    -   Response body
    -   Headers
    -   Specific fields
    -   `expect(response).toBeOK()`
7.  **Authentication**
    -   Bearer token
    -   API key
    -   Basic authentication
    -   Reusing authentication
8.  **API + UI combination**
    -   Create data through API → verify through UI
    -   API setup → UI test
    -   UI action → API validation
9.  **API chaining**
    -   API 1 response → extract ID/token → use it in API 2
10. **Reusable API framework**

-   API utility/helper
-   Fixtures
-   Environment/base URL
-   Test data


