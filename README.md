# VPC Peering

AWS CloudFormation scripts that show different VPC Peering approaches

## 1. [Simple VPC Peering](https://github.com/gford1000-aws/vpc-peering/blob/master/vpc-peering-example.cform)

In this example, two VPCs containing private subnets are peered together.  The VPCs are assumed to be created using the script in [VPC](https://github.com/gford1000-aws/vpc), taking the default values in that script.

The script creates the following:

![alt text](https://github.com/gford1000-aws/vpc-peering/blob/master/Simple%20peering%20between%20VPCs.png "Script per designer")

Notes:

* The two VPCs must have different CIDR blocks


## Arguments

| Argument           | Description                                               |
| ------------------ |:---------------------------------------------------------:|
| CidrAddressVPC1    | The initial X.Y of the CIDR X.Y.0.0/16 for the first VPC  |
| CidrAddressVPC2    | The initial X.Y of the CIDR X.Y.0.0/16 for the second VPC |
| VPCPeeringRole     | The value for the Role tag in the VPC Peering             |
| VPCTemplateURL     | The S3 url to the VPC Cloudformation script               |


## Outputs

| Output           | Description                        |
| ---------------- |:----------------------------------:|
| VPC1             | The resource id of the first VPC   |
| VPC2             | The resource id of the second VPC  |


## 2. [Multiple VPC Peering](https://github.com/gford1000-aws/vpc-peering/blob/master/multi-vpc-peering-example.cform)

In this example, four VPCs containing private subnets are peered together - showing the associative nature of VPC Peering.  Again all VPCs are assumed to be created using the script in [VPC](https://github.com/gford1000-aws/vpc), taking the default values in that script.

The script creates the following:

![alt text](https://github.com/gford1000-aws/vpc-peering/blob/master/Multi-vpc%20peering.png "Script per designer")

Notes:

* All VPCs must have different CIDR blocks.  For example, if VPC2 and VPC4 had the same CIDR range, then VPC1 and VPC3 cannot add routes to their respective route tables for both VPC2 and VPC4. 


## Arguments

| Argument           | Description                                               |
| ------------------ |:---------------------------------------------------------:|
| CidrAddressVPC1    | The initial X.Y of the CIDR X.Y.0.0/16 for the first VPC  |
| CidrAddressVPC2    | The initial X.Y of the CIDR X.Y.0.0/16 for the second VPC |
| CidrAddressVPC3    | The initial X.Y of the CIDR X.Y.0.0/16 for the third  VPC |
| CidrAddressVPC4    | The initial X.Y of the CIDR X.Y.0.0/16 for the fourth VPC |
| VPCPeeringRole     | The value for the Role tag in the VPC Peering             |
| VPCTemplateURL     | The S3 url to the VPC Cloudformation script               |


## Outputs

| Output           | Description                        |
| ---------------- |:----------------------------------:|
| VPC1             | The resource id of the first VPC   |
| VPC2             | The resource id of the second VPC  |
| VPC3             | The resource id of the third VPC   |
| VPC4             | The resource id of the fourth VPC  |

## 3. [Peering to JumpBox VPC](https://github.com/gford1000-aws/vpc-peering/blob/master/vpc-peering-jumpbox-example.cform)

In this example, a private VPC is created (no internet access), along with a second VPC containing a JumpBox server that should have access to the private VPC.  The
private VPC uses the normal [script](https://github.com/gford1000-aws/vpc), whilst the JumpBox VPC is created using the [robust JumpBox](https://github.com/gford1000-aws/robust-jumpbox-in-isolated-vpc/blob/master/create_jumpbox_asg_in_vpc.cform) script.

Since the Jumpbox VPC network access is explicitly controlled via Network ACL entries, additional entries must be added to allow the JumpBox server to access servers in the private VPC.  Note that the access is one-way: once on an EC2 instance in the private VPC, there is no access back to the JumpBox (and therefore nor to the internet).

The script creates the following:

![alt text](https://github.com/gford1000-aws/vpc-peering/blob/master/Screen%20Shot%202017-06-17%20at%202.39.46%20PM.png "Script per designer")


## Arguments

| Argument                  | Description                                                        |
| ------------------------- |:------------------------------------------------------------------:|
| AllowedCIDRRangeToJumpBox | The CIDR address block that can access the VPC                     |
| InstanceAmiId             | The AMI used for the JumpBox instance                              |
| InstanceType              | The instance type (default t2.micro) for the JumpBox instance      |
| JumpBoxCidrAddress        | First 2 elements of CIDR block, which is extended to be X.Y.0.0/16 |
| JumpBoxTemplateURL        | The S3 URL to the JumpBox VPC template                             |
| KeyName                   | The KeyName required to access the JumpBox instance                |
| PrivateVPCCidrAddress     | First 2 elements of CIDR block, which is extened to be X.Y.0.0/16  |
| VPCPeeringRole            | The value for the 'Role' tag of the VPC Peering                    |              
| VPCTemplateURL            | The S3 URL to the VPC template                                     |


## Outputs

| Output        | Description                          |
| ------------- |:------------------------------------:|
| PrivateVPC    | The resource id of the private VPC   |
| JumpBoxVPC    | The resource id of the JumpBox VPC   |
| EIP           | The Elastic IP of the JumpBox server |


## Licence

This project is released under the MIT license. See [LICENSE](LICENSE) for details.
