
###  VPC - Virtual Private Computing
1. Private,  isolated from other VPCs. Two EC2 can comm. if they are inside same VPC.  Regionally  Resillient.
2. A  range of  IP addresses = CIDR Range. 
3. To make it easier to get started, there is a "default  vpc" in every region and it has only one CIDR range(172.31.0.0/16 this one) and other "custom VPC" can be  setup and assigned more than one CIDR range.
4. Multiple private services can be connected together, privately...sort of an 'intra-net'.
5. Or a private service, say an EC2 inside a VPC, can be given a public ip via an Internet Gateway, to access the public internet.
6. Possible Scenario:  Our home network(private network) can connect to the internet(public network) which then connect to an AWS public service(e.g. S3) **or** a private  service(EC2 inside a VPC 'made'  public  by _VPN_ or _direct-connect_ )
7. 

###  EC2 - Elastic Compute Cloud
1. TCP port  3389  is used and must be allowed to RDP into an EC2 instance  and  for linux we can connect with ssh private-public key pair.
2. 
3. 

### S3
1. Object storage(like Redis!), not block storage(virtual hard drives EBS that we can mount  in our VMs), not File System(that we can browse like a file explorer in windows),
2. Region-based Resilliency. But each S3 bucket names have to be globally unique, just add '1234'! A bucket name cannot have underscores, upto 63 characters. 100 max limit of buckets can be increased upto 1000 through support tickets.
3. A bucket hold unlimited number of _objects_, each 0 bytes to 5TB. Each object's Filename is called 'object key'. folders are basically prefix in object names.
4. S3 Transfer Acceleration: Instead of using public internet to make the bucket avialable globally, use  'AWS Global network
   - to turn it on the bucket name must be DNS name compatible and cannot contain a period.
   - aws provides [a tool](https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html) to check how much difference it makes interms of speed and latency improvement.
   - 
6. 

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

### CloudWatch

1. It does not pull, the services push their logs into it. (It just 'watches').
2. Log = timestamped data; what happened at a certain time. Metrics= a number  measured  over period of time eg. CPU usage: average cpu metric.
   -  Traces: History of request that travels to  multiple apps/services, so that we can pinpoint failure/performance degradation
   -  
4. "log stream is a sequence of log events that share the same source." [docs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html)
5. Log Events(e.g.  a new entry in /var/log of an EC2 linux instance) --> Log Stream for each instances --> Log Groups --> Metric Filter --> Metric  --> Alarm.
<img width="1259" height="596" alt="image" src="https://github.com/user-attachments/assets/4e8e6d99-4e24-4796-9291-5fd0597cd1db" />
6. Logs Insights contain more filtering option that the lower level filter feature in log stream.
7. Install cloudwatch Agent via SSM  on a EC2 that has the 'CloudWatchAgentServerRole' permission.
8. 

### VPC Flow Logs
1. Any  data (in  the  network interface (ENI) level) that has got to do with flow of data into or out of VPC. not internal contents!
2. _Not Realtime_
3. Can be  accessed  from CloudWatch Logs or S3
4. Athena for querying

### CloudTrail
1. Regional service. _Not realtime_.
2. Trail implies investigation... auditing.
3. CloudTrails records(logs) each and every activity(by user,role,service) in AWS.
4. 90 days history free. 1 Trail/region is free. Only for Mgmnt events.
5. Example of events: Mgmnt(aka control-plane operation) events, data events, insight events, Network activity events(within a vpc)
6. Creating a "Trail" in a region enables us to pass the logs to CloudWatch, configure and save it in S3 bucket as compressed JSON.  Global services event logged in us-east1(n. virginia) but only after making a 'trail'
7. 

### AWS  Athena

1. Serverless querying service
2. Pay only for amount of data consumed, not hourly.  Data can be structured or unstructured.
3. We can apply  a schema on the data(xml,json,csv,avro,parquet,apache,cloudtrail,vpc flowlogs, aws glue data catalog, web server logs).
4. The data(sitting on  S3) remains unchanged! Gets structured by the schema mid-flight before query is applied..
5. Optimize the original data-set(s3)  to optmize cost.


### AWS Config
1.  Tracks changes to configuration of services,  resources and tracks  any compliance-breach(compliant/non-compliant)
2.  Cannot  prevent changges, only monitors them
3.  

###  KMS
1. Stores and lets users, applications, other aws service use Keys.
2. Does not let us download the keys.
3. Each key  are "logical"(not a physical keyfab) and contains: id,date, resource policy, desc & state
4. 




