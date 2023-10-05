#Instructions

In order to apply the two cloudformation files, we need to execute these commands to both files:

```aws configure set region us-east-1```

```aws cloudformation create-stack --capabilities CAPABILITY_IAM --stack-name stack_name --template-body file://./file_name```


ecs-ec2-with-cf.yml:
- ec2
- ecs
- sg
- asg
- container instances
- ecs instance role

core-infrastructure-setup.yml:
- VPC
- 2 subnets in 2 different AZs
- Internet Gateway (IGW)
- route tables
  
#Policies and roles

Create a policy called codeBuildBatchPolicy and attach the following permissions to the codeBuildServiceRole IAM role
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Resource": [
                "arn:aws:codebuild:us-east-1:<your_account_number>:project/simplehttp-cb"
            ],
            "Action": [
                "codebuild:StartBuild",
                "codebuild:StopBuild",
                "codebuild:RetryBuild"
            ]
        }
    ]
}
```

Create a policy called codeBuildServiceRolePolicy and attach the following permissions to the codeBuildServiceRole IAM role
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ecr:GetDownloadUrlForLayer",
                "ecr:GetAuthorizationToken",
                "codecommit:GitPull",
                "s3:GetBucketAcl",
                "logs:CreateLogGroup",
                "logs:PutLogEvents",
                "s3:PutObject",
                "s3:GetObject",
                "logs:CreateLogStream",
                "ecr:BatchGetImage",
                "s3:GetBucketLocation",
                "s3:GetObjectVersion",
                "ecr:BatchCheckLayerAvailability"
            ],
            "Resource": "*"
        }
    ]
}
```

Finally attach a policy called AmazonEC2ContainerRegistryPowerUser to codeBuildServiceRole IAM role