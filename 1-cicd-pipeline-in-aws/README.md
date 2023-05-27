# CI/CD pipeline in AWS

> **Continuous Integration (CI)** - *The developer will push their code to a central repository. A build/test server will then pick up the code and startup builds and tests. The developer then gets feedback regarding the succeeded/failed builds and tests.* This complete process is called Continuous Integration.

> **Continuous Delivery (CD)** - *If all the builds and tests have succeeded in the CI process, the builds can then be deployed (to application servers) by a deployment server.* This complete process is called Continuous Delivery.

![AWS CI/CD Pipeline](./media/aws-cicd-pipeline.png)

## AWS CodeCommit

AWS CodeCommit is a **Version Control System** (VCS like Github, Gitlab, BitBucket etc.) as a service offered by AWS. Features of AWS CodeCommit -

- Repositories can be scaled seamlessly as there is **no size limit**.
- Sourcecode in a repository **can be automatically encrypted using AWS KMS**.
- We can **leverage AWS IAM to configure access control to the repository** (We can enable cross AWS account access using AWS IAM and STS). Developers who have access, then **can connect to the CodeCommit repository using secure protocols like HTTPS (username and passed based) or SSH (SSH key based)**.
- CodeCommit **supports integration with CI tools** like Jenkins, AWS CodeBuild etc.
- It is a highly available service, completely managed by AWS.
- On any specific type of event happening in a CodeCommit repository -
    - *the notification can be collected in an AWS SNS topic.*
    - *an AWS Lambda function can be triggered.*
    - *an AWS CodePipeline managed CI/CD pipeline can be triggered.*
    
    **A CodeCommit repository can be integrated with AWS EventBridge**.
    
**Branch protection and Pull Request Approval Rules can be created using IAM policies.** (Also, AWS has created templates for  Pull Request Approval Rules)

Taking **backups** of a CodeCommit repository -
> Here AWS Lambda is used as an intermediate instead of AWS EventBridge, because to clone/update the CodeCommit repository, we need to know details about the commits. Notifications sent to AWS EventBridge doesn’t contain that.

![Untitled](./media/backup-codecommit-repository.png)

## AWS CodePipeline