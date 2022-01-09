# What it does

* This is a CloudFormation template for building a squid proxy in ECS.
* There are two CloudFormation templates: 1) for NLB and 2) for CloudMap.

## Image

   [NLB]
<img src="/images/nlb.png" >

   [CloudMap]
<img src="/images/Cloudmap.png" >

## Deployment

Deployments using Cloudformation templates target ECS (Cluster, Service, Task), IAM related to ECS, SecurityGroup releated to ECS, NLB or Cloudmap.

### Prerequisites

* The squid to be deployed must be registered in ECR (Private Registry). 
* If you use NLB, create a hostzone in Route53. 
* Because the NLB deployed by mkecs-squid-elb.yaml uses the proxy protocol, you need to add "proxy_protocol_access", "http_port [listen port] require-proxy-header" should be updated to the squid.conf.
* To make the squid definitions and logs persistent, configure a directory in EFS to place these files.

## Usage

    *Deploy

    [NLB]
    $ aws cloudformation deploy --template-file mkecs-squid-elb.yaml --stack-name sim-squid-elb-sn --capabilities CAPABILITY_NAMED_IAM

    [CloudMap]
    $ aws cloudformation deploy --template-file mkecs-squid-mz.yaml --stack-name sim-squid-mz-sn --capabilities CAPABILITY_NAMED_IAM

    *Update

    [NLB]
    $ aws cloudformation update-stack --template-body file:///mkecs-squid-elb.yaml --stack-name sim-squid-elb-sn --capabilities CAPABILITY_NAMED_IAM 

    [CloudMap]
    $ aws cloudformation update-stack --template-body file:///mkecs-squid-mz.yaml --stack-name sim-squid-mz-sn --capabilities CAPABILITY_NAMED_IAM
