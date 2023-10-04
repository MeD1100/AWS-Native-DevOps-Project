In order to apply the ecs-ec2-with-cf.yml file, we need to execute this command to both files correspondingly:

```aws cloudformation create-stack --capabilities CAPABILITY_IAM --stack-name stack_name --template-body file://./file_name```
  
