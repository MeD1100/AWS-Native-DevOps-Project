#Instructions

In order to apply the ecs-ec2-with-cf.yml file, we need to execute this command to both files correspondingly:

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
  
