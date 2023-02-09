[[_TOC_]]

## Overview

The test strategy for this solution involves the requirements for load testing the solution as well as test integration with Azure Dev Ops.

Testing will be carried out by the Azure Load Testing service which provides the following features:

- Fully managed service - provides central location to view and manage load tests and results
- Optimize application performance, scalability, and capacity
- Provides detailed metrics to determine performance bottlenecks
- Allows integration within CI/CD workflows
- Utilizes Key Vault for storing secret parameters

### Azure Load Testing Components

Azure Load Testing Service consists of the following components:

- Test - A test specifies the test script, and configuration settings for running a load test
- Test Engine - A test engine is computing infrastructure, managed by Microsoft, that runs the Apache JMeter test script
- Test Run - A test run represents one execution of a load test
- App Component - When you run a load test for an Azure-hosted application, you can monitor resource metrics for the different Azure application components
- Metric Analysis - During a load test, Azure Load Testing collects metrics about the test execution

![azureloadtestingarchitecture](/Integration-Services/.attachments/azure-load-testing-architecture-b51db126-b6f7-4044-9222-cd6d391e3dd0.png)

### Creating Tests

There are two primary approaches to creating load tests. The first is a quick test using a web application URL.

Quick tests are used to load test a single endpoint and can be created through the web UI.

- In the Azure portal, and go to your Azure Load Testing resource.
- Select Tests in the left pane, select + Create, and then select Create a quick test.
- Enter the URL and load parameters.

![createquicktest](/Integration-Services/.attachments/create-quick-test-5560ab23-c0ac-41a4-bc0f-198ec3cccb7f.png)

The second approach is to use a JMeter script. This method enables reusing JMeter scripts and allows for more advanced testing. Tests are created by uploaded a JMX file.

- In the Azure portal, and go to your Azure Load Testing resource.
- Select Tests in the left pane, select + Create, and then select Upload a JMeter script.
- On the Basics page, enter the basic test information.

By selecting Run test after creation, the test will start automatically. You can start your test manually at any time, after creating it.

![createjmetertest](/Integration-Services/.attachments/create-jmeter-test-fa75b2de-cbc7-41b0-90c1-91460e16b0b1.png)

### Test Plans

The test plan contains all files that are needed for running your load test. At a minimum, the test plan should contain one *.jmx JMeter script. Azure Load Testing only supports one JMX file per load test. In addition, you can include a user property file, configuration files, or input data files.

To upload tests to a test plan, navigate to the Test Plan and select all local tests to upload them to Azure.

![testplanuploadfiles](/Integration-Services/.attachments/test-plan-upload-files-210b69b6-7cf4-4cac-8ee4-641fa87ff0db.png)

### Parameters

Parameters are used to make test plans configurable. Here you can specify key-value pairs and reference their value in the JMeter script by using the parameter name.

There are two types of parameters: environmental variables and secrets.

![configureparameters](/Integration-Services/.attachments/configure-parameters-26ce2a55-ec80-48ba-94d9-3125b4f264cf.png)

For more information regarding setting up parameters for environmental variables and Key Vault secrets, see [Parameterize a load test with environment variables and secrets](https://docs.microsoft.com/en-us/azure/load-testing/how-to-parameterize-load-tests).

### Load

Under the Load section is where configuration for the number of virtual users for the JMeter script and the engines run the script in parallel.

![configuretestengineinstances](/Integration-Services/.attachments/configure-test-engine-instances-3ca6f967-88d7-4c95-8f5f-b43db4a9e7f6.png)

### Test Criteria

Under the Test Criteria section, you may specify load test failure criteria. This criteria is based on client metrics and when a test surpasses the set threshold the test will be set to a Failed status.

The client metrics that can be used are Average Response Time and Error Percentage.

![configuretestcriteria](/Integration-Services/.attachments/configure-test-criteria-ce4973cb-e78d-44d0-821c-82ce51773032.png)

### Monitoring

Azure Load Testing can capture detailed resource metrics for the Azure app components which can be used to identify performance bottlenecks.

When editing a load test, select an App component to monitor. Azure Load Testing selects the most relevant resource metrics, but other resource metrics can be added or removed at any time.

When a load test completes, the test result dashboard displays a graph detailing the performance for every App component and resource metric.

![testresultdashboard](/Integration-Services/.attachments/test-result-dashboard-6ab4a64e-7abd-4041-aef8-44f3f8408fb2.png)
