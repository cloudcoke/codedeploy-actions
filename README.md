# ECS deploy with CodeDeploy

# Usage

```yaml
- uses: cloudcoke/codedeploy-ecs@v1
  with:
      # AWS IAM access key to use
      aws-access-key-id: ""

      # AWS IAM access secret key to use
      aws-secret-access-key: ""

      # Which AWS region to use
      # Default: ap-northeast-2
      aws-region: ""

      # Name of CodeDeploy app to use
      codedeploy-app-name: ""

      # Name of CodeDeploy group to use
      codedeploy-group-name: ""

      # Name of Amazon S3 bucket with revision
      codedeploy-bucket-name: ""

      # Name of the uploaded revision
      codedeploy-bucket-key: ""

      # Type of the uploaded revision
      # Default: YAML
      # For example: YAML|JSON
      codedeploy-bucket-type: ""
```

# Examples

## Default Deploy

```yaml
name: Deploy CodeDeploy

on:
    push:
        branches: main

jobs:
    deploy:
        runs-on: ubuntu-latest
        steps:
            - name: Deploy CodeDeploy
              uses: cloudcoke/codedeploy-ecs@v1
              with:
                  aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
                  aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
                  codedeploy-app-name: ${{ secrets.CODEDEPLOY_APP_NAME }}
                  codedeploy-group-name: ${{ secrets.CODEDEPLOY_GROUP_NAME }}
                  codedeploy-bucket-name: ${{ secrets.CODEDEPLOY_BUCKET_NAME }}
                  codedeploy-bucket-key: ${{ secrets.CODEDEPLOY_BUCKET_KEY }}
```

# Required IAM Permissions

```json
{
    "Statement": [
        {
            "Action": [
                "s3:PutObject",
                "codedeploy:RegisterApplicationRevision",
                "codedeploy:ListDeployments",
                "codedeploy:GetDeploymentConfig",
                "codedeploy:GetDeployment",
                "codedeploy:GetApplicationRevision",
                "codedeploy:CreateDeployment"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ],
    "Version": "2012-10-17"
}
```
