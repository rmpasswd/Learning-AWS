S3

1. bucket _versioning_ has 3 stages: disabled -> enabled <-> suspended -> disabled.  Enabled state can change to Suspended state but not disabled state
   - To delete specific version, mention the  ID.
   - if the ID is not mentioned, a 'delete  marker'  is places, hiding all older versions. If the 'delete marker'  is removed,  the object is 'un-deleted.
   - 
2. Single Upload vs Multi-part upload(requires file to be at least 100MB,  the last  fragment can be 5MB no prob)



IAM

1. In an s3 buckets  inline policy,  we can only  specify  access  controls for IAM  users,  not  groups!
2. Groups cannot be referred  as a 'principal' in a IAM   _policy_. But we can attached a managed _policy_ to a group.
3. 


CloudFormation:
1. The AMI image id (used  in template files) is unique for each  region. The ImageId in us-east-1 will not work if used inside a cloudFormation stack in  us-west-1 region.
2. 


Cost  Allocation Tag
-   Can  take upto 24  hours  to appear  in Billing and Cost Management console for activation. E.g. tagging prod. resources and dev to isolate billing stats.

- CloudTrail is not real-time
- Use other IdP Federation tools, such  as SAML 2.0 for 5000+ users. or if there are already  an existing on-premise identity  management platform in place.
- 






