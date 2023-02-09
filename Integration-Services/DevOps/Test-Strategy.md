[[_TOC_]]

## Overview

The test strategy for this solution involves testing both infrastructure deployment and application logic both in a manual and automated fashion.

1. [Manual tests](#manual-tests) will be used to validate parts of the system which are tedious or difficult to test in an automated fashion. Azure DevOps test cases will be used to document these and execute them using parameters.

2. [Automated tests](#automated-tests) will validate application logic at various layers, such as L0 for unit tests and L2 & L3 for integration tests.

## Test Strategy

Testing is broken out into various layers provided its difficulty and dependencies.

- L0 - Includes testing at the unit level. This level should include the most number of tests as it's easier to maintain and modify. This level is also part of the build validation. At this level, one is testing code changes by class or method.
- L1 - This level starts integration testing but without any dependencies deployed. This can use self-hosting APIs using test frameworks to test changes. This level is also part of the build validation.
- L2 - This level requires dependencies to be deployed. The tests are smaller sets and more brittle compared to L3. These are automated tests run during deployment before production.
- L3 - This level requires dependencies to be deployed. These are automated tests run during and after deployment to production.

![testpyramid](/.attachments/test-pyramid.png)

### Shift-Left Testing

The goal for shifting left is to move quality upstream by performing testing tasks earlier in the pipeline. A combination of test and process improvements reduces the time for tests to execute and the impact of failures later on. Most importantly, it ensures that most testing is completed even before a change is merged into the main.

![testshiftleft](/.attachments/test-shift-left.png)

### Test Frameworks

1. Microsoft Test Framework ([MSTest](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-mstest)) - Framework used for unit testing C# changes.
2. [Postman](https://www.postman.com/) & [Newman](https://github.com/postmanlabs/newman) - Framework used for integration and automated tests
3. [Azure DevOps Test Cases](https://docs.microsoft.com/en-us/azure/devops/test/create-test-cases?view=azure-devops) - Framework used for documenting tests and building manual tests.

## Department Specific Tests

Various tests will be created to support testing from an integration standpoint, requests flowing through the system and affecting each department individually.

1. Authentication - Will validate that a provider only has access to the approved APIs and content. Create a department-specific test provider to automate sending authenticated requests and validate that data was sent to the correct FHIR store.
2. Business logic - Execute unit tests associated with each department's set of NuGet packages with each pull request validating each department's collection of business logic.

## Manual Tests

Azure DevOps Test Cases will be used to set up manual tests. These are tests that are too time-consuming or difficult to automate, such as validating infrastructure. A test plan for each area of the infrastructure is set up, and individual test cases given various scenarios are added.

1. Logging - Logging - Validates that logging is configured at the application and infrastructure level. Logs should be sent as API requests are made, and diagnostics should be configured for each service.
2. API Management - Validates that the expected API endpoints are configured in Azure API Management with their respective policies.
3. FHIR Service - Validates that the expected FHIR API is deployed to each department's resource group and appropriately named.

![testmanualrun](/.attachments/test-manual-run.png)

### Manual Test Parameters

Test parameters are associated with manual tests to repeat the test for a different environment. This spreadsheet-style configuration will list the Azure configuration expected across Dev, QA, and Production.

![testmanualparams](/.attachments/test-manual-params.png)

## Automated Tests

There are various types of automated tests ranging from L0 to L3. The lower in the pyramid, the more tests will be included.

### Build Validation

Branch policy will be configured on the `main` branch requiring PR changes to build successfully before the PR can complete. This will help reduce breaks and keep test results passing. This policy will queue a new build when a new PR is created, or changes are pushed to an existing PR that targets the branch.

#### Build Validation Settings

- Will trigger automatically
- The Build must succeed in order to complete pull requests
- The Build expires immediately when the `main` branch is updated

![testbuildvalsetup](/.attachments/test-build-validationsetup.png)

#### Validation Results

Results are displayed on each Pull request showing whether the tests passed or failed.

![testbuildvalresult](/.attachments/test-build-validation-result.png)

#### Code Coverage

Code coverage will be a metric tracked to help measure the percentage of the code being tested. This will help ensure that the quality of the project improves over time. Code coverage will be assessed during a pull request as part of the build validation pipeline and only pertains to changes to code. It does not track untouched code.

![testcc](/.attachments/test-build-validationsetup.png)

### Unit Tests

Unit tests are C# coded tests using MS Test framework and NSubstitute mock framework. These are added to a test project following the name of the project being tested and ending in `.UnitTests`. Tests will be created for every change to the application logic.

### Integration Tests

Integration tests will use Postman collections and Newman CLI for automation.

These tests will be run after deployment to a slot and after the slot is swapped with the live one allowing for a Blue-Green deployment. This will enable one to test changes before swapping and after.

#### Blue/Green Test Steps:

1. Deploy to App Service slot
2. Run tests against staging slot
3. Swap slot
4. Run tests against live slot

### Security Tests

Various types of security tests should run at multiple stages in the devops process. This verification phase involves a comprehensive effort to ensure that the code meets the security and privacy tenents.

1. Application Dependencies - This step is done in the compilation stage to scan and esnure the application and it's dependent libraries are clear of any known vulnerable components.

2. Penetration Testing

#### Find and fix vulnerabilities  in application depdendencies

1. [OWASP Dependency Check](https://owasp.org/www-project-dependency-check/) - Should run during a Pull Request or as a scheduled pipeline in order to detect publicly disclosed vulnerabilities. The Azure DevOps [extension](https://marketplace.visualstudio.com/items?itemName=dependency-check.dependencycheck) will be used to support this check.

#### Perform security penetration testing

ZAP will be leveraged after deployment to development in order to run penetration test and help find vulnerabilities in API endpoints exposed. Penetration testing via [OWAS Zap](https://www.zaproxy.org/getting-started/). The Azure DevOps [extension](https://marketplace.visualstudio.com/items?itemName=CSE-DevOps.zap-scanner) can be used to support this check.

Vulnerabilties assessed:

- Cross-site scripting
- SQL injection
- Broken Authentication
- Sensitive data exposure
- Broken Access control
- Security misconfiguration
- Insecure Deserialization
