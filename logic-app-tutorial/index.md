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


  ###### [Site Root](https://linuxlsr.github.io)