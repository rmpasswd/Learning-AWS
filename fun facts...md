IAM

1. In an s3 buckets  inline policy,  we can only  specify  access  controls for IAM  users,  not  groups!  Groups cannot be referred  as a 'principal' in a IAM   _policy_.


CloudFormation:
1. The AMI image id (used  in template files) is unique for each  region. The ImageId in us-east-1 will not work if used inside a cloudFormation stack in  us-west-1 region.
2. 
