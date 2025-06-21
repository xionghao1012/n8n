# Testing Framework | n8n-io/n8n | DeepWiki

This page documents n8n's comprehensive testing infrastructure, including end-to-end (E2E) testing with Cypress, unit testing with Jest, integration testing, and database compatibility testing. The testing framework ensures code quality, prevents regressions, and validates functionality across different environments and database engines.

## Relevant Source Files

* [.github/scripts/bump-versions.mjs](https://github.com/xionghao1012/n8n/blob/master/.github/scripts/bump-versions.mjs)
* [.github/scripts/package.json](https://github.com/xionghao1012/n8n/blob/master/.github/scripts/package.json)
* [.github/scripts/update-changelog.mjs](https://github.com/xionghao1012/n8n/blob/master/.github/scripts/update-changelog.mjs)
* [.github/workflows/check-documentation-urls.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/check-documentation-urls.yml)
* [.github/workflows/check-pr-title.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/check-pr-title.yml)
* [.github/workflows/check-run-eligibility.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/check-run-eligibility.yml)
* [.github/workflows/chromatic.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/chromatic.yml)
* [.github/workflows/ci-master.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/ci-master.yml)
* [.github/workflows/ci-postgres-mysql.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/ci-postgres-mysql.yml)
* [.github/workflows/ci-pull-requests.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/ci-pull-requests.yml)
* [.github/workflows/docker-base-image.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/docker-base-image.yml)
* [.github/workflows/docker-images-nightly.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/docker-images-nightly.yml)
* [.github/workflows/e2e-reusable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/e2e-reusable.yml)
* [.github/workflows/e2e-tests-pr.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/e2e-tests-pr.yml)
* [.github/workflows/e2e-tests.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/e2e-tests.yml)
* [.github/workflows/linting-reusable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/linting-reusable.yml)
* [.github/workflows/release-create-pr.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/release-create-pr.yml)
* [.github/workflows/release-publish.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/release-publish.yml)
* [.github/workflows/release-push-to-channel.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/release-push-to-channel.yml)
* [.github/workflows/security-trivy-s scan-callable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/security-trivy-scan-callable.yml)
* [.github/workflows/test-workflows-nightly.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/test-workflows-nightly.yml)
* [.github/workflows/test-workflows-pr-approved.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/test-workflows-pr-approved.yml)
* [.github/workflows/test-workflows-pr-comment.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/test-workflows-pr-comment.yml)
* [.github/workflows/units-tests-reusable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/units-tests-reusable.yml)
* [CONTRIBUTING.md](https://github.com/xionghao1012/n8n/blob/master/CONTRIBUTING.md)
* [cypress/constants.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/constants.ts)
* [cypress/e2e/10-undo-redo.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/10-undo-redo.cy.ts)
* [cypress/e2e/11-inline-expression-editor.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/11-inline-expression-editor.cy.ts)
* [cypress/e2e/12-canvas-actions.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/12-canvas-actions.cy.ts)
* [cypress/e2e/12-canvas.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/12-canvas.cy.ts)
* [cypress/e2e/13-pinning.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/13-pinning.cy.ts)
* [cypress/e2e/14-data-transformation-expressions.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/14-data-transformation-expressions.cy.ts)
* [cypress/e2e/14-mapping.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/14-mapping.cy.ts)
* [cypress/e2e/15-scheduler-node.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/15-scheduler-node.cy.ts)
* [cypress/e2e/16-webhook-node.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/16-webhook-node.cy.ts)
* [cypress/e2e/41-editors.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/41-editors.cy.ts)
* [cypress/e2e/5-ndv.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/5-ndv.cy.ts)
* [cypress/e2e/6-code-node.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/6-code-node.cy.ts)
* [cypress/e2e/7-workflow-actions.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/7-workflow-actions.cy.ts)
* [cypress/e2e/8-http-request-node.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/8-http-request-node.cy.ts)
* [cypress/e2e/9-expression-editor-modal.cy.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/e2e/9-expression-editor-modal.cy.ts)
* [cypress/pages/ndv.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/ndv.ts)
* [cypress/pages/workflow.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/pages/workflow.ts)
* [cypress/support/commands.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/support/commands.ts)
* [cypress/support/e2e.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/support/e2e.ts)
* [cypress/support/index.ts](https://github.com/xionghao1012/n8n/blob/master/cypress/support/index.ts)

## Testing Strategy Overview

n8n employs a multi-layered testing approach that includes end-to-end tests, unit tests, integration tests, and database compatibility tests. The testing framework is built around modern tools and follows industry best practices for maintainability and reliability.

### Test Types and Coverage

| Test Type | Framework | Purpose | Location |
| --- | --- | --- | --- |
| E2E Tests | Cypress | User workflow validation | `cypress/e2e/` |
| Unit Tests | Jest | Component/function testing | Various `*.test.ts` files |
| Integration Tests | Jest | API and service testing | `packages/cli/test/integration/` |
| Database Tests | Jest | Multi-database compatibility | Database-specific test suites |

## Cypress E2E Testing Framework

The E2E testing framework uses Cypress to simulate real user interactions and validate complete workflows. Tests are organized using the Page Object pattern for maintainability and reusability.

### Core Page Objects

The testing framework implements the Page Object pattern with several key classes:

* **NDV (Node Details View)**: Provides comprehensive testing utilities for node interaction
* **WorkflowPage**: Handles canvas-level operations and workflow management

### Key Test Components

The `NDV` class provides:

* **Parameter Input Testing**: Methods for form validation
* **Execution Testing**: Workflow execution validation
* **Data Validation**: Data flow testing
* **Expression Testing**: Expression validation

The `WorkflowPage` class handles:

* **Node Management**: Adding, deleting, duplicating nodes
* **Workflow Operations**: Saving, executing, activating workflows
* **Canvas Interaction**: Zooming, selecting, drag and drop operations

### Test Execution and Support

The support system provides essential testing utilities:

* **Authentication Commands**: Role-based testing
* **Workflow Management**: Loading test workflows from JSON fixtures
* **Custom Interactions**: Complex UI interactions
* **Database Reset**: Clean test state between runs

## CI/CD Testing Pipeline

The testing pipeline is implemented through GitHub Actions workflows that run different test suites based on triggers and conditions.

### Test Parallelization and Distribution

The E2E testing framework supports parallel execution across multiple containers:

* **Container Matrix**: Tests can run across up to 15 parallel containers
* **Spec Distribution**: Individual test specs are distributed across containers
* **Cypress Dashboard**: Integration for test recording and parallel coordination
* **Unique Build IDs**: Each test run gets a unique identifier

## Database Compatibility Testing

n8n supports multiple database engines, and the testing framework validates compatibility across all supported databases.

### Database Test Matrix

Each database engine has specific test configurations:

* **SQLite Pooled**: Tests connection pooling
* **PostgreSQL**: Tests with minimal pool size to detect deadlocks
* **MySQL Variants**: Tests multiple MySQL versions for compatibility
* **MariaDB**: Validates MariaDB-specific behavior and compatibility

The database tests run with extended timeouts to accommodate slower database operations and container startup times.

## Unit and Integration Testing

The unit testing framework uses Jest and covers both frontend and backend components with comprehensive test suites.

### Test Execution and Coverage

The unit testing system provides:

* **Backend Testing**: Runs all backend-related tests
* **Node Testing**: Executes node-specific test suites
* **Frontend Testing**: Validates UI components and interactions
* **Coverage Collection**: Configurable coverage tracking
* **Codecov Integration**: Automatic upload of test results and coverage data

The testing framework supports multiple Node.js versions with version 22.x being the primary version for coverage collection.

## Test Data and Fixtures

The testing framework uses a comprehensive fixture system for consistent test data and workflow definitions.

### Fixture Organization

Test fixtures are organized by functionality and provide realistic test scenarios:

* **Workflow Fixtures**: JSON files containing complete workflow definitions
* **Node Configuration**: Pre-configured node setups
* **Test Data**: Sample input/output data
* **Binary Test Files**: Support for testing file uploads and binary data handling

The `createFixtureWorkflow()` command loads workflows from the fixtures directory and automatically sets up the test environment.

### Test Environment Management

The test environment management ensures:

* **Clean State**: Each test starts with a fresh database state
* **Proper Authentication**: Role-based authentication
* **Network Handling**: Consistent handling of API calls and loading states
* **Error Handling**: Graceful handling of console errors and uncaught exceptions