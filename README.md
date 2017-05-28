# Lambda in Vpc

AWS CloudFormation script that demonstrates a Lambda function running within a VPC and accessing internet.

The script creates an S3 bucket, and a Lambda function that creates a record within that bucket, 
thereby demonstrating a route to the internet to invoke the S3 API.

The VPC that the Lambda function is associated with is created using the script in [VPC](https://github.com/gford1000-aws/vpc),
creating a public subnet and 3 private subnets (to which the Lambda is associated) by default.

The script creates a nested stack, constructing the VPC separately from the Lambda and S3 bucket, for clarity.  

Notes:

1. the VPC *must* have ```EnableDnsSupport = true``` so that DNS resolution of URLs can be performed.

2. the Lambda IAM Role includes ```ec2:CreateNetworkInterface```, ```ec2:DescribeNetworkInterfaces```, ```ec2:DeleteNetworkInterface``` to allow the ENI to be created within the VPC

3. the Lambda Security Group only allows egress via the VPC, and no ingress.


## Arguments

| Argument           | Description                                                        |
| ------------------ |:------------------------------------------------------------------:|
| CidrAddress        | First 2 elements of CIDR block, which is extended to be X.Y.0.0/16 |
| PrivateSubnetCount | The number of private subnets to be created (2-6 can be selected)  |
| VPCTemplateURL     | The S3 URL to the VPC template                                     |


## Outputs

| Output                  | Description                                                 |
| ----------------------- |:-----------------------------------------------------------:|
| Bucket                  | The name of the S3 bucket to which the Lambda will write    |
| Lambda                  | The name of the Lambda function                             |
| VPC                     | The reference to the VPC                                    |


## Licence

This project is released under the MIT license. See [LICENSE](LICENSE) for details.
