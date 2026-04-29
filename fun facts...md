S3

1. bucket _versioning_ has 3 stages: disabled -> enabled <-> suspended -> disabled.  Enabled state can change to Suspended state but not disabled state
   - To delete specific version, mention the  ID.
   - if the ID is not mentioned, a 'delete  marker'  is places, hiding all older versions. If the 'delete marker'  is removed,  the object is 'un-deleted.
   - 
2. Single Upload vs Multi-part upload(requires file to be at least 100MB,  the last  fragment can be 5MB no prob)
3. If you try to add the following **bucket policy** you will encounter this error and nothing else: `Action does not apply to any resource(s) in statement`. Double resource name spelling but the real issue is that the permission 'ListBucket' cannot be used when targetting **objects** in the resource section. Fix is to not use listbucket! or do not use the `/*` and only use the bucket name, depending on your goal.
   - Bucket Policy:
     ```
           {
      	"Version": "2012-10-17",
      	"Statement": [
      		{
      			"Sid": "AllowReadonly",
      			"Principal": "*",
      			"Effect": "Allow",
      			"Action": ["s3:GetObject", "s3:ListBucket"],
      			"Resource": ["arn:aws:s3:::blog-fastapi-2026/profile_pics/*"]
      		}
      	]
      }
     ```


IAM

1. In an s3 buckets  inline policy,  we can only  specify  access  controls for IAM  users,  not  groups!
2. Groups cannot be referred  as a 'principal' in a IAM   _policy_. But we can attached a managed _policy_ to a group.
3. 


CloudFormation:
1. The AMI image id (used  in template files) is unique for each  region. The ImageId in us-east-1 will not work if used inside a cloudFormation stack in  us-west-1 region.
2. 

CloudWatch
1. CloudWatch only monitors the health of the resources that you own based on certain metrics but it does not check the underlying hardware that hosts the AWS resources. Use AWS Health Events  instead.
2.  




Cost  Allocation Tag
-   Can  take upto 24  hours  to appear  in Billing and Cost Management console for activation. E.g. tagging prod. resources and dev to isolate billing stats.

- CloudTrail is not real-time
- Use other IdP Federation tools, such  as SAML 2.0 for 5000+ users. or if there are already  an existing on-premise identity  management platform in place.
- 

- Two services,  AWS Direct Connect and dynamic VPNs,  use  Border  Gateway Protocol which is a routing protocol  used to control how data flows from point A to B, C  and finally the destination D.


EC2
1. An  instance can have EBS-backed or the default existing native Instance-store-backed. For the latter, all data will  be  lost when the EC2 instance  is stopped.   But EBS volumes can persist,  or exporting necessary  files to S3 bucket is another option.
2. 



