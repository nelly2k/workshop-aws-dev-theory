
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
## Repository
In order to obtain credentials for git go to IAM -> Users-> User-> Security Credentials tab -> HTTPS Git credentials for AWS CodeCommit
![Git credentials](./img/git-credentials.jpg)


You can create repository using CLI

```cmd 
aws codecommit create-repository --repository-name nelli-playing-with-ci
```
The output give you clone link

or

Console -> Developer Tools -> CodeCommit -> Source -> Repositories -> Create -> Repository

## Code
### Create lambda
create index.js and paste code 
```javascript
exports.handler = async (event) => {
    const response = {
        statusCode: 200,
        body: JSON.stringify('Hello from Lambda2!'),
    };
    return response;
};
```

### Create CloudFormation template
create buildSpec.yaml

```yaml
Description: Dev Theory Workshop
Resources:
  my-lambda:
      Type: AWS::Lambda::Function
      Properties: 
        Handler: index.handler
        Runtime: nodejs12.x
        Code: ./my-lambda/
```

### Artefact storage
Create s3 bucket for artefacts 

```aws s3 mb s3://lambda-deployment-artifacts-123456789012```

5. add build spec
