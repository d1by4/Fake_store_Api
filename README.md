# Fake Store API Testing with Postman

This repository contains a Postman collection for testing product endpoints of the [Fake Store API](https://fakestoreapi.com/). It demonstrates basic positive testing, negative testing, response validation, and creation of test data through REST API requests.

## Project Overview

The collection currently covers the following operations:

| Request | Method | Endpoint | Validation |
| --- | --- | --- | --- |
| Get products | `GET` | `/products` | Verifies status `200` and confirms that the response body is an array |
| Product not found | `GET` | `/products/9999` | Verifies status `404` for a product that does not exist |
| Create new product | `POST` | `/products` | Sends valid product data to create a new product |

## Tools and Technologies

- Postman
- JavaScript test scripts
- REST API
- JSON

## Collection Structure

```text
Fake store Api
├── get product
├── failed product id
└── create new product
```

## Prerequisites

Before running the collection, install one of the following:

- [Postman Desktop](https://www.postman.com/downloads/)
- Newman for command-line execution

To install Newman globally:

```bash
npm install -g newman
```

## Setup

1. Clone or download this repository.
2. Open Postman.
3. Select **Import** and choose `Fake store Api.postman_collection.json`.
4. Open the imported collection and select the **Variables** tab.
5. Set both the initial and current values of `FakebaseUrl` to:

```text
https://fakestoreapi.com
```

6. Save the collection.

## Running the Tests in Postman

1. Open the **Fake store Api** collection.
2. Click **Run collection**.
3. Select the requests that you want to execute.
4. Click **Run Fake store Api**.
5. Review the request status, response body, and test results in the Collection Runner.

## Running the Tests with Newman

After installing Newman, run:

```bash
newman run "Fake store Api.postman_collection.json" \
  --env-var "FakebaseUrl=https://fakestoreapi.com"
```

## Automated Assertions

### Get products

The request verifies that:

- The HTTP response status is `200 OK`.
- The response body is an array.

```javascript
pm.test("Status 200 and response is array", function () {
    pm.response.to.have.status(200);
    pm.expect(pm.response.json()).to.be.an("array");
});
```

### Product not found

The negative test verifies that the API returns `404 Not Found` when the requested product does not exist.

```javascript
pm.test("Product not found", function () {
    pm.response.to.have.status(404);
});
```

### Create new product

The request sends the following sample payload:

```json
{
  "title": "QA Test Product",
  "price": 99.99,
  "description": "Created using Postman",
  "image": "https://i.pravatar.cc",
  "category": "electronics"
}
```

This request currently demonstrates sending a valid POST request. Automated assertions for its status code and response schema have not yet been added.

## Current Test Coverage

- Positive testing for retrieving product data
- Negative testing using a non-existent product ID
- HTTP status-code validation
- Response data-type validation
- Valid JSON request-body testing

## Planned Improvements

- Add assertions for the create-product response.
- Validate required response properties and their data types.
- Add tests for retrieving a product by a valid ID.
- Add update and delete product scenarios.
- Add response-time assertions.
- Add an environment file without sensitive data.
- Integrate Newman execution with GitHub Actions.

## Notes

- This project is a QA portfolio exercise using a public practice API.
- The collection variable `FakebaseUrl` must be configured before execution.
- Fake Store API may simulate write operations; created, updated, or deleted data may not persist permanently.

## Author

**I Kadek Dibya Wardhana Dinata**  
Software Quality Assurance Engineer  
[GitHub](https://github.com/d1by4)
