# SauceDemo Playwright Automation

End-to-end UI automation framework built with **Playwright** and **TypeScript** for the SauceDemo application, with additional API automation practice using JSONPlaceholder.

---

## Overview

This is an automation testing project built using Playwright and TypeScript.

The main UI automation suite tests the **SauceDemo** web application and demonstrates hands-on experience in designing and maintaining a structured automation framework using the **Page Object Model (POM)**.

The project includes reusable page objects, custom fixtures, centralized test data, parameterized tests, hooks, UI validations, and end-to-end test scenarios across major SauceDemo modules.

The project also contains an **API automation suite using JSONPlaceholder** to practice REST API testing with Playwright, including GET, POST, PUT, PATCH, DELETE, query parameters, response validation, and negative testing.

The UI suite runs across **Chromium, Firefox, and WebKit**, while API tests run separately through a dedicated Playwright API project.

The framework also includes HTML reporting, screenshots, videos, traces for failed or retried tests, and CI integration through **GitHub Actions**.

---

## Tech Stack

| Technology      | Purpose                                             |
| --------------- | --------------------------------------------------- |
| Playwright      | UI and API automation and test execution            |
| TypeScript      | Automation framework development                    |
| Node.js         | JavaScript runtime environment                      |
| Git             | Source control                                      |
| GitHub          | Repository hosting and version control              |
| GitHub Actions  | Continuous Integration and automated test execution |
| HTML Reporter   | Test execution reporting                            |
| Trace Viewer    | Test debugging and analysis                         |
| JSONPlaceholder | Public REST API used for API automation practice    |

---

## Application Under Test

### UI Testing

**SauceDemo**

The UI automation suite currently covers:

- Login
- Products
- Product Details
- Shopping Cart
- Checkout

### API Testing

**JSONPlaceholder**

JSONPlaceholder is used separately from SauceDemo for REST API automation practice.

The API suite currently covers:

- GET single resource
- POST create resource
- PUT full resource update
- PATCH partial resource update
- DELETE resource
- GET requests with query parameters
- Response status validation
- Response body validation
- Data type validation
- Array validation
- Negative testing using `404 Not Found`

---

## Project Structure

The UI automation framework follows the **Page Object Model (POM)** design pattern to separate test logic from page-specific locators and actions.

This improves maintainability, reduces duplicated code, and allows reusable methods to be shared across multiple test scenarios.

```text
saucedemo-playwright/
│
├── .github/
│   └── workflows/
│       └── playwright.yml        # GitHub Actions CI workflow
│
├── fixtures/
│   └── pages.fixture.ts          # Custom fixtures for initializing Page Objects
│
├── pages/
│   ├── LoginPage.ts              # Login page locators, actions, and validations
│   ├── ProductPage.ts            # Products page functionality
│   ├── ProductDetailsPage.ts     # Product details functionality
│   ├── CartPage.ts               # Shopping cart functionality
│   └── CheckoutPage.ts           # Checkout workflow functionality
│
├── test-data/
│   ├── users.ts                  # User credentials and checkout information
│   ├── products.ts               # Product information and sorting data
│   ├── productdetail.ts          # Product details test data
│   ├── checkouts.ts              # Checkout validation data
│   └── login.ts                  # Login validation data
│
├── tests/
│   ├── ui/
│   │   ├── login.spec.ts         # Login test scenarios
│   │   ├── product.spec.ts       # Product page test scenarios
│   │   ├── productdetail.spec.ts # Product details test scenarios
│   │   ├── cart.spec.ts          # Shopping cart test scenarios
│   │   └── checkout.spec.ts      # Checkout test scenarios
│   │
│   └── api/
│       └── post.spec.ts          # JSONPlaceholder API test scenarios
│
├── playwright.config.ts          # Playwright configuration
├── package.json                  # Dependencies, npm scripts, and Node configuration
├── package-lock.json             # Locked dependency versions
└── .gitignore                    # Files excluded from Git tracking
```

---

## Installation & Setup

### Prerequisites

Before running the project, make sure the following are installed:

- Node.js 24.x
- npm
- Git

### 1. Clone the Repository

```bash
git clone https://github.com/KingChard/saucedemo-playwright.git
cd saucedemo-playwright
```

### 2. Install Dependencies

```bash
npm ci
```

### 3. Install Playwright Browsers

```bash
npx playwright install
```

For Linux or CI environments:

```bash
npx playwright install --with-deps
```

---

## Playwright Projects

The framework separates UI and API execution through Playwright projects.

| Project  | Test Scope     |
| -------- | -------------- |
| Chromium | UI tests       |
| Firefox  | UI tests       |
| WebKit   | UI tests       |
| API      | API tests only |

UI tests are executed across the three major browser engines, while API tests run only once because they use Playwright's `request` fixture and do not require a browser.

---

## Running the Tests

### Run the Complete Test Suite

```bash
npm test
```

This runs:

```text
UI Tests
├── Chromium
├── Firefox
└── WebKit

API Tests
└── API project
```

### Run UI Tests Only

```bash
npm run test:ui
```

### Run API Tests Only

```bash
npm run test:api
```

### Run a Specific UI Test

Example:

```bash
npm run test:ui -- -g "CHK-001"
```

### Run a Specific API Test

Example:

```bash
npm run test:api -- -g "API-007"
```

### Run UI Tests in Headed Mode

```bash
npm run test:ui -- --headed
```

### Run a Specific UI Test in Headed Mode

```bash
npm run test:ui -- -g "CHK-001" --headed
```

> `--headed` is primarily useful for UI tests because API tests do not require a visible browser window.

### Open the HTML Report

```bash
npm run report
```

---

## API Testing

The API automation suite uses Playwright's built-in `request` fixture to send and validate HTTP requests against **JSONPlaceholder**.

The API tests are separate from the SauceDemo UI tests because SauceDemo does not provide the REST endpoints used in this practice suite.

### API Test Coverage

| Test ID | Method | Scenario                              |
| ------- | ------ | ------------------------------------- |
| API-001 | GET    | Retrieve a single post                |
| API-002 | POST   | Create a new post                     |
| API-003 | PUT    | Update an existing post               |
| API-004 | PATCH  | Partially update a post               |
| API-005 | DELETE | Delete a post                         |
| API-006 | GET    | Retrieve posts using query parameters |
| API-007 | GET    | Validate `404` for a nonexistent post |

### API Concepts Practiced

- REST HTTP methods
- Request payloads
- Query parameters
- Dynamic endpoint values
- JSON response parsing
- HTTP status code validation
- Response property validation
- Data type validation
- Array validation
- Collection filtering validation
- Positive testing
- Negative testing

---

## Current Framework Capabilities

- Page Object Model
- Custom Playwright fixtures
- Centralized test data
- Parameterized testing
- Playwright hooks
- Reusable locators and page methods
- End-to-end UI testing
- Cross-browser UI testing using Chromium, Firefox, and WebKit
- Dedicated API test project
- API tests execute independently from browser projects
- REST API automation
- Positive and negative API testing
- Query parameter validation
- Request and response validation
- HTML test reporting
- Screenshots on test failure
- Video retention on test failure
- Playwright traces on retry
- Separate UI and API test execution
- GitHub Actions CI integration
- Automated execution on pushes and pull requests to `main`

---

## Available npm Scripts

| Command            | Purpose                                           |
| ------------------ | ------------------------------------------------- |
| `npm test`         | Run the complete UI and API test suite            |
| `npm run test:ui`  | Run UI tests across Chromium, Firefox, and WebKit |
| `npm run test:api` | Run API tests once using the API project          |
| `npm run report`   | Open the Playwright HTML report                   |

---
