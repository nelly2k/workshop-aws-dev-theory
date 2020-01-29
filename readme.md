
https://docs.aws.amazon.com/lambda/latest/dg/build-pipeline.html
1. Create role so CloudFormation template can be executed
- Trusted entity – AWS CloudFormation
- Permissions – AWSLambdaExecute
- Role name – cfn-lambda-pipeline

```json
{
    "Statement": [
        {
            "Action": [
                "apigateway:*",
                "codedeploy:*",
                "lambda:*",
                "cloudformation:CreateChangeSet",
                "iam:GetRole",
                "iam:CreateRole",
                "iam:DeleteRole",
                "iam:PutRolePolicy",
                "iam:AttachRolePolicy",
                "iam:DeleteRolePolicy",
                "iam:DetachRolePolicy",
                "iam:PassRole",
                "s3:GetObject",
                "s3:GetObjectVersion",
                "s3:GetBucketVersioning"
            ],
            "Resource": "*",
            "Effect": "Allow"
        }
    ],
    "Version": "2012-10-17"
}
```
2. Setup repository 
In order to obtain credentials for git go to IAM -> Users-> User-> Security Credentials tab -> HTTPS Git credentials for AWS CodeCommit

<details><summary>How to obtain git credentials</summary>
![Git credentials](./img/git-credentials.jpg)


</details>
```  aws2 codecommit create-repository --repository-name nelli-playing-with-ci```


3. Create lambda 

4. Create CloudFormation template
5. Create s3 bucket for artefacts ```aws s3 mb s3://lambda-deployment-artifacts-123456789012```
5. add build spec
