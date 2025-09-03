# AWS CodeDeploy

## AWS Doc

### Tutorial

{% embed url="https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorials-github-create-application.html" %}

## Definition

CodeDeploy works by managing the process of getting your application code from a repository to its final destination. A typical deployment process involves the following components:&#x20;

* **Application**: The container for the entire deployment process, which manages the relationship between a set of code, the deployment settings, and the deployment environment.
* **Revision**: The specific version of your deployable code and related files, such as scripts and configuration. Revisions can be stored in an Amazon S3 bucket, a GitHub repository, or a Bitbucket repository.
* **Deployment Group:** The set of target instances or compute services for your deployment. These can be Amazon EC2 instances, on-premises servers, Amazon ECS services, or AWS Lambda functions.
  * **AppSpec** file: A YAML or JSON formatted file included with your application revision that specifies the deployment actions. It defines which files to copy and what scripts to run at different stages of the deployment lifecycle.
  * **Deployment Configuration**: Defines the rules and conditions for a deployment, such as how to handle failures or ensure a minimum number of healthy instances.&#x20;
