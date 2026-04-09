
### CloudFormation

1. Workflow: Writing  a Template --> CF makes a stack --> Run/Delete the stack to Create/Modify/Delete Physical Resources(EC2, VPC subnets, S3 Buckets anything).
2. _Non-portable template_ means values are hardcoded; as opposed to Portable. Example: region names should be under a variable. that variable can be defined when running the 'stack'
3. Portable templates contains 'parameters', some provided by user, some already exists as metadata(`AWS::Region`,  `AWS::AccountId`  etc)
4. Top-Level Objects include: Resources, Parameters, Mappings, Output  etc.
5. Example:
    ```yaml
       Parameters:
        LatestAmiId:
          Description: "AMI for EC2"
          Type: 'AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>'
          Default: '/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2'
      Resources:
        Bucket:
          Type: 'AWS::S3::Bucket'
        Instance:
          Type: 'AWS::EC2::Instance'
          Properties:
            InstanceType: "t2.micro"
            ImageId: !Ref "LatestAmiId"
    
    ```
7. 
8. 
