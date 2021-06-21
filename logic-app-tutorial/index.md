# Design & Deploy an Azure Logic App using Terraform and Azure Devops

This tutorial is intended to outline a process where you can deploy a piece of serverless technology using infrastucture as code and continuous integration / continuous deployment tools.
This logic apps solution with have the following devops practices or gates applied if in __bold__:
1. __source control__
2. branching strategy
3. code coverage
4. static code analysis
5. security analysis
6. __OSS__
7. artifact storage
8. __code deployment__
9. __infrastructure as code__
10. build / unit test
11. behavior driven design / automated test driven design (BDD/ATDD)
12. performance testing
13. automated rollback
14. automated change order
15. zero downtime
16. feature toggle

Tools:
* Azure subscription
* Azure devops account
* github account / code repo
* text editor / IDE

Concepts:
* Logic App: cloud based serverless function that executes a task based on a trigger. There are no servers; once the task is triggered and completed, no further compute resources are used. Billing is based on time it takes the function or app to execute.
* Infrastructure as Code: cloud resources created via a declarative state language, such as terraform. There is no cost for terraform (open source), but the resources it creates may have costs in the cloud. Proceed at your own risk.
* CI/CD: task automation via pipelines. Abstract tasks to patterns, inputs and outputs.

Steps:
1. Design the app
- send text message when object added to storage account
- test in portal logic app designer 
2. portal create app
* Basics:
- resource group
- instance details: consumption / standard
- logic app name (DNS compliant and unique)
- Publish: workflow / docker container
- region
* Hosting:
- storage account
- plan type (workflow standard / app service plan(not supported in my location?))
- windows plan (creates new plan)
- SKU (WS1, WS2, WS3)
* Monitoring:
- Enable App Insights
* Tags:
- Name / Value
* Review + create

It creates windows plan that allocates resources on the "serverfarms"

* New Workflow
- Workflow Name
- State Type (stateful, stateless)
- Edit in designer
* add trigger: Azure Blob
- create connection
- connection name
- blob storage connection string

##### References

- [Choosing between Azure Logic Apps and Azure Functions](https://walkerscott.co/2020/03/azure-logic-apps-vs-azure-functions/)
- [10 Differences between Azure Functions and Logic Apps](https://www.codit.eu/blog/10-differences-between-azure-functions-and-logic-apps/)
- [Pluralsight: Logic Apps: Getting Started](https://app.pluralsight.com/library/courses/azure-logic-apps-getting-started/table-of-contents)
- [Pluralsight: Creating Enterprise Logic Apps](https://app.pluralsight.com/library/courses/microsoft-azure-enterprise-logic-app-creating/table-of-contents)
- [Pluralsight: Logic Apps: Fundamentals](https://app.pluralsight.com/library/courses/azure-logic-apps-fundamentals/table-of-contents)

  ###### [Site Root](https://linuxlsr.github.io)