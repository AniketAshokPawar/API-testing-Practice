Topic 9: API + UI Combination
-----------------------------

This is a very important real-world automation concept. Instead of performing every setup step through the UI, we use APIs to prepare data quickly and then use the UI to verify the actual user experience.

There are three common workflows:

1.  Create data through API → verify through UI

2.  API setup → UI test

3.  UI action → API validation

1\. Create data through API → verify through UI
===============================================

### Example scenario

Suppose an application has a user-management page.

Normally, to create a user through the UI, we need to:

1.  Open the application.

2.  Navigate to the user page.

3.  Click Add User.

4.  Enter user details.

5.  Click Save.

6.  Search for the user.

This may take several seconds.

Instead, we can create the user through an API and then verify it in the UI.

### Workflow

```
API creates user
        ↓
Open application UI
        ↓
Search for user
        ↓
Verify user is displayed
```

### Example code

```
import { test, expect } from '@playwright/test';

test("Create user through API and verify through UI", async ({ request, page }) => {

    // 1. Create user through API
    const createUserResponse = await request.post(
        'https://api.example.com/users',
        {
            data: {
                name: "Aniket",
                email: "aniket@example.com"
            }
        }
    );

    // 2. Validate API response
    expect(createUserResponse.status()).toBe(201);

    const userBody = await createUserResponse.json();

    // 3. Store created user's name
    const userName = userBody.name;

    // 4. Open application UI
    await page.goto('https://app.example.com');

    // 5. Navigate to users page
    await page.getByText('Users').click();

    // 6. Search for created user
    await page.getByPlaceholder('Search users').fill(userName);

    // 7. Verify user is displayed
    await expect(page.getByText(userName)).toBeVisible();
});
```

### Important point

The API creates the data, but the UI verifies that the data is correctly displayed to the user.

This is useful because:

-   Test execution becomes faster.

-   We avoid repetitive UI setup.

-   We can focus the UI test on the actual functionality being tested.

2\. API setup → UI test
=======================

This is similar to the first workflow, but the API may prepare more complex conditions.

### Example scenario

Suppose we want to test an order page where the user already has an order.

Creating an order through the UI may require many steps:

1.  Login.

2.  Search for a product.

3.  Add product to cart.

4.  Enter address.

5.  Make payment.

6.  Place order.

Instead, we create the order through an API and directly test the order page in the UI.

### Workflow

```
API creates required test data
        ↓
Open UI
        ↓
Navigate directly to required page
        ↓
Verify functionality
```

### Example code

```
import { test, expect } from '@playwright/test';

test("API setup followed by UI validation", async ({ request, page }) => {

    // API setup: create an order
    const orderResponse = await request.post(
        'https://api.example.com/orders',
        {
            data: {
                productId: 101,
                quantity: 2,
                customerId: 10
            }
        }
    );

    expect(orderResponse.status()).toBe(201);

    const orderBody = await orderResponse.json();

    const orderId = orderBody.id;

    // UI test: open the order page
    await page.goto(`https://app.example.com/orders/${orderId}`);

    // Verify order details
    await expect(page.getByText(`Order ID: ${orderId}`)).toBeVisible();
    await expect(page.getByText('Quantity: 2')).toBeVisible();
});
```

Here:

```
const orderId = orderBody.id;
```

stores the ID of the newly created order.

Then we use that ID to open the corresponding UI page.

### Why is this useful?

Suppose the application has different order states:

-   Pending

-   Approved

-   Shipped

-   Cancelled

The API can quickly create an order in the required state, and the UI can verify how that state is displayed.

3\. UI action → API validation
==============================

In this workflow, the user performs an action through the UI, and we verify the backend result through an API.

### Example scenario

The user clicks Delete User in the UI.

We need to verify that the user was actually deleted from the backend.

### Workflow

```
Perform action in UI
        ↓
Backend data changes
        ↓
Call API
        ↓
Verify backend result
```

### Example code

```
import { test, expect } from '@playwright/test';

test("Delete user through UI and validate through API", async ({ request, page }) => {

    const userId = 101;

    // 1. Open application
    await page.goto('https://app.example.com');

    // 2. Navigate to users page
    await page.getByText('Users').click();

    // 3. Delete user through UI
    await page.getByText(`User ${userId}`).click();
    await page.getByRole('button', { name: 'Delete' }).click();

    // 4. Confirm deletion
    await page.getByRole('button', { name: 'Confirm' }).click();

    // 5. Validate backend through API
    const response = await request.get(
        `https://api.example.com/users/${userId}`
    );

    // 6. Verify user no longer exists
    expect(response.status()).toBe(404);
});
```

The UI may show a success message, but that alone does not always prove that the backend data was deleted correctly.

The API validation gives us stronger confirmation.


Important difference
====================

### API validation

Checks backend behavior:

```
expect(response.status()).toBe(200);
```

### UI validation

Checks what the user sees:

```
await expect(page.getByText('Order created')).toBeVisible();
```

A complete end-to-end test may validate both.

Interview answer
================

> API and UI combination means using API calls and UI actions together in one test workflow. We can create or prepare test data through APIs and verify it through the UI. We can also perform an action through the UI and validate the resulting backend data through an API. This improves execution speed, reduces repetitive UI steps, and provides better end-to-end coverage.
